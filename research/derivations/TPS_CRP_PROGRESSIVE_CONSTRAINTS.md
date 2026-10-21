# TPS-CRP Progressive Constraints and Image-Space Feedback

**Status:** Research — Proposed Method, Not Physically Validated
**Scope:** Mathematical reasoning for the experimental TPS Camera Recovery Procedure (TPS-CRP) v0.1.
**Authority:** Non-normative research. This document does not change the TPS Specification or TPS-CRP v0.1.

## 1. Purpose

TPS recovery compares a recorded three-point projection with a current camera projection. The proposed progressive method does not solve a camera pose from three points. It organizes the available image observations so that an operator can begin with useful, interpretable comparisons and then introduce the third point while continuing to inspect the whole image.

The central research question is whether this staged presentation improves practical conditioning and operator feedback compared with attempting to adjust all available controls without an intermediate A/B comparison. That is a hypothesis. No physical result is claimed here.

The canonical TPS concepts remain in [`../../SPECIFICATION.md`](../../SPECIFICATION.md), [`../../docs/DEFINITIONS.md`](../../docs/DEFINITIONS.md), and [`../../docs/USE_CASES.md`](../../docs/USE_CASES.md). The operator-facing procedure is [`../../docs/TPS_CAMERA_RECOVERY_PROCEDURE.md`](../../docs/TPS_CAMERA_RECOVERY_PROCEDURE.md).

## 2. Definitions and notation

Let the physical reference points be A, B, and C. Their corresponding image points in the recorded reference are a, b, and c. The current camera view produces corresponding image observations `a'`, `b'`, and `c'`.

Use one declared image coordinate frame for both views. For a conventional raster frame:

- `u` increases to the right;
- `v` increases downward;
- coordinates are expressed in pixels, or in normalized image units after an explicitly documented normalization;
- all points are compared only after orientation, crop, scale, mirror state, and registration have been accounted for.

Define the six-observation vectors:

```text
P_target   = [uA, vA, uB, vB, uC, vC]^T
P_current  = [uA', vA', uB', vB', uC', vC']^T
```

The target/current residual is:

```text
e = P_target - P_current
```

Thus `e` has six components, with the same image-coordinate units as `P`. A positive residual means that the current observation is lower in that coordinate than the target under the selected convention.

The recorded three-point projection is an image-space reference. It does not by itself establish a world coordinate origin, a unique camera pose, or a complete lens model.

## 3. Camera variables and local model

Let the adjustable camera state be represented locally by:

```text
q = [q1, q2, ..., qn]^T
```

The entries may include translations, rotations, focal length, focus state, or rig-specific controls. A six-variable rigid-camera example is:

```text
q = [x, y, z, pan, tilt, roll]^T
```

This is only a local model. The axes must be declared for the particular rig; `z` is not automatically world depth, camera-local depth, or the rig’s named `zT`. Focal length, focus, crop, active sensor area, and image registration may also be free or uncertain variables.

The projection function is written abstractly as:

```text
P(q) = [uA(q), vA(q), uB(q), vB(q), uC(q), vC(q)]^T
```

Near a current state `q0`, a first-order approximation is:

```text
P(q0 + Δq) ≈ P(q0) + J(q0) Δq
```

where the Jacobian is:

```text
J(q0) = ∂P/∂q |q0
```

For six image observations and `n` local controls, `J` has dimensions `6 × n`. With six local camera variables it is `6 × 6`; with an additional focal-length or focus variable it may be `6 × 7` or larger. Its rows correspond to image coordinates and its columns to the selected controls.

To reduce the residual locally, the linearized correction satisfies approximately:

```text
J Δq ≈ e
```

One conditional least-squares estimate is:

```text
Δq ≈ J⁺ e
```

where `J⁺` is the Moore–Penrose pseudoinverse. This estimate is meaningful only after the controls, units, registration, and local model have been declared. It is not a camera solver, does not guarantee convergence, and does not select a unique global solution. In practice, a damped or weighted estimate may be safer:

