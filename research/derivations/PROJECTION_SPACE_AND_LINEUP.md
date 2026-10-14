# Projection Space and Lineup Geometry

**Status:** Research document — proposed analysis, not an approved specification change.

## 1. Executive Summary

TPS is best understood as an operator-guided camera-view registration method. Its essential comparison is between a saved three-point projection and a live three-point projection. The operator adjusts the physical camera toward the closest practical image-space match. TPS does not require solving for, or uniquely recovering, the camera's absolute pose.

The proposed lineup reasoning combines established perspective projection with production procedure. A physical triangle supplies identifiable points and measured relationships. A recorded projection supplies corresponding image observations. Working Focal Length and TPS Reference Distance can establish useful initial conditions, but their practical interpretation is subject to the assumptions in the existing Working Focal Length derivation. Visual registration then evaluates the combined effect of mechanics, optics, measurement error, and coordinate-frame registration.

Several parts of the proposed reasoning are not yet definitions in the specification. In particular, the meaning of tilt, the use of a shared UP direction, the tilt/reference-distance construction, the term `zT`, and the exact adjustment sequence require clarification or experiment. The present document preserves those distinctions rather than promoting them to universal TPS requirements.

## 2. Physical and Virtual Coordinate Systems

Physical motion-control equipment and a computer-generated camera may use independent coordinate systems. A physical system can define an origin through mechanical home positions, axis zeros, calibration, or set-specific conventions. A CG scene can define a separate world origin, camera frame, and axis convention. There is no general basis for identifying the physical origin `(0,0,0)` with the virtual origin `(0,0,0)`.

This does not prevent a direction from being compared between systems. Gravity can provide a physical vertical direction, while a CG scene can define a virtual vertical axis. A shared direction is weaker than a shared coordinate frame: it does not establish a common origin, scale, or position.

This distinction is consistent with the existing TPS constraint that a reference records image-space correspondence and does not require physical and virtual coordinate systems to share an origin. It is not currently an approved TPS requirement that a virtual system be used at all.

## 3. Shared UP Direction and Tilt

The proposed workflow uses a shared vertical direction to establish an inclination parameter before other lineup adjustments. The operator measures tilt with an inclinometer placed square to the camera and attempts to measure the camera inclination as accurately as practical. This describes the measurement procedure; it does not by itself define camera axes, Euler angles, or a sign convention.

If a physical camera's inclination is measured relative to gravity, the measurement can constrain one component of orientation relative to the chosen reference. It does not, by itself, establish complete orientation. Rotation about the vertical direction remains unresolved, and the result depends on whether the camera's optical axis, sensor axes, or rig axes define the measured angle. Camera roll also matters because a rolled image changes the relationship between image-horizontal and the physical A–B direction.

The procedure is intended to remain applicable when the camera has roll. Roll is also measured with an inclinometer placed square to the camera. “Square to the camera” is an operator measurement convention, not a complete mathematical specification of the instrument's sensing axes. Tilt and roll cannot be assumed independent of instrument orientation until the inclinometer placement, sensing plane, camera reference surfaces, and rotation convention are defined and examined.

Accordingly, “establish tilt first” should remain a proposed operating procedure. Before it can become normative, TPS must specify:

- The reference axis from which tilt is measured.
- Whether tilt is an angle from horizontal, vertical, or another rig axis.
- The positive direction and sign convention.
- The relationship between camera optical axis, sensor axes, and rig axes.
- How roll is measured and corrected.
- Whether the camera is assumed to be levelled with respect to gravity.
- How an inclinometer placed square to the camera is registered to the relevant camera reference axes.

The shared-UP argument supports a possible alignment aid. It does not establish a complete 3D orientation or a common coordinate system.

## 4. Tilt/Reference-Distance Triangle

The proposed construction places the UP direction, an inclined reference line, and a horizontal component in one vertical plane. If the line length is `D` and the angle `θ` is measured from horizontal, an ideal right-triangle construction gives:

```text
vertical component   = D sin(θ)
horizontal component = D cos(θ)
```

If `θ` is measured from vertical, the sine and cosine roles change. These relationships are elementary trigonometry, but their application to TPS depends entirely on what physical line `D` measures.

