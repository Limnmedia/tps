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
