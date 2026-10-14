# TPS Lineup — Mathematical Verification Report

**Status:** Research verification draft; not a normative amendment to TPS Specification v0.1.

## 1. Scope and conclusion

This report independently checks the perspective-motion equations, sign conventions, numerical example, tilt/reference-distance construction, and staged A–B → C lineup reasoning in `TPS_CAMERA_LINEUP_GEOMETRY.md`.

The principal result is positive: the image Jacobian in the lineup draft is correct for its stated convention. The convention is:

- Camera coordinates are right-handed: `X` is image-right, `Y` is image-up, and `Z` is forward from the camera into the scene.
- A static world point has camera coordinates `P=(X,Y,Z)` with `Z>0`.
- `v=(v_x,v_y,v_z)` is camera-center velocity expressed in camera coordinates.
- `ω=(ω_x,ω_y,ω_z)` is camera angular velocity expressed in camera coordinates.
- Positive camera motion changes point coordinates by `P_dot = -v - ω × P`.
- Perspective projection is `x=X/Z`, `y=Y/Z`, `u=f_x x+c_x`, and `v_image=f_y y+c_y`.

The draft contained one trigonometric wording error in its tilt/reference-distance discussion. It stated the `D sin θ`/`D cos θ` assignment in a way that reversed the stated horizontal/vertical angle interpretation. That paragraph has been corrected in the research draft. The correction does not change TPS canonical mathematics or the approved meaning of `D`.

The A–B → C sequence is mathematically plausible as a staged operator heuristic, but it does not follow as a universally optimal or uniquely determined algorithm. A depth-separated C can improve sensitivity to some translation modes, while an equal-depth or poorly placed C may not. The sequence remains a proposed method requiring experiments.

## 2. Independent Jacobian derivation

Let:

```text
P = (X, Y, Z)
x = X/Z
y = Y/Z
```

For camera translation and rotation under the declared convention:

```text
X_dot = -v_x - ω_y Z + ω_z Y
Y_dot = -v_y - ω_z X + ω_x Z
Z_dot = -v_z - ω_x Y + ω_y X
```

Using the quotient rule:

```text
x_dot = (X_dot Z - X Z_dot) / Z²
y_dot = (Y_dot Z - Y Z_dot) / Z²
```

Substituting `X=xZ` and `Y=yZ` gives:

```text
x_dot = -v_x/Z + x v_z/Z
         + x y ω_x - (1+x²) ω_y + y ω_z

y_dot = -v_y/Z + y v_z/Z
         + (1+y²) ω_x - x y ω_y - x ω_z
```

Therefore:

```text
[x_dot]   [ -1/Z   0    x/Z     x*y    -(1+x²)    y ] [v_x]
[y_dot] = [  0   -1/Z   y/Z   (1+y²)    -x*y     -x ] [v_y]
                                                       [v_z]
                                                       [ω_x]
                                                       [ω_y]
                                                       [ω_z]
```

The matrix in the lineup draft is therefore internally consistent with its stated camera-motion convention. Pixel derivatives are:

```text
u_dot = f_x x_dot
v_image_dot = f_y y_dot
```

for fixed intrinsics and no distortion, crop, or rolling-shutter terms.

The signs are convention-dependent. If `v` denotes point velocity rather than camera-center velocity, or if positive camera axes are defined differently, translation signs change. A publication-quality version must retain the convention next to the matrix.

## 3. Motion interpretation

### 3.1 Lateral translation

For positive camera-center translation `v_x`, with orientation fixed:

```text
u_dot_i = -f_x v_x/Z_i
```

All points move in the negative image-horizontal direction for positive `v_x` under this convention. The differential between points A and C is:

```text
u_dot_C - u_dot_A = -f_x v_x (1/Z_C - 1/Z_A)
```

If `Z_C = Z_A`, this differential is zero. Thus depth separation is useful for diagnosing this particular lateral-translation cue. It is not a universal requirement for TPS correspondence.