```text
Δq ≈ (Jᵀ W J + λ² I)⁻¹ Jᵀ W e
```

with an explicitly chosen observation weight matrix `W` and damping parameter `λ`. This equation is a research formulation only; no value of `W` or `λ` is prescribed by TPS.

## 4. A/B image-space quantities

The A/B Base Pair provides four scalar image observations. It can also be summarized by separation, midpoint, and orientation.

Let:

```text
dAB = b - a = [uB - uA, vB - vA]^T
mAB = (a + b) / 2
θAB = atan2(vB - vA, uB - uA)
sAB = ||dAB||
```

Here `dAB` is the directed image-space separation vector, `mAB` is the midpoint, `θAB` is the directed image orientation, and `sAB` is the Euclidean image separation. The same quantities are computed for the current view using `a'` and `b'`.

The quantity residuals are:

```text
e_d   = dAB_target - dAB_current
e_m   = mAB_target - mAB_current
e_s   = sAB_target - sAB_current
e_θ   = wrap(θAB_target - θAB_current)
```

`wrap` maps the angle difference into a declared interval such as `(-π, π]`. The vector residuals `e_d` and `e_m` have image units; `e_s` has image units; `e_θ` is in radians or degrees according to the declared convention.

These summaries are not independent observations in addition to A and B. They are different representations of the same four coordinates. In particular, separation, midpoint, and orientation should not be counted as seven new constraints. A/B quantities are useful because they provide an operator-readable decomposition:

- separation exposes scale and relative displacement;
- midpoint exposes common translation of the pair;
- orientation exposes the pair’s image angle;
- the two point residuals retain the full information.

The derivatives of the basic quantities show how their sensitivities are formed. For a small change in point coordinates:

```text
δdAB = δb - δa
δmAB = (δa + δb) / 2
δsAB ≈ (dAB / ||dAB||) · δdAB       when ||dAB|| > 0
δθAB ≈ (-dy δdx + dx δdy) / (dx² + dy²)
```

where `dAB = [dx, dy]^T`. The orientation derivative becomes unstable as the pair approaches coincidence. The separation derivative is also poorly conditioned when the pair is very short or when pixel uncertainty is large relative to its length.

## 5. Progressive constraint stages

Progressive constraints mean progressive observation and feedback, not progressive proof that camera degrees of freedom have been eliminated.

### Stage 1 — Recorded tilt and roll references

The operator establishes recorded tilt and roll as initial conditions when those measurements are available and their sign conventions are known. These values provide orientation references and can reduce avoidable starting error.

They do not determine complete camera orientation. A shared UP direction is not a shared origin, and measured tilt or roll may be affected by instrument placement, rig pivots, reference surfaces, and sign conventions.

### Stage 2 — Approximate focal length, distance, and scale

The operator restores the recorded Working Focal Length, TPS Reference Distance, focus condition, and image-gate/crop condition as closely as practical. The existing TPS Working Focal Length equations remain the approved calculation convention under their stated assumptions; this document does not redefine them.

This stage attempts to reduce global scale disagreement before positional refinement. It cannot determine whether a scale error came from distance, focal length, focus breathing, crop, active sensor area, or registration error without additional evidence.

### Stage 3 — Compare A/B projected separation

Compare `sAB` or the full `dAB` vector between the reference and current views. The observation can indicate that the pair’s projected scale or relative displacement differs.

It cannot uniquely determine camera distance, focal length, or any single translation. A change in depth, focal length, focus, sensor gate, or point depth can produce related image effects.

### Stage 4 — Compare A/B projected midpoint

Compare `mAB_target` and `mAB_current`. The midpoint describes common displacement of the pair in the registered image.

It can provide useful feedback for horizontal or vertical image displacement. It cannot uniquely identify pan, lateral translation, camera height, tilt, or a rig pivot. The local response depends on the camera model, axis convention, point depths, and current configuration.