The clarified operating convention measures TPS Reference Distance `D` physically from a sensor-plane mark on the camera to the estimated midpoint between the physical base pair A and B. The operator makes this measurement as accurately as practical. This does not redefine `D` as an optical-center distance, perpendicular depth, or automatically as a camera-forward-axis distance. It remains the practical sensor-plane-to-reference-location measurement used by the existing TPS definition.

The midpoint measurement must also be related to the existing phrase “designated physical reference plane.” If the estimated A–B midpoint lies on that designated plane, the clarification supplies a concrete reference location on the plane. If it does not, the relationship between the point measurement and the plane convention remains unresolved.

Therefore the proposed triangle can use `D` as its hypotenuse only under additional assumptions. At minimum, the measured sensor-plane-mark-to-A–B-midpoint segment must be the inclined reference line represented by the triangle; the inclinometer angle must be measured relative to the same horizontal direction used by the triangle; the relevant motion and UP direction must lie in one vertical plane; and the sensor-plane mark and A–B midpoint must be the endpoints of that line. If `D` is merely a general distance between a sensor-plane mark and a midpoint on a differently oriented plane, the right-triangle components do not follow automatically.

Possible interpretations include:

1. `D` is redefined as a distance along a specified viewing line. This would conflict with the current canonical definition and must not be done implicitly.
2. The existing sensor-plane-to-reference-plane measurement is retained, and a separate projected or slanted distance is derived. The derivation would require the sensor/reference-plane orientation and the relevant reference point.
3. The triangle is explicitly labelled an approximate construction using `D` as a practical surrogate. Its error would then require analysis and experiment.

The current research conclusion is that the existing `D` convention must be preserved. The clarified midpoint measurement makes the intended endpoints more precise, but it does not by itself establish that the measured segment is the hypotenuse of the proposed right triangle. The triangle remains a conditional research construction, not a canonical TPS construction.

## 5. Three-Point Projection Mapping

Let A, B, and C be identified physical points. Let a, b, and c be their corresponding image points. For a fixed camera model, the projection can be represented abstractly as:

```text
P(q; A, B, C) = [u_A, v_A, u_B, v_B, u_C, v_C]
```

where `q` denotes camera configuration and imaging parameters held fixed or varied by the operation. The saved and live observations are:

```text
P_saved = P(q_saved; A, B, C)
P_live  = P(q_live; A, B, C)
```

The lineup objective is comparison in a common registered image frame:

```text
P_live ≈ P_saved
```

The correspondence is explicit and must remain unchanged:

```text
A → a
B → b
C → c
```

This is consistent with the approved definitions of physical point, image point, correspondence, three-point projection, TPS reference, and projection match. The physical triangle and image triangle remain distinct geometric objects. Matching the image locations does not assert that their side lengths or angles are equal, nor that the underlying camera configuration is unique.

## 6. Six Image Observations and Local Camera Alignment

A camera configuration may be represented locally as:

```text
q = (x, y, z, pan, tilt, roll)
```

This six-parameter representation is a useful local model for a rigid camera with three translations and three rotations. For motion-control notation, `T` denotes translation and `R` denotes rotation:

```text
xT = X-axis translation    yT = Y-axis translation    zT = Z-axis translation
xR = X-axis rotation       yR = Y-axis rotation       zR = Z-axis rotation
```

The X, Y, and Z axes are not assumed to be world-aligned. Their meaning depends on the coordinate frame established by the relevant rig or operation. This notation is not currently a complete TPS definition, and it does not establish a relationship between physical and virtual origins.

Three image points provide six scalar image observations:

```text
P(q) = [u_A, v_A, u_B, v_B, u_C, v_C]
```

For a sufficiently smooth projection model, a local first-order approximation is:

```text
ΔP ≈ J(q) Δq
```

where `J(q)` is the 6-by-6 Jacobian of image observations with respect to the selected six camera variables. If `J` has full local rank at a configuration, small changes in the six variables can, in principle, produce locally independent changes in the six observations. If the rank is deficient or the matrix is poorly conditioned, some motions cannot be distinguished reliably from the three-point image data.

This does not mean that six observations automatically provide six independent constraints. Rank depends on point geometry, camera configuration, intrinsic parameters, coordinate conventions, and which variables are actually free. Degenerate or near-degenerate configurations can reduce rank or make the inverse adjustment highly sensitive to error.