### 3.2 Axial translation

For positive camera-center translation `v_z`:

```text
u_dot_i = f_x x_i v_z/Z_i
v_image_dot_i = f_y y_i v_z/Z_i
```

The image expands about the principal point for points with positive normalized coordinates and contracts toward it for negative coordinates, under the declared convention. A point on the principal point has no first-order axial image displacement. Therefore axial translation cannot be diagnosed reliably from a point configuration concentrated at or near the principal point.

This verifies the draft's statement that `zT` can produce depth-dependent expansion/contraction. It does not prove that `zT` is the correct or sole adjustment for every residual at C.

### 3.3 Rotation

For positive camera angular velocities:

```text
ω_x: x_dot = x y ω_x,       y_dot = (1+y²) ω_x
ω_y: x_dot = -(1+x²) ω_y,  y_dot = -x y ω_y
ω_z: x_dot = y ω_z,         y_dot = -x ω_z
```

These are image-space effects for rotations about camera-local axes. A physical pan, tilt, or roll control may not be a pure camera-local rotation because its mechanical pivot can be displaced from the projection center. The rig's joint-to-camera kinematics must then be included. Consequently, “pan,” “tilt,” and “roll” cannot be assigned universal image effects without a declared rig frame and pivot geometry.

## 4. Numerical example recalculation

The draft uses:

```text
W_image = 1920 px
f_x = 1200 px
c_x = 960 px
Z_A = Z_B = 2.0 m
AB = 0.40 m
```

For a centered horizontal base pair:

```text
u_A = 960 - (1200 × 0.20 / 2.0) = 840 px
u_B = 960 + (1200 × 0.20 / 2.0) = 1080 px
Δu_AB = 1080 - 840 = 240 px
```

Using `D=2.0 m` as the TPS approximation:

```text
f_px = 240 × 2.0 / 0.40 = 1200 px
AOV_h = 2 atan(1920 / (2 × 1200))
      ≈ 77.32°
```

These calculations are correct and dimensionally consistent under the stated ideal assumptions.

For a lateral camera-center translation `v_x=0.010 m`:

```text
Δu_A = -1200 × 0.010 / 2.0 = -6 px
Δu_C = -1200 × 0.010 / 3.0 = -4 px
Δu_C - Δu_A = +2 px
```

More precisely, these are the first-order image displacements associated with the stated 10 mm motion. The result is a 2 px differential under the ideal model.

For axial camera-center translation `v_z=0.010 m`, a point with `u-c_x=120 px` has `x=120/1200=0.1`:

```text
Δu_A ≈ 1200 × 0.1 × 0.010 / 2.0 = +0.6 px
Δu_C ≈ 1200 × 0.1 × 0.010 / 3.0 = +0.4 px
```

The sign is positive because the report defines positive camera-center motion along +Z and uses `P_dot=-v` for static scene points. A different translation convention reverses the sign.

The example is mathematically correct as an idealized first-order calculation. It is not an accuracy claim. Lens distortion, marking uncertainty, pixel sampling, focus changes, mechanical play, and the difference between D and projection-center depth may exceed the predicted displacement.

## 5. Jacobian rank and conditioning

For three points, stack the three 2×6 point Jacobians to form a 6×6 image-motion Jacobian. Six scalar image residuals do not guarantee rank six.

Important cases include:

- Coincident or nearly coincident image points.
- Collinear or nearly collinear projected points.
- Points with weak spatial spread in the image.
- Points at similar depths when relying on lateral-translation parallax.
- Points near the principal point when relying on axial-translation expansion.
- Unknown focal length, principal point, distortion, or crop included as free variables.
- Mechanical pivots that couple nominal rig axes.
- Physical point movement, misidentification, occlusion, or marking noise.
- A constrained procedure in which tilt or other variables are locked.

Conditioning depends on the actual 3D coordinates, camera orientation, intrinsics, and units used to scale translations and rotations. Singular values of a sensibly normalized Jacobian are appropriate diagnostics. No universal “best triangle” follows from the six-observation count alone.