### Stage 5 — Compare A/B projected orientation

Compare `θAB_target` and `θAB_current`. The angle can reveal an image rotation or a change in the pair’s relative direction.

It cannot uniquely establish camera roll. Tilt, point-depth differences, perspective, a non-level physical arrangement, crop/registration error, and coupled rig movements may also change the observed orientation. The orientation quantity becomes unreliable for a near-coincident or nearly unresolved pair.

### Stage 6 — Introduce point C

Point C adds two image-space observations:

```text
e_C = [uC_target - uC_current,
       vC_target - vC_current]^T
```

The complete residual is now:

```text
e = [e_A, e_B, e_C]^T
```

where each `e_*` is a two-component image residual. C can reveal disagreement that is hidden by an A/B-only comparison, especially when C differs in depth or location. It does not uniquely determine pan, depth, or any remaining camera axis. Its diagnostic value depends on geometry, visibility, image registration, and the local rank and conditioning of `J`.

### Stage 7 — Refine using all points

The operator makes small adjustments while evaluating A, B, C, and stable scene features outside the triangle. A local response model can be estimated or updated from observed movements. The objective is to reduce the registered image residual without allowing one point to be improved at the unexplained expense of the others.

### Stage 8 — Evaluate the surrounding image

Agreement at A, B, and C is not proof that the entire scene or camera pose matches. Compare stable features outside the triangle and record lighting, focus, distortion, set changes, and other differences. Whole-image evaluation is a separate practical check.

## 6. Why A/B first may help

The proposed benefit of A/B-first operation is interpretability, not added mathematical information. A/B provides a compact foundation for observing:

- common versus relative image displacement;
- pair separation and apparent scale;
- pair orientation;
- whether a change improves both points together or only one point.

This may improve operator feedback by making an early mismatch easier to describe and by reducing the number of visible competing residuals. It may also provide a useful starting state for estimating a local response matrix.

The benefit is conditional. A/B may be nearly degenerate, at similar image locations, poorly identified, or unrepresentative of the rest of the scene. Progressive presentation can also create anchoring bias: an operator may preserve an A/B match even when a different adjustment would produce a better whole-view result. These are empirical questions.

## 7. Rank, observability, and coupled controls

The rank of `J` describes how many locally independent image-motion directions the selected controls produce at the current configuration. It does not count camera degrees of freedom by itself.

- If `rank(J) < n`, some local control combinations cannot be distinguished from the selected image observations.
- If `rank(J) = n` for a square or overdetermined local model, a local correction may be identifiable under the model, but global uniqueness still does not follow.
- A high condition number or small singular values indicate sensitivity: small image or measurement errors may produce large changes in the estimated correction.
- With only A/B, the observation vector has four scalar coordinates. A six-variable camera model therefore cannot generally be identified from A/B alone.
- With A/B/C, there are six scalar image coordinates, but six observations do not guarantee six independent constraints. Point geometry, camera configuration, intrinsic parameters, and control coupling determine rank.

Pan, horizontal translation, tilt, height, axial translation, focal length, and focus may have similar or coupled image signatures. A local column of `J` should therefore not be interpreted as a universal one-control diagnosis. Rig-specific pivots and coordinate conventions are part of the model.

## 8. Experimental Jacobian estimation

A local Jacobian can be estimated from controlled perturbations without claiming a global camera solve.

For each selected control `qj`:

1. Record the current registered observations `P(q0)`.
2. Apply a small, known perturbation `+δqj` while holding other controls as constant as practical.
3. Record `P(q0 + δqj)`.
4. Estimate the column:

```text
J[:, j] ≈ (P(q0 + δqj) - P(q0)) / δqj
```

5. Where safe and repeatable, repeat with `-δqj` and use a central difference:

```text
J[:, j] ≈ (P(q0 + δqj) - P(q0 - δqj)) / (2 δqj)
```

