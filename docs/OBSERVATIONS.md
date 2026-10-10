# Observations

## Review Statuses

- **Proposed:** Under discussion.
- **Approved:** Reviewed and accepted for the working draft.
- **Validated:** Supported by mathematical proof or appropriate testing.

## Observation 1

**Plain-language statement:**

Three points can form a triangle.

**Precise statement:**

Three distinct points that do not lie on the same straight line form a triangle.

**Classification:** Established geometric fact.

**Status:** Approved — Working Draft 0.1

**Explanation:**

Three points define a triangle when they are distinct and non-collinear.

This is an established property of Euclidean geometry, not a new TPS discovery or experimental hypothesis.

## Observation 2

**Plain-language statement:**

A camera can see three points of a triangle.

**Precise statement:**

Three distinct, non-collinear physical points can be projected into a camera's image.

**Classification:** Established principle of camera projection geometry.

**Status:** Approved — Working Draft 0.1

**Explanation:**

A camera produces a two-dimensional image of the physical scene in front of it.

When the three physical points are within the camera's field of view and are not obscured, each can appear at a corresponding location in the image.

The physical triangle exists in three-dimensional space. Its image is a two-dimensional projection.

Observation 2 establishes that the three physical points can be represented in an image.

It does not establish:

- That their image positions uniquely determine the camera's position.
- That the projected triangle preserves the physical triangle's lengths or angles.
- That all camera configurations produce a usable three-point projection.

These questions belong to later observations, definitions, and geometric analysis.

## Observation 3

**Plain-language statement:**

The camera's image is two-dimensional.

**Precise statement:**

The camera represents visible physical points as locations in a two-dimensional image coordinate system.

**Classification:** Established principle of camera projection geometry.

**Status:** Approved — Working Draft 0.1

**Explanation:**

Physical points exist in three-dimensional space.

A camera projects visible physical points onto a two-dimensional image.

Each projected point has a location in that image.

The three physical points form a triangle in space. Their corresponding image points also form a triangle when the projected points are distinct and non-collinear.

The physical triangle and its image projection are related, but they are not geometrically identical.

Observation 3 establishes the dimensional relationship between physical space and image space.

It does not establish:

- That physical distances are preserved in the image.
- That physical angles are preserved in the image.
- That the image contains enough information to reconstruct the original three-dimensional geometry.
- That the three projected points must always form a nondegenerate triangle.

These questions belong to later geometric analysis.

## Observation 4

**Plain-language statement:**

Changing the camera's focal length can change where the three points appear in the image.

**Precise statement:**

Changing a camera's focal length, while holding its position and orientation fixed, can change the projected image coordinates of three stationary physical points.

**Classification:** Established principle of camera projection geometry.

**Status:** Approved — Working Draft 0.1

**Explanation:**

A camera's focal length affects how physical points are projected into its image.

When the camera remains stationary, changing the focal length can change the positions of the three projected points.

The physical triangle remains unchanged.

This establishes that camera parameters can affect the image projection independently of camera movement.

Observation 4 does not establish:

- A formula for calculating focal length.
- That focal length can be uniquely determined from three projected points.
- That changing focal length always changes every projected point's image coordinates.
- That changing focal length changes the physical triangle.
- That focal length and camera distance are interchangeable.

Focal length is distinct from:

- Physical sensor dimensions.
- Sensor cropping.
- Digital image scaling.
- Changes in image resolution.

These relationships will be examined in the geometric model and mathematical formulation.

## Observation 5

**Plain-language statement:**

Moving the camera can change where the three points appear in the image.

**Precise statement:**

Changing a camera's position or orientation, while holding the physical points and camera's intrinsic parameters fixed, can change the projected image coordinates of those points.

**Classification:** Established principle of camera projection geometry.

**Status:** Approved — Working Draft 0.1

**Explanation:**

Camera movement can change the relationship between physical points and their projected image positions.

Two types of camera movement are relevant:

1. **Translation:** Moving the camera from one position to another.
2. **Rotation:** Changing the direction the camera faces without changing its position.

Both can change the projected positions of the three physical points.

The physical triangle remains unchanged.

Observation 5 does not establish:

- That every camera movement changes the projection.
- That matching projections uniquely determine the camera's physical position.
- That camera translation and rotation produce equivalent geometric effects.
- That the physical triangle changes when the camera moves.
- That camera movement alone is sufficient to reproduce a particular projection.

These relationships belong to the later geometric model and mathematical formulation.

## Observation 6 — Reproducing the Projection

**Plain-language statement:**

When the same three points appear in the same places in the image, we've matched the three-point view.

**Precise statement:**

When three corresponding physical points project to the same three image coordinates as a recorded reference, the three-point projection has been reproduced.

**Classification:** Geometric correspondence principle.

**Status:** Approved — Working Draft 0.1

**Explanation:**

A camera projects three physical points into an image.

The positions of those projected points can be recorded and used as a reference.

A camera configuration reproduces the recorded three-point projection when the same three physical points appear at the same three image coordinates.

This correspondence can be established without requiring the camera's physical coordinate system to be aligned with another coordinate system.

The comparison takes place in image space.

Observation 6 does not establish:

- That matching projections uniquely determine the camera's physical position.
- That the camera's orientation is necessarily identical.
- That the focal lengths are identical.
- That the entire image has been reproduced.
- That matching three points guarantees all other physical objects will appear in the same locations.
- That three-point correspondence uniquely determines the complete camera configuration.

These questions belong to the geometric model, assumptions, constraints, and validation.
