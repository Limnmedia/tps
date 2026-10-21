# TPS Camera Recovery Procedure (TPS-CRP) v0.1

**Status:** Experimental — Not Yet Physically Validated
**Purpose:** Provisional operator-facing guide for recovering a recorded camera view with a TPS reference and Dragonframe overlay.
**Scope:** Practical view matching, not camera-pose reconstruction, lens calibration, or a unique six-degree-of-freedom solve.

This document is a proposed procedure for review. It does not amend or replace the TPS Specification, definitions, calculations, or stated limitations. The canonical TPS material remains in [`../SPECIFICATION.md`](../SPECIFICATION.md), [`DEFINITIONS.md`](DEFINITIONS.md), and [`USE_CASES.md`](USE_CASES.md).

## 1. Prerequisites

Prepare the following before beginning recovery:

- The recorded A-side reference image.
- Stable, identifiable physical reference points A, B, and C.
- The corresponding image points a, b, and c, with their identities preserved.
- The recorded TPS measurements and calculation inputs, including the A–B measurement and TPS Reference Distance where available.
- Recorded camera and lens information, including focal-length, focus, tilt, and roll information where available.
- A transparent reference overlay generated from the TPS package, or another registered representation of the reference.
- A live camera image in Dragonframe that can be compared with the reference.
- A consistent image frame, including orientation, crop, scale, and registration.

The original reference remains authoritative. Do not silently replace its image dimensions, point identities, coordinate frame, or measurements with values from the recovery setup.

## 2. Roles and authority

### TPS requirements

TPS preserves correspondence between physical points A/B/C and image points a/b/c. Recovery compares the recorded three-point projection with the corresponding points in a live view. The objective is the closest practical reproduction under the operating conditions. TPS does not require an identical camera, does not guarantee a unique camera configuration, and does not prescribe a universal numerical tolerance.

### Proposed operator guidance

The sequence below is a practical, measurement-anchored workflow. It is guidance for this experimental procedure, not a universal TPS requirement. Camera controls are coupled; an apparent improvement does not prove that a particular parameter was the original source of error.

### Dragonframe-specific instructions

Dragonframe is used here as the live-view and overlay comparison environment. Its menus, overlay controls, image scaling, and registration behavior may vary by version and setup. Confirm the exact control names on the installed system without treating Dragonframe behavior as part of the TPS specification.

## 3. Register the reference overlay in Dragonframe

1. Load the intended live camera feed in Dragonframe.
2. Load the transparent TPS reference overlay or reference plate into the overlay/reference-image function.
3. Match the overlay orientation, aspect ratio, crop, and displayed frame to the live camera image. Do not stretch the reference to conceal a mismatch in image dimensions or registration.
4. Align the overlay using stable image features or the declared frame-registration marks. Preserve the recorded correspondence A→a, B→b, and C→c.
5. Set overlay opacity or display mode so that both the live image and reference markers remain visible.
6. Confirm that the overlay is not being shifted by an undocumented crop, resize, mirror, rotation, or pixel-aspect conversion.

The overlay is a representation of the TPS reference, not the complete TPS reference. If registration cannot be established reliably, stop and record the ambiguity before adjusting the camera.

## 4. Experimental recovery sequence

Use the following eight-step order. Make small, observable changes and continue to inspect all three points after each adjustment.

### 1. Match tilt

Restore the recorded tilt as closely as practical using the documented measurement convention. Treat the value as an initial condition and recovery reference, not proof that the camera pose has been solved.

### 2. Match roll when available

Restore the recorded roll when it is available and measured under a known convention. If roll is unknown, ambiguous, or coupled to another adjustment, record that condition rather than inferring it from the triangle alone.

### 3. Match distance using A–B scale

Use the A–B Base Pair and its recorded image separation as a scale cue. Restore the TPS Reference Distance and related setup measurements as closely as practical. A scale difference may also result from focal length, focus breathing, crop, sensor/gate changes, or registration error; do not attribute it uniquely to distance.

### 4. Match horizontal position

Compare the live A/B pair with the registered reference and adjust the camera’s horizontal position in small increments. Observe the effect on both points. Rig pivots and axis conventions can make the visible result differ from the nominal control direction.

### 5. Match camera height

Adjust camera height to reduce the remaining vertical mismatch while continuing to monitor A, B, and the overall frame. Tilt and height can produce similar image effects, so do not treat one residual as a unique diagnosis.

