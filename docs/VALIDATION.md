# Validation

This document defines the preparation protocol for three physical TPS experiments. Mathematical verification and physical camera experiments remain distinct. The experiments are **Not Yet Performed**; this document records the procedure and evidence structure only.

Registered comparison between the original and recovered images is the primary practical evidence. Measurements and operator observations are supporting evidence. No universal numerical acceptance threshold is defined.

Evidence is collected in:

- [Test 1 — Camera Recovery](../validation/test-01-camera-recovery/README.md)
- [Test 2 — View Transfer](../validation/test-02-view-transfer/README.md)
- [Test 3 — Scale Variation](../validation/test-03-scale-variation/README.md)

## Common sequence

1. Establish the original camera view.
2. Record the TPS reference and measurements.
3. Change the camera or physical setup according to the test.
4. Recover the view using TPS.
5. Capture the recovered image.
6. Compare the original and recovered images in a registered frame.
7. Record observations and supporting measurements.

Use one Base Pair, A–B, and the third reference point, C. Preserve the original reference. Use the existing TPS definitions and calculation conventions without introducing new requirements.

## Test 1 — Camera Recovery

**Status: Not Yet Performed**

Record a camera view and TPS reference on one physical setup. Move or remove the camera while leaving the reference setup in place. Use the recorded reference to recover the view on the same physical setup.

Evidence: `original.png`, `recovered.png`, `comparison.png`, and the completed `measurements.md` in [test-01-camera-recovery](../validation/test-01-camera-recovery/).

## Test 2 — View Transfer

**Status: Not Yet Performed**

Record a TPS reference on one physical setup. Reproduce the reference on a second physical setup, identify the corresponding A, B, and C points, and record the actual relationships on the second setup. Use the original recorded image correspondences to guide recovery on the second setup.

The original reference remains unchanged. Differences between the setups are documented rather than silently treated as equivalent. An identical physical triangle is not assumed unless a specific operation requires it.

Evidence: `original.png`, `recovered.png`, `comparison.png`, and the completed `measurements.md` in [test-02-view-transfer](../validation/test-02-view-transfer/).

## Test 3 — Scale Variation

**Status: Not Yet Performed**

Repeat the view-transfer procedure with one declared change in physical scale or capture geometry. Identify exactly what changed and record the original-reference and second-setup measurements separately.

Physical scale changes and image-gate changes are distinct conditions. Do not assume they are mathematically equivalent. Record the relevant physical dimensions, active sensor or gate information, crop/resampling information, and image-frame interpretation.

Evidence: `original.png`, `recovered.png`, `comparison.png`, and the completed `measurements.md` in [test-03-scale-variation](../validation/test-03-scale-variation/).

## Evidence interpretation

The original and recovered images, viewed in registered comparison, are the primary practical evidence. Measurements constrain the initial setup and document changed conditions. Operator observations record what was adjusted, what remained different, and how the comparison was judged. No result should be described as experimental validation until the test is performed and its evidence is preserved.