The local Jacobian statement is different from camera solving. It explains why an operator may receive useful feedback while adjusting a suitable rig near an existing setup. It does not provide a global uniqueness theorem, a P3P solver, or a guarantee that a numerical adjustment exists. Multiple global configurations can produce the same three-point projection, as already recognized by TPS Projection Principle 3 and the existing paper.

A known approximate starting configuration can matter operationally. A local adjustment process may converge toward one nearby match even when other global matches exist. This is a hypothesis about a practical lineup workflow and requires experiment; it must not be described as global camera recovery.

## 7. Sequential Lineup Procedure

The following is a proposed operator sequence, not an approved universal requirement:

1. Identify the three physical reference points A, B, and C.
2. Load the recorded TPS reference.
3. If a shared vertical convention is available and defined, establish the recorded inclination parameter.
4. Lock that parameter if the selected procedure requires it.
5. Establish the recorded Working Focal Length as closely as the equipment permits.
6. Establish the recorded TPS Reference Distance using its documented sensor-plane convention.
7. Use any justified tilt/distance geometry only as an approximate initial condition.
8. Compare the live and saved projections of A and B.
9. Adjust available rig controls to reduce the base-pair mismatch.
10. Examine the remaining discrepancy at C.
11. Adjust the relevant remaining camera movement while preserving the base-pair registration as closely as practical.
12. Iterate small adjustments while maintaining the declared constraints.
13. Accept the closest practical three-point projection match.

This sequence is measurement-anchored and operator-guided. It is not an unconstrained six-DOF numerical search. The exact effect of pan, height, horizontal position, depth, or other rig controls depends on the physical rig and its axis conventions. Measurements establish the initial configuration; saved/live projection comparison provides the final registration feedback. Small departures from nominal measured or calculated values may be accepted when they improve the visual registration. In this proposed sequence, tilt is intentionally held fixed during refinement, subject to the limitations and measurement conventions stated above.

## 8. Base-Pair Registration

The base pair A–B contributes four image-coordinate observations:

```text
a_live ≈ a_saved
b_live ≈ b_saved
```

Using A and B first can provide a practical visual reference for translation and orientation adjustments, but it does not prove that the base pair isolates particular degrees of freedom. Camera controls are coupled, and a movement intended to improve one coordinate can alter others.

The physical measurements establish initial geometry and provide a way to check or re-establish the recorded triangle measurements. The live projection provides feedback on the combined effects of mechanical tolerances, optical differences, coordinate-system differences, and measurement error. The operator need not identify each error source separately to reduce the observed image mismatch.

The proposed base-pair sequence should therefore be presented as a workflow heuristic. Its repeatability, convergence, and sensitivity to point placement require empirical testing.

## 9. Third-Point Registration

After A and B are approximately registered, C supplies two additional image observations:

```text
c_live ≈ c_saved
```

The third point can reveal residual differences not visible from the base pair alone. It does not automatically identify a unique remaining camera movement. Because projection variables are coupled, the operator may need to iterate across multiple controls.

In the described production workflow, the author identifies `zT` as the movement that predominantly addresses the remaining third-point discrepancy. Under the notation above, `zT` means Z-axis translation in the relevant motion-control coordinate frame. It must not be silently equated with world-Z translation, camera-local forward translation, or vertical height. This is a workflow-specific observation, not a universal mathematical guarantee; the dominant correction depends on the rig, axes, point geometry, and starting configuration.

## 10. Optical and Measurement-Error Considerations

The current Working Focal Length derivation uses:

```text
f_px = |xB - xA| * D / AB
AOV_h = 2 * atan(AB * W_image / (2 * D * |xB - xA|))
f_mm = f_px * W_sensor / W_image
```

The equations are dimensionally consistent under their stated ideal assumptions. Their application to a real camera is approximate. The existing derivation identifies unequal point depths, A–B misalignment, reference-plane tilt, sensor-plane distance, lens distortion, crop, resampling, and measurement uncertainty as limitations.

The proposed lineup should not treat the Working Focal Length as a guarantee of optical identity between systems. Lens breathing, principal-point differences, distortion, active sensor-area differences, focus changes, and mechanical error can alter the recorded image coordinates. Visual registration evaluates the combined result of the actual system; it does not eliminate or separately measure every optical difference.

