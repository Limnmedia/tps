# TPS Physical Validation Protocol — Draft

**Status:** Non-normative draft for review.  
**Purpose:** Test whether TPS helps one operator reproduce a recorded camera view under three increasingly different physical conditions.  
**Scope:** Physical camera recovery and view transfer. Mathematical verification remains separate.

## Governing structure

TPS uses one Base Pair: **A–B**. **C** is the third spatial reference point. No additional Base Pairs or alternative triangle configurations are introduced by this protocol.

The primary evidence for every test is visual registration between the original reference image and the recovered image. Measurements, image coordinates, and operator observations are supporting evidence. This protocol does not impose a universal numerical accuracy threshold and does not require camera-pose measurement.

Use the existing TPS definitions and equations without modification. Record the actual captured image dimensions, image coordinate frame, physical relationships among A, B, and C, TPS Reference Distance, and Working Focal Length inputs and values when applicable.

## Common procedure

For each test, use ordinary equipment available to one camera operator: a camera, lens, tripod or practical support, a ruler or tape measure, a suitable inclinometer when available, and a way to display or compare the original and live/recovered images.

1. Identify stable, distinguishable physical points A, B, and C. Existing scene features or deliberately placed markers may be used.
2. Record the original reference image, with A→a, B→b, and C→c identified in a declared image coordinate frame.
3. Record the physical relationships among A, B, and C and the applicable TPS Reference Distance and Working Focal Length calculation inputs.
4. Preserve the original image and all reference information before changing the setup.
5. Perform the test-specific change.
6. Present the original reference in registration with the live or recovered image.
7. Use TPS to align the camera view. A–B is the Base Pair used for initial alignment; C supplies the additional image observation. Adjust iteratively while observing all three points. No fixed camera-control sequence is required.
8. Record the recovered image and compare it with the original reference image.
9. Preserve observations about A/B/C, the image frame, visible scene features outside the triangle, and any setup differences.

The comparison should distinguish three-point agreement from agreement across the rest of the image. A match at A, B, and C is not evidence that the entire image, scene, or camera pose has been recovered.

## Test 1 — Same physical setup: camera recovery

### Objective

Test recovery after the camera has moved while the physical reference setup remains unchanged.

### Initial setup and TPS measurements

- Establish one physical scene containing A, B, and C.
- Record the original camera view and the correspondence A→a, B→b, and C→c.
- Measure and record the physical relationships among A, B, and C.
- Record the TPS Reference Distance, captured image dimensions, image coordinate frame, and Working Focal Length inputs and value when applicable.
- Preserve the original camera/lens and setup observations as context, without treating them as a solved camera pose.

### Change and lineup

- Move the camera, or remove and replace it in a changed position, while leaving the physical reference points in place.
- Present the original reference image in registration with the live view.
- Use TPS to recover the original view, beginning with A–B and then evaluating C while continuing to observe A and B.

### Evidence

- Original reference image.
- Recovered image from the same physical setup.
- Visual registration comparison of the two images.
- Supporting records: measured values, image-frame information, point observations, visible features outside A/B/C, camera changes, and operator notes.

## Test 2 — Different physical setup: view transfer

### Objective

Test whether a TPS reference established on one physical setup can guide reproduction of the recorded view on a second setup.

### Initial setup and TPS measurements

- Establish Setup 1 with A, B, and C and record the original reference image.
- Record A→a, B→b, and C→c, the physical relationships among the points, and the applicable TPS measurements and image-frame information.
- Reproduce the reference geometry on Setup 2. Document how the corresponding A, B, and C locations are identified and any differences between the setups.
- Do not assume that a different physical arrangement is equivalent merely because it has three points. Record the relationships needed to interpret the transfer.

### Change and lineup

- Use the Setup 1 reference image while working with Setup 2.
- Register the reference and live/recovered image frames according to the recorded image information and the declared transfer conditions.
- Use TPS to adjust the camera on Setup 2 toward the Setup 1 recorded view, using A–B as the Base Pair and C as the third observation.

### Evidence

- Original Setup 1 reference image.
- Recovered Setup 2 image.
- Visual registration comparison of the original and recovered images.
- Supporting records: Setup 1 and Setup 2 measurements, point identities, image-frame mapping, physical differences, visible features outside A/B/C, and operator observations.

The result tests view transfer under the declared physical correspondence. It does not establish that the two setups share a unique camera pose or that all scene geometry is equivalent.

## Test 3 — Scale variation: view transfer

### Objective

Repeat Test 2 while declaring one intentional scale-related change and documenting its effect on the transfer.

### Initial setup and TPS measurements

- Establish Setup 1 and record the TPS reference as in Test 2.
- Establish Setup 2 and identify the declared scale variable before lineup.
- Record all relevant physical measurements, captured image dimensions, active sensor information when known, image coordinate frames, and Working Focal Length inputs.

### Declare the scale variation

Choose and document one of the following, without treating them as equivalent:

- **Physical scale change:** the physical distances or scene geometry are enlarged or reduced by a declared factor or construction method. Record which physical relationships changed and which were intended to remain corresponding.
- **Image-gate change:** the camera’s active image gate, crop, resampling, image dimensions, or related capture framing changes. Record the active imaging area and the justified coordinate-frame mapping.

A physical scale change changes the scene geometry. An image-gate change changes how the camera capture is represented or framed. Their effects must be documented separately and must not be treated as mathematically interchangeable without an explicit model and evidence.

### Change and lineup

- Use the original reference image and the declared Setup 2 conditions.
- Register the image frames using the recorded coordinate and gate information.
- Use TPS to align the Setup 2 camera view, beginning with A–B and evaluating C without introducing another Base Pair or a camera-pose measurement.

### Evidence

- Original reference image.
- Recovered image under the declared scale variation.
- Visual registration comparison of the original and recovered images.
- Supporting records: the scale variable and its value or description, physical measurements, gate/crop/image dimensions, image-frame mapping, A/B/C observations, visible features outside the triangle, and operator notes.

The result is evidence about the declared transfer condition only. It does not establish equivalence between physical scaling and image-gate scaling, nor does it establish whole-image agreement beyond the observed comparison.

## Reporting template

For each test, preserve:

- Test name and date.
- Camera, lens, capture mode, and image dimensions.
- Original reference image.
- Recovered image.
- A/B/C identities and a/b/c image correspondence.
- Physical relationships among A, B, and C.
- TPS Reference Distance and Working Focal Length inputs/values when applicable.
- Declared image coordinate frame and any crop, gate, or scale mapping.
- Description of the camera movement or setup transfer.
- Visual registration observations, including features outside the triangle.
- Supporting measurements and operator notes.
- Any failure, ambiguity, or changed physical condition.

## Interpretation limits

These tests are intended to demonstrate practical view reproduction under stated conditions. They do not establish a unique camera pose, complete scene reconstruction, universal accuracy, or superiority over PnP, matchmoving, calibration, or other lineup methods. Repeatability and reproducibility require additional trials and operators after the basic tests are completed.
