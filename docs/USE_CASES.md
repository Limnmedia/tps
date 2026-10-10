# UC-001: Recovering a Camera View

## Problem

A camera has been positioned to photograph a physical scene. The camera is subsequently moved, removed, or replaced.

The original view must be reproduced, potentially days, weeks, or months later.

Traditional approaches may depend on detailed camera measurements, motion-control equipment, or specialized camera-tracking workflows. These resources are not always available to independent animators, students, and small productions.

## Objective

Use TPS to record sufficient information about the original camera view so that it can be reproduced later.

## Preconditions

- Three distinct, non-collinear physical points can be identified as A, B, and C.
- The points can be viewed by a camera and are not obscured.
- The corresponding image points a, b, and c can be identified consistently.
- A TPS reference can establish a consistently registered image coordinate frame.
- The physical triangle geometry, focus distance, and Working Focal Length can be recorded as part of the TPS reference.

## Method

1. Identify three physical reference points A, B, and C.
2. Establish their corresponding image points a, b, and c.
3. Record their correspondence and image locations in a consistently defined image coordinate frame.
4. Preserve the physical triangle geometry.
5. Record focus distance, measured from the camera sensor plane to the designated reference plane.
6. Calculate Working Focal Length once when establishing the TPS reference, and preserve the calculated value and necessary calculation inputs.
7. During recovery, establish the corresponding physical reference points and adjust the camera view until the three image points match the recorded reference within the specified tolerance.

## Expected Outcome

The recorded three-point projection is reproduced within the specified tolerance.

The TPS reference also preserves camera-reference information for subsequent production or VFX work.

## Limitations

A three-point projection match does not necessarily establish that:

- The original camera position has been recovered.
- The original camera orientation has been recovered.
- The entire image matches exactly.
- A unique camera solution has been found.

TPS is a view-matching method, not a unique camera-reconstruction method.

## Proposed Validation

This use case provides a basis for experiments:

- Record a reference view.
- Move or remove the camera.
- Attempt to reproduce the reference.
- Measure image-point correspondence errors.
- Compare additional scene features to assess the practical limits of the match.

These are proposed experiments, not validated results.
