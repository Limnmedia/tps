# Validation

Mathematical verification and physical camera experiments are distinct forms of validation and are documented separately.

## Test-01 — TPS Overlay Recovery

**Date:** 2026-10-13
**Status:** Operational validation recorded
**Test data:** [`tps-testing/test-01`](../tps-testing/test-01)

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

The package checksums validate successfully. The annotated reference plate is
available at [`annotated_reference_plate.png`](../tps-testing/test-01/a-side/take-02/tps_001_02_X1_0001.tps/graphics/annotated_reference_plate.png).

### Observation

The A-side reference and the B-side aligned image show close practical
correspondence at the three TPS markers and across the main scene objects:
the central ball and pedestal, left cup, rear triangle, right cylinder, and
foreground cones. The remaining visible differences are primarily lighting,
shadow, exposure, and surface texture.

This supports the conclusion that the TPS overlay successfully guided the
physical B-side camera line-up for this test.

### Scope and limitation

TPS does not prescribe a universal numerical acceptance tolerance. This record
therefore documents practical overlay recovery, not a calibrated residual
error. A future recovery record may optionally preserve observed marker
coordinates or operator notes, but those are not required to establish the TPS
reference itself.
