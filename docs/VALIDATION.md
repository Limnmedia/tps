# Validation

Mathematical verification and physical camera experiments are distinct forms of validation and are documented separately.

## Test-01 — TPS Overlay Recovery

**Date:** 2026-10-13
**Status:** Operational validation recorded
**Test data:** [`tps-testing/test-01`](../tps-testing/test-01)

Public evidence record: [Test-01 Camera Recovery](../validation/test-01-camera-recovery/README.md).
The take-02 comparison is [`comparison.png`](../tps-testing/test-01/a-side/take-02/comparison/comparison.png);
no take-01 comparison is substituted.

### Purpose

Verify that a TPS reference can be used as an image overlay to guide physical
camera line-up in Dragonframe.

This is an operational TPS recovery test. It is not a camera solve, lens
calibration, multi-view reconstruction, or calibrated geometric-residual
measurement.

### Procedure

1. Establish the A-side TPS reference from image 1:
   [`tps_001_02_X1_0001.jpg`](../tps-testing/test-01/a-side/take-02/tps_001_02_X1_0001.jpg).
2. Use the generated TPS package as the Dragonframe overlay layer:
   [`tps_001_02_X1_0001.tps`](../tps-testing/test-01/a-side/take-02/tps_001_02_X1_0001.tps).
3. Physically adjust the camera while comparing the overlay with image 2,
   [`tps_001_02_X1_0002.jpg`](../tps-testing/test-01/a-side/take-02/tps_001_02_X1_0002.jpg).
4. Inspect the correspondence of the three physical reference markers and
   their image projections in the B-side view.

### Reference

The package records the three-point TPS reference with:

- physical triangle sides: 74 / 87.5 / 79 mm;
- calculated working focal length: 39.680971 mm;
- reference distance: 304.4 mm;
- camera tilt / roll: 4.6° / 0.7°; and
- normalized reference raster: 6000 × 4000 px.

The local package checksums validated successfully before publication. The
annotated reference plate is
available at [`annotated_reference_plate.png`](../tps-testing/test-01/a-side/take-02/tps_001_02_X1_0001.tps/graphics/annotated_reference_plate.png).

The source captures are from a Canon EOS R100: A-side at 2026-10-13
11:58:47 PDT and B-side at 12:16:21 PDT. The images were captured by
Christopher Weinberg, who approved public redistribution. Raw CR3 files are
excluded from the public evidence set because they contain camera
serial-number metadata.

### Observation

The A-side reference and the B-side aligned image show close practical
correspondence at the three TPS markers and across the main scene objects:
the central ball and pedestal, left cup, rear triangle, right cylinder, and
foreground cones. The remaining visible differences are primarily lighting,
shadow, exposure, and surface texture.

This supports the conclusion that the TPS overlay successfully guided the
physical B-side camera line-up for this test.

### Provenance and redistribution

The images were captured by Christopher Weinberg. Public redistribution of the
images and associated validation materials is approved by the author,
Christopher Weinberg.

The public copies remove camera serial-number metadata; raw source files remain
outside the public evidence set.

### Scope and limitation

TPS does not prescribe a universal numerical acceptance tolerance. This record
therefore documents practical overlay recovery, not a calibrated residual
error. A future recovery record may optionally preserve observed marker
coordinates or operator notes, but those are not required to establish the TPS
reference itself.

## Planned follow-on experiments

Registered comparison between the original and recovered images is the primary
practical evidence. Measurements and operator observations are supporting
evidence. No universal numerical acceptance threshold is defined.

Evidence is collected in:

- [Test 1 — Camera Recovery](../validation/test-01-camera-recovery/README.md)
- [Test 2 — View Transfer](../validation/test-02-view-transfer/README.md)
- [Test 3 — Scale Variation](../validation/test-03-scale-variation/README.md)

### Common sequence

1. Establish the original camera view.
2. Record the TPS reference and measurements.
3. Change the camera or physical setup according to the test.
4. Recover the view using TPS.
5. Capture the recovered image.
6. Compare the original and recovered images in a registered frame.
7. Record observations and supporting measurements.

Use one Base Pair, A–B, and the third reference point, C. Preserve the
original reference. Use the existing TPS definitions and calculation
conventions without introducing new requirements.

### Test 1 — Camera Recovery

Record a camera view and TPS reference on one physical setup. Move or remove
the camera while leaving the reference setup in place. Use the recorded
reference to recover the view on the same physical setup.

Evidence: `original.png`, `recovered.png`, `comparison.png`, and the completed
`measurements.md` in [test-01-camera-recovery](../validation/test-01-camera-recovery/).

### Test 2 — View Transfer

Record a TPS reference on one physical setup. Reproduce the reference on a
second physical setup, identify the corresponding A, B, and C points, and
record the actual relationships on the second setup. Use the original
recorded image correspondences to guide recovery on the second setup.

The original reference remains unchanged. Differences between the setups are
documented rather than silently treated as equivalent. An identical physical
triangle is not assumed unless a specific operation requires it.

Evidence: `original.png`, `recovered.png`, `comparison.png`, and the completed
`measurements.md` in [test-02-view-transfer](../validation/test-02-view-transfer/).

### Test 3 — Scale Variation

Repeat the view-transfer procedure with one declared change in physical scale
or capture geometry. Identify exactly what changed and record the original-
reference and second-setup measurements separately.

Physical scale changes and image-gate changes are distinct conditions. Do not
assume they are mathematically equivalent. Record the relevant physical
dimensions, active sensor or gate information, crop/resampling information,
and image-frame interpretation.

Evidence: `original.png`, `recovered.png`, `comparison.png`, and the completed
`measurements.md` in [test-03-scale-variation](../validation/test-03-scale-variation/).

## Evidence interpretation

The original and recovered images, viewed in registered comparison, are the
primary practical evidence. Measurements constrain the initial setup and
document changed conditions. Operator observations record what was adjusted,
what remained different, and how the comparison was judged. No result should
be described as experimental validation until the test is performed and its
evidence is preserved.