The Working Focal Length and AOV are recorded reference quantities. If active sensor dimensions are unavailable, `f_px` and `AOV_h` remain usable while `f_mm` is omitted. The nominal focal length printed by a manufacturer and the TPS Working Focal Length should not be treated as interchangeable without further verification.

## 11. Geometric Limitations and Ambiguities

The following limitations remain consistent with the approved TPS material:

- Three image points do not guarantee unique camera pose.
- A projection match does not guarantee complete scene alignment.
- A non-collinear physical triangle can have a collinear or coincident image projection under some configurations.
- A shared UP direction does not determine a complete orientation.
- Six observations do not guarantee a full-rank Jacobian.
- Physical and virtual coordinate origins may remain unrelated.
- A sensor-plane-to-reference-plane distance is not automatically a line-of-sight distance.
- Physical triangle similarity is conditional and is not a universal TPS requirement.
- Exact image equality and practical visual agreement within an unspecified tolerance remain distinct.

These are limitations of interpretation and operation, not reasons to introduce camera-reconstruction requirements into TPS.

## 12. Relationship to Existing TPS Definitions

The proposed reasoning agrees with the current definitions in the following ways:

- A physical point is independent of the observing camera.
- An image point is a two-dimensional image-space location.
- Correspondence preserves identity A→a, B→b, and C→c.
- Projection maps physical points into image space.
- A three-point projection is ordered and may be degenerate.
- A TPS reference preserves correspondence, locations, coordinate-frame information, measurements, and derived reference quantities.
- A projection match compares corresponding image locations without asserting a unique camera configuration.

The reasoning adds proposed workflow concepts that are not currently defined: shared UP, tilt, locking tilt, the tilt/reference-distance triangle, base-pair registration order, third-point adjustment, and `zT`. These should remain research terms until reviewed and, where appropriate, defined separately.

## 13. Implications for Paper 1

Paper 1 can describe TPS as a portable, operator-guided view-registration method rather than a camera-pose reconstruction algorithm. The six-observation/Jacobian discussion may explain local feedback, provided it is labelled as a mathematical model and not as a claim of global identifiability or experimental performance.

The paper should distinguish the three triangles:

1. **Physical reference triangle:** A, B, and C with measured physical relationships.
2. **Projected image triangle:** a, b, and c in image space.
3. **Tilt/reference-distance triangle:** a proposed auxiliary construction whose validity depends on the definition of the measured distance and angle.

The third construction should not be presented as an established TPS mathematical foundation until the distance convention is resolved. Production experience may be reported as context for practical feasibility, but it does not establish numerical accuracy, repeatability, LAIKA endorsement, or originality of the complete method.

## 14. Open Questions Requiring Clarification

1. What exact rotation convention defines pan, tilt, and roll after the inclinometer measurements are made?
2. How is an inclinometer placed square to the camera registered to the camera's relevant axes?
3. Is tilt measured from horizontal, vertical, the optical axis, the sensor plane, or a rig axis?
4. How is camera roll measured and removed from the horizontal A–B calculation?
5. Does the proposed tilt/reference-distance construction use the canonical sensor-mark-to-A–B-midpoint `D` directly, or require a projected or separate slanted distance?
6. What physical plane contains the estimated A–B midpoint, and how is that related to the designated reference plane when the plane is tilted?
7. In which motion-control coordinate frame are `xT`, `yT`, `zT`, `xR`, `yR`, and `zR` expressed?
8. Under what point configurations does the local projection Jacobian have full rank?
9. How does the practical workflow behave when the Jacobian is ill-conditioned?
10. What starting-range assumptions are needed for the sequential procedure to be repeatable?
11. Which camera controls are available in the intended operating context?
12. How should point visibility, occlusion, and changing physical geometry be recorded during recovery?
13. What evidence will distinguish a useful local lineup heuristic from a general TPS requirement?

## 15. Proposed Specification Changes

No canonical specification changes are recommended at this stage. Before any change, the following research work should be completed:

