# Geometry

This document is a placeholder for geometric models and derivations.

The focal-length formulation is unresolved.

No equations are introduced at this stage.

## Geometry Principle 1 — Physical and Image Triangles

**Status:** Approved — Working Draft 0.1

**Classification:** Geometric principle.

### Plain-Language Statement

The triangle in the picture doesn't have to look like the triangle in the real world.

### Precise Statement

Under perspective projection, the image of three non-collinear physical points does not generally preserve the side-length ratios or internal angles of the physical triangle.

### Explanation

Three non-collinear physical points A, B, and C define a triangle in three-dimensional space.

When observed through a perspective camera, these points project to image points a, b, and c.

The resulting image triangle depends on the relationship between:

- The physical locations of A, B, and C.
- The camera's position.
- The camera's orientation.
- The camera's intrinsic parameters.

Perspective projection does not generally preserve physical distances, side-length ratios, or internal angles.

Consequently, the physical triangle and its image triangle need not be geometrically similar.

### Example

A physical triangle may have a horizontal A–B side.

Depending on the camera's position and orientation, its projected a–b side may appear tilted in the image.

This illustrates that physical orientation and image orientation are not necessarily the same.

### Important Distinctions

- Physical points A, B, C exist in 3D space.
- Image points a, b, c exist in a 2D image coordinate system.
- Correspondence preserves point identity, not physical distances or angles.
- Perspective projection can change the apparent shape of a triangle.
- Particular camera configurations may preserve some geometric relationships.
- The principle does not imply that every projection must distort the triangle.
- A non-collinear physical triangle may produce a degenerate image triangle under certain viewing configurations.

### TPS Implication

A TPS projection match compares corresponding image-point locations against a recorded reference.

It must not assume that the physical triangle and the image triangle are geometrically similar.

The geometric conditions needed to reproduce a reference projection remain subjects for subsequent derivation and validation.

## Geometry Principle 2 — Perspective and Depth

**Status:** Approved — Working Draft 0.1

**Classification:** Geometric principle.

### Plain-Language Statement

Things farther from the camera usually look smaller in the picture.

### Precise Statement

Under an ideal perspective camera model, the projected position of a physical point depends on its position relative to the camera, including its depth along the camera's viewing direction.

### Explanation

Under ideal perspective projection, a physical point's image location depends on:

- Its position relative to the camera.
- Its depth along the camera's viewing direction.
- The camera's intrinsic parameters.

Depth influences the apparent separation of physical points in the image.

For example, two points separated by 100 mm and positioned at the same depth may appear farther apart in an image when they are closer to the camera than when they are farther away.

This comparison assumes:

- The physical separation remains unchanged.
- The points' orientation relative to the camera remains unchanged.
- The camera's intrinsic parameters remain fixed.
- The points remain visible.

### Important Distinctions

1. **Depth alone does not determine an image point's location.**

   The point's position relative to the camera's optical axis also matters.

2. **A change in depth does not necessarily change image coordinates.**

   Under ideal perspective projection, moving a point along the same ray from the camera's projection center preserves its projected image location.

3. **The principle describes an ideal perspective camera model.**

   Real camera systems may introduce lens distortion and other deviations that require separate treatment.

4. **The principle does not establish that TPS can uniquely recover camera position, orientation, or focal length.**

### TPS Implication

The projected locations of A, B, and C depend on the spatial relationship between the physical triangle and the camera.

Reproducing a TPS reference therefore involves the relationship between physical geometry, camera geometry, and image coordinates.

Matching three projected points does not necessarily establish a unique camera pose or reproduce the entire scene.

### Scope

This principle does not establish:

- A camera calibration procedure.
- A required TPS triangle size.
- A required TPS triangle orientation.
- A required camera-to-triangle distance.
- A universal camera model for TPS.
- A unique inverse projection.
- A focal-length calculation.