### 6. Use C for pan and top-point completion

After A and B are usefully close, evaluate C and the complete projected triangle. Use C as the additional image observation for pan and remaining vertical or depth-related refinement. Continue to monitor A and B; improving C may disturb the Base Pair.

### 7. Fine-check A, B, and C

Iterate small adjustments while comparing all three corresponding projections in the registered frame. Check image orientation, scale, point identity, focus state, crop, and visible scene features outside the triangle. Record any remaining mismatch or uncertainty.

### 8. Operator approval

Accept the result only when the responsible operator judges it to be the closest practical match for the intended shot and records the conditions and observations. Operator approval is not a claim of exact image equality, a unique camera solution, or complete scene alignment.

## 5. Interpreting A/B and C

The A–B Base Pair supplies the initial scale and image-registration reference. It is useful for seeing separation, midpoint, orientation, and common displacement, but it does not isolate one camera control or determine a complete camera configuration.

C provides the third image observation. It helps expose discrepancies that A and B alone cannot reveal and can provide useful feedback about depth-related or coupled adjustments. C does not uniquely identify a remaining error or guarantee that one particular control is the correct correction.

The physical triangle and its image projection are distinct. Do not require them to be similar, and do not substitute image-triangle similarity for TPS correspondence.

## 6. Failure and ambiguity guidance

Stop or record an explicit exception when:

- A, B, or C cannot be identified consistently between the reference and live view.
- The overlay cannot be registered without an unexplained crop, scale, mirror, rotation, or aspect-ratio change.
- The reference image dimensions or coordinate frame are unknown or have been changed.
- A/B alignment improves while C becomes materially worse, or the reverse, without a documented adjustment rationale.
- A scale mismatch may be caused by focal length, focus breathing, active sensor area, crop, resampling, or lens distortion rather than distance alone.
- Tilt, roll, rig axes, or measurement endpoints use an unknown sign or orientation convention.
- The camera or physical reference has changed, moved, or deformed in a way that invalidates the recorded correspondence.
- A three-point match is achieved but other stable scene features do not agree.

Do not claim that a successful three-point match recovered the original camera position, orientation, lens model, or entire image. Record the remaining differences, setup changes, and operator judgment.

## 7. Evidence to preserve

For each experimental recovery, preserve:

- The original A-side reference image.
- The recovered B-side image.
- The TPS package and transparent overlay used.
- Camera, lens, capture mode, and captured image dimensions.
- A/B/C identities and a/b/c image correspondence.
- TPS measurements and calculation inputs used to establish the reference.
- Overlay registration and image-frame notes.
- The camera changes and adjustment order.
- Observations for A, B, C, and stable scene features outside the triangle.
- The operator’s acceptance or rejection and any unresolved ambiguity.

Registered comparison between the original and recovered images is the primary practical evidence. Measurements and operator observations are supporting evidence.

## 8. Validation status

TPS-CRP v0.1 has not yet been physically validated as a repeatable Dragonframe procedure. The existing TPS validation experiments remain separate and are marked **Not Yet Performed**. The recorded LIMNTPS Dragonframe overlay test demonstrates practical overlay use, but does not establish a universal tolerance, camera solve, or complete recovery guarantee.

This draft must remain experimental until the procedure is reviewed, performed under declared conditions, and its evidence is preserved. No research heuristic in this document should be treated as a new TPS specification requirement without explicit approval.

## References

- [TPS Specification](../SPECIFICATION.md)
- [TPS Definitions](DEFINITIONS.md)
- [TPS Use Case: Recovering a Camera View](USE_CASES.md)
- [TPS Validation](VALIDATION.md)
- [TPS Camera Lineup: Operational Method and Geometric Foundations](../research/methods/TPS_CAMERA_LINEUP_GEOMETRY.md)
- [TPS Physical Camera Lineup — Procedure Review](../research/methods/TPS_PHYSICAL_LINEUP_PROCEDURE_REVIEW.md)
- [TPS Physical Validation Protocol — Draft](../research/reviews/TPS_PHYSICAL_VALIDATION_PROTOCOL_DRAFT.md)
- LIMNTPS `CAMERA_INTERRUPTION_WORKFLOW.md`
- LIMNTPS `STAGE_LINE_UP_WORKFLOW.md`
- LIMNTPS `TPS_OVERLAY_RECOVERY_TEST_01.md`