- Define camera-axis and rotation conventions only if TPS needs them operationally.
- Resolve whether the tilt/reference-distance triangle is compatible with the canonical TPS Reference Distance.
- Define the motion-control frame for `zT` if the term is used in TPS-facing documents, while preserving its workflow-specific status.
- Analyze representative Jacobian ranks and degeneracies without converting the analysis into a camera-solving requirement.
- Run controlled experiments for lineup sequence, starting conditions, operator repeatability, and optical-system differences.
- Decide whether the sequential procedure belongs in a recommended-practices document rather than the core specification.

The current candidate specification can remain unchanged while these questions are investigated.

## Review Findings

### Conflicts with Existing TPS Documentation

- **Potential terminology conflict:** The proposed “tilt” parameter and shared-UP procedure are not defined by the current specification. The inclinometer procedure clarifies how the author measures it operationally, but it does not define a TPS rotation convention or make the procedure a requirement.
- **Reference Distance conflict risk:** The clarified convention measures `D` from a sensor-plane mark to the estimated A–B midpoint. This is compatible with the existing practical sensor-plane/reference definition only if the midpoint is the relevant location on the designated reference plane. Using `D` as the hypotenuse of a tilt triangle still requires the segment and angle to satisfy the same-plane right-triangle assumptions.
- **Motion-control notation:** `xT`, `yT`, `zT`, `xR`, `yR`, and `zR` are now documented as rig-frame notation in this research document. They must not be interpreted as world-aligned or virtual-camera axes without a declared coordinate frame.
- **Scope alignment:** The operator-guided matching objective agrees with the current Recovery and Matching Principle sections.
- **No conflict:** The six-observation model is compatible with the three image points, but it does not replace the specification's warnings about ambiguity and non-unique camera configurations.

### Mathematical Claims Requiring Correction or Qualification

- “Six observations provide six independent constraints” would be incorrect without a full-rank Jacobian assumption. The correct statement is conditional local observability.
- The right-triangle components `D sin(θ)` and `D cos(θ)` are valid only when `D` is the relevant inclined segment and `θ` is defined from the stated axis.
- A shared vertical direction constrains a direction, not a complete orientation or origin.
- The Working Focal Length equations remain dimensionally consistent under the existing ideal assumptions, but do not become exact real-camera identities through visual lineup.

### Undefined Coordinate Conventions

- Camera and rig axes for `x`, `y`, `z`, including the motion-control frame for `xT`, `yT`, `zT`, `xR`, `yR`, and `zR`.
- Positive directions and units for pan, tilt, and roll.
- Definition of tilt reference axis and inclinometer-to-camera registration.
- Image-frame convention after roll correction.
- Physical meaning and coordinate system of `zT`, including the evidence for its predominant effect on the third-point discrepancy.
- Exact line or plane represented by the TPS Reference Distance in the proposed triangle.

### Statements Requiring Empirical Evidence

- That establishing tilt first, using an inclinometer placed square to the camera, improves lineup efficiency or repeatability.
- That base-pair-first registration reliably reduces the remaining error at C.
- That a known approximate starting configuration produces useful local convergence.
- That the sequential procedure is repeatable across operators, rigs, cameras, or lenses.
- That the tilt/reference-distance construction, using sensor-mark-to-A–B-midpoint `D`, provides a practical initial position.
- That three-point matching provides adequate practical accuracy for intended productions.

## Classification Summary

| Material | Classification | Current status |
|---|---|---|
| Perspective projection and image correspondence | Established mathematical foundation | Supported by existing research; not experimental TPS validation |
| Six image observations and local Jacobian model | Conditional mathematical model | Research derivation; rank and conditioning require analysis |
| Projection ambiguity | Established limitation in relevant camera geometry | Consistent with current TPS principles |
| Shared UP direction | Production/geometric convention | Proposed; requires defined axes and validation |
| Tilt-first sequence | Operating hypothesis | Proposed; requires experiment |
| Tilt/reference-distance triangle | Conditional construction | Unresolved because canonical `D` is not automatically a slanted distance |
| Base-pair and third-point sequence | Operator workflow proposal | Proposed; requires experiment |
| `zT` | Workflow-specific motion-control notation | Defined here as rig-frame Z-axis translation; predominant effect remains an empirical observation |
| LAIKA-related experience | Production-derived context | Must not be presented as endorsement or validation |