The perturbation must be large enough to rise above point-picking and image-registration noise but small enough for the local linear approximation to remain reasonable. Repeat measurements estimate variability. The resulting matrix is local to the rig, lens, focus, point geometry, crop, and current camera state.

An experiment may compare the observed displacement with `J Δq`, inspect singular values, and test whether a bounded pseudoinverse correction reduces the residual on a subsequent trial. This would test local feedback usefulness, not establish a universal TPS algorithm.

## Tilt, Reference Distance, and Conditional Position Estimates

The canonical TPS Reference Distance `D` is measured from a camera sensor-plane mark toward the estimated midpoint of the physical A–B Base Pair. It is a practical measurement convention, distinct from focus distance, a lens focus-ring marking, optical-center distance, or a manufacturer-reported focus distance. The existing TPS definition does not identify `D` automatically with a camera-forward depth or a line-of-sight segment.

Measured camera tilt is a camera-orientation measurement relative to a declared reference such as gravity, UP, a camera surface, or a rig axis. The inclination of the reference-distance vector is the angle of the particular physical segment represented by `D`. These are not automatically the same angle. They coincide only if the measured camera axis, the distance vector, the selected vertical/horizontal plane, and the inclinometer convention are explicitly related.

### Conditional right-triangle construction

Suppose, as an additional research assumption, that:

- `D` is the straight-line segment between the selected sensor-plane endpoint and the selected A–B midpoint endpoint;
- that segment lies in one vertical plane;
- the plane has declared horizontal and vertical axes;
- `θ` is the inclination of that same segment, measured from horizontal;
- the endpoints and angle use the same sign and coordinate conventions.

Only under these assumptions, the segment can be treated as the hypotenuse of a right triangle:

```text
Δhorizontal = D cos(θ)
Δvertical   = D sin(θ)
```

If `θ` is measured from vertical instead, the components become:

```text
Δhorizontal = D sin(θ)
Δvertical   = D cos(θ)
```

The signs depend on the declared direction of each axis. These are elementary component relationships for the assumed segment; they are not additional TPS equations and do not redefine the canonical `D` convention.

### Why this does not establish absolute camera position

The component equations describe a displacement between two selected endpoints. They do not identify a world origin, camera center, optical center, rig origin, or absolute height/depth. A sensor-plane mark is not automatically the projection center, and the A–B midpoint may lie on a plane whose orientation and position have not been fully measured. Camera tilt alone also leaves other orientation and translation variables unresolved.

To use the construction for a physical position estimate, the experiment would additionally need the endpoint coordinates or a surveyed reference frame, the exact sensor-plane-to-reference segment, the A–B midpoint’s position and plane orientation, the camera/rig axis mapping, the tilt and angle zero conventions, and a declared target such as sensor-plane position, projection-center position, or rig position. Without those data, the result is at most a conditional local offset or starting estimate.

### Uncertainty

If the conditional components are used, uncertainty in `D` and `θ` propagates into the estimates. For `θ` measured from horizontal:

```text
σ²_horizontal ≈ (cos(θ) σ_D)² + (D sin(θ) σ_θ)²
σ²_vertical   ≈ (sin(θ) σ_D)² + (D cos(θ) σ_θ)²
```

where `σ_θ` is expressed in radians and independent-error propagation is assumed. Correlated errors, endpoint ambiguity, plane tilt, inclinometer placement, and systematic sensor-plane/projection-center offset can add further error. These expressions are uncertainty estimates for the conditional construction, not validated TPS accuracy measures.

### zT and zR

`zT` denotes Z-axis translation and `zR` denotes Z-axis rotation only after a rig coordinate frame has been declared. Neither symbol is automatically world-Z motion, camera-local axial motion, optical-axis rotation, or image roll. A rig-axis-to-camera-twist mapping is required before interpreting either variable physically. The existing research provides a conditional camera-local axial-translation model for `zT`-like motion, but it does not establish a universal `zT` correction or a dedicated rig-specific `zR` equation.

