# TPS Validation Evidence

This directory holds evidence for the three physical TPS experiments. Test 01
now has a public evidence record documenting practical visual overlay recovery.
Tests 02 and 03 remain **Not Yet Performed**.

For each test, preserve:

- `original.png` — the original reference image.
- `recovered.png` — the image captured after the camera or physical setup was changed and the view was recovered.
- `comparison.png` - a side-by-side comparison of the original and recovered images.
- `measurements.md` — setup measurements and operator observations.

Image comparison is the primary practical evidence. Measurements and
observations are supporting evidence. The take-02 artifact is a side-by-side
grayscale comparison, not a calibrated registration. Test 01 demonstrates visual recovery;
quantitative TPS accuracy has not been established. Do not add arbitrary
acceptance thresholds or generalize this result to the other tests.

[![Test-01 take-02 comparison](../tps-testing/test-01/a-side/take-02/comparison/comparison.png)](test-01-camera-recovery/README.md)

Test-01 demonstrates recovery of a recorded camera view after camera
repositioning. [Open the complete Test-01 record](test-01-camera-recovery/README.md)
or inspect the [full-resolution comparison](../tps-testing/test-01/a-side/take-02/comparison/comparison.png).

## Tests

- [Test 1 — Camera Recovery](test-01-camera-recovery/README.md)
- [Test 2 — View Transfer](test-02-view-transfer/README.md)
- [Test 3 — Scale Variation](test-03-scale-variation/README.md)