## 6. Verification of the staged A–B → C procedure

The proposed sequence has a defensible operational rationale:

1. Locking tilt and stabilizing optical state reduces the number of actively changing variables.
2. A/B supplies four visible residual components and useful midpoint, separation, and orientation summaries.
3. C supplies two additional residual components and can reveal depth-dependent disagreement.
4. Iterating A/B after C is necessary because controls are coupled.

The mathematical justification is conditional, not absolute. A/B does not isolate pan, height, or horizontal translation. A/B alignment can be reproduced by compensating changes in depth, focal state, rotation, or pivot position. C can help distinguish some alternatives, but it does not uniquely identify `zT` or any other control.

The staged method may have a practical advantage over simultaneous unconstrained adjustment by reducing the operator's active search space and making residuals easier to interpret. This is a hypothesis about usability and convergence, not a theorem. To establish an advantage, compare the staged procedure with a defined simultaneous or unguided baseline using time to convergence, adjustment count, final point residuals, off-triangle landmark residuals, operator variability, and failure rate.

The staged procedure can be expressed as progressively constrained adjustment, but “progressively constrained” must not be confused with mathematically optimal. Locking tilt removes or restricts a degree of freedom; stabilizing optics removes a changing nuisance variable; A/B-first and C-second select an observation order. None proves global convergence or superiority.

## 7. Tilt/reference-distance verification

The corrected draft now uses the following convention:

- If `θ` is measured from horizontal, vertical component `ΔH=D sin θ` and horizontal-forward component `ΔZ=D cos θ`.
- If `θ` is measured from vertical, `ΔH=D cos θ` and `ΔZ=D sin θ`.
- These formulas require `D` to be the slanted segment between the same endpoints in the same vertical plane.

The canonical TPS definition measures D from a sensor-plane mark to a designated physical reference plane. The clarified operator convention targets the estimated A–B midpoint. That measurement does not automatically establish a slanted hypotenuse or a camera-forward-axis distance. The right-triangle construction therefore remains conditional and must not be inserted into the canonical Working Focal Length equations without an additional geometric definition.

## 8. Corrections and recommendations

Applied to `TPS_CAMERA_LINEUP_GEOMETRY.md`:

- Corrected the angle-reference wording for the `sin`/`cos` component relationships.
- Preserved the explicit warning that the triangle requires matching endpoints, axes, and a slanted D measurement.

Recommended for later review, not applied to the canonical specification:

- Retain the Jacobian with its camera-center velocity convention adjacent to the equation.
- Keep `zT` as a rig-frame workflow notation and empirical heuristic.
- Treat depth-separated C as advantageous for selected diagnostics, not mandatory.
- Keep tilt locking, A/B-first ordering, focus-state stabilization, and troubleshooting as research-method or recommended-practice material.
- Add an authoritative image-based visual-servoing reference before publication if the Jacobian is retained as a literature-backed claim.

## 9. Verification status

| Item | Result | Status |
|---|---|---|
| Six-DOF image Jacobian | Matches independent derivation under declared convention | Verified mathematically |
| Translation signs | Correct for camera-center velocity convention | Verified conditionally |
| Rotation terms | Correct for stated camera-frame angular velocity convention | Verified conditionally |
| Numerical example | Recalculates to 240 px, 1200 px, approximately 77.32°, −6/−4 px, and +0.6/+0.4 px | Verified mathematically |
| Tilt/reference triangle wording | Original angle qualification required correction | Corrected in draft |
| A–B → C sequence | Plausible staged heuristic; no optimality proof | Needs experiment |
| `zT` as primary C adjustment | Workflow-specific observation only | Needs experiment |
| Full-rank local alignment | Configuration-dependent | Needs rank/conditioning analysis |
| Whole-image agreement | Not implied by three-point agreement | Requires experiment |

No canonical TPS document, application code, or approved Working Focal Length equation was modified.