This conditional geometry is discussed in [PROJECTION_SPACE_AND_LINEUP.md](PROJECTION_SPACE_AND_LINEUP.md), [TPS_CAMERA_LINEUP_GEOMETRY.md](../methods/TPS_CAMERA_LINEUP_GEOMETRY.md), and [WORKING_FOCAL_LENGTH.md](WORKING_FOCAL_LENGTH.md). Those documents preserve the same boundary: the construction remains research material until its geometry, conventions, uncertainty, and physical behavior are defined and tested.

## 9. Units, weighting, and uncertainty

Use consistent units within each calculation:

- image coordinates: pixels or normalized image units;
- translations: a declared physical unit or rig unit;
- rotations: radians for derivatives, with degrees allowed for operator display;
- focal length and sensor dimensions: the units declared by the TPS calculation;
- distances and triangle sides: the recorded physical units.

If image observations have unequal uncertainty, a weighted residual is more honest than treating all coordinates as equally precise:

```text
minimize ||W^(1/2)(e - J Δq)||²
```

Weights may reflect point size, visibility, blur, image registration, or coordinate precision. No universal weights are defined here.

Uncertainty enters through point placement, physical measurements, tilt/roll instruments, focal-length assumptions, focus breathing, sensor dimensions, crop, lens distortion, and rig repeatability. A correction direction should be presented as uncertain when multiple controls have similar Jacobian columns, when singular values are small, or when the residual is comparable to observation noise.

An operator-facing implementation should prefer language such as “try a small horizontal adjustment; confidence is low” over an unconditional claim that one physical axis is responsible.

## 10. Registration, focal length, and crop dependencies

All residuals are meaningful only in a consistently registered image frame. Before interpreting a camera mismatch, verify:

- image orientation and mirroring;
- captured dimensions and display dimensions;
- crop and active image gate;
- aspect ratio and pixel aspect;
- overlay scale and position;
- principal-point or framing changes when relevant.

An unregistered overlay can produce residuals that look like camera movement. A crop can change point coordinates without changing the underlying camera. A focal-length or focus change can change A/B separation and the apparent scale of the whole image. These effects must remain possible explanations until controlled or measured.

## 11. Failure and degeneracy cases

The proposed method becomes weak or ambiguous when:

- A and B are too close in the image to estimate separation or orientation reliably;
- A, B, and C are collinear, coincident, occluded, or poorly identifiable;
- all points lie at nearly the same image location or provide insufficient depth diversity for the intended diagnostic;
- point labels are swapped between the reference and current view;
- the reference and live images are cropped, mirrored, rotated, or scaled inconsistently;
- the rig motion changes multiple controls together;
- lens focus, focal length, distortion, or active sensor area changes;
- the physical reference or scene deforms;
- the camera is outside the local neighborhood where the Jacobian was estimated;
- the target is not reachable under the available controls;
- the local Jacobian is rank-deficient or poorly conditioned.

In these cases, the correct result may be “ambiguous” or “not recoverable under the recorded conditions,” not a forced camera-axis diagnosis.

## 12. Research questions and validation plan

### 12.1 Does progressive feedback improve conditioning or operation?

Compare an A/B-first procedure with an all-points procedure under the same equipment and starting errors. Measure:

- time to a declared practical match;
- number and magnitude of control changes;
- A/B/C residuals after each adjustment;
- residuals at independent scene features;
- operator confidence and correction reversals;
- repeatability across operators and sessions;
- failure and ambiguity rates.

No result should be reported until the tests are performed.

### 12.2 What conditions permit individual adjustment estimates?

Estimate the rig-specific Jacobian under controlled perturbations. Test whether candidate controls produce distinguishable columns and whether the result is stable across camera distance, point geometry, lens/focus state, and crop. A control can be estimated only conditionally on the local model and measurement quality.

### 12.3 What must be measured?

At minimum, a validation record should preserve:

- camera, lens, focus, capture mode, and image dimensions;
- physical A/B/C identities and measurements;
- TPS Reference Distance and Working Focal Length inputs;
- tilt and roll instruments, surfaces, signs, and accuracy;
- rig axis definitions and control perturbations;
- overlay registration method;
- target/current point coordinates and uncertainty estimates;
- full-image comparison features outside A/B/C;
- repeated trials, operator, environment, and failure cases.

The existing physical validation plan in [`../../docs/VALIDATION.md`](../../docs/VALIDATION.md) and [`../../validation/`](../../validation/) remains the governing evidence structure. Those tests are currently marked **Not Yet Performed**.

## 13. Relationship to TPS-CRP v0.1

This document supplies mathematical interpretation for the experimental TPS-CRP sequence:

| TPS-CRP step | Image-space interpretation |
|---|---|
| Match tilt | Establish an orientation reference and initial condition. |
| Match roll | Establish a second orientation reference when available. |
| Match distance using A/B scale | Compare A/B separation and scale-related residuals. |
| Match horizontal position | Compare A/B midpoint and full point residuals. |
| Match camera height | Examine vertical residuals without treating height as uniquely identified. |
| Use C for pan and top-point completion | Add the two C observations and continue monitoring A/B. |
| Fine-check A/B/C | Use the complete residual and local feedback. |
| Operator approval | Evaluate the whole composition and record practical acceptance. |

The table explains the procedure; it does not add requirements to TPS or prove that each step isolates the named camera adjustment.

## 14. Possible future relationship to LIMNTPS Align

The framework could support a future LIMNTPS Align system in limited, conditional ways:

- maintain registered target/current point observations;
- display A/B summaries and the C residual;
- estimate a rig-specific local response matrix from controlled movements;
- report correction suggestions with confidence and ambiguity;
- preserve adjustment history and evidence;
- compare independent scene features after the three-point match.

It should not silently become an automatic six-degree-of-freedom solver. Any live guidance would need declared camera, lens, rig, coordinate, registration, and uncertainty models. The current LIMNTPS marketplace scope and TPS-CRP do not require this behavior.

## 15. Relationship to existing research and conflicts

This derivation is consistent with the existing research in treating A/B-first alignment as a proposed operator strategy, C as additional image evidence, and `ΔP ≈ J Δq` as a local approximation. It preserves the existing warnings that:

- the physical triangle and image triangle are distinct;
- three-point agreement does not guarantee whole-image agreement;
- three points do not guarantee a unique camera pose;
- rig controls are coupled;
- the Working Focal Length is approximate under stated assumptions;
- practical validation remains outstanding.

One terminology caution remains: “progressive constraints” can sound as though each stage mathematically removes camera degrees of freedom. In this document it means progressive observation, conditioning, and operator feedback. A/B summaries are derived from the same four A/B coordinates, and adding C adds observations without guaranteeing independent rank. That distinction should remain explicit in any future implementation or normative proposal.

## References

- [`../../SPECIFICATION.md`](../../SPECIFICATION.md)
- [`../../docs/DEFINITIONS.md`](../../docs/DEFINITIONS.md)
- [`../../docs/TPS_CAMERA_RECOVERY_PROCEDURE.md`](../../docs/TPS_CAMERA_RECOVERY_PROCEDURE.md)
- [`PROJECTION_SPACE_AND_LINEUP.md`](PROJECTION_SPACE_AND_LINEUP.md)
- [`../methods/TPS_CAMERA_LINEUP_GEOMETRY.md`](../methods/TPS_CAMERA_LINEUP_GEOMETRY.md)
- [`../methods/TPS_PHYSICAL_LINEUP_PROCEDURE_REVIEW.md`](../methods/TPS_PHYSICAL_LINEUP_PROCEDURE_REVIEW.md)
- [`../methods/TPS_LINEUP_MATHEMATICAL_VERIFICATION.md`](../methods/TPS_LINEUP_MATHEMATICAL_VERIFICATION.md)
- [`../../docs/VALIDATION.md`](../../docs/VALIDATION.md)
