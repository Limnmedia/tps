# Derivation 1 — Physical and Image Triangles

**Status:** Research derivation. This document does not add a normative TPS requirement or claim experimental validation.

## Purpose

This derivation explains why a triangle formed by three physical points need not have the same side-length ratios or internal angles as its perspective image.

## Assumptions

1. Three physical points are distinct and non-collinear.
2. The camera is modeled as an ideal pinhole perspective camera.
3. Camera coordinates are used, with the camera center as the origin and the viewing direction as the positive (Z) axis.
4. The image plane is represented by coordinates ((x,y)), and focal length (f) is positive.
5. All points have positive depth: (Z_i > 0).
6. Lens distortion, sensor imperfections, cropping, and image resampling are excluded from this derivation.

## Perspective Projection

Let a physical point be

\[
P_i=(X_i,Y_i,Z_i).
\]

Under the ideal perspective model, its image point is

\[
 p_i=(x_i,y_i)=\left(f\frac{X_i}{Z_i},f\frac{Y_i}{Z_i}\right).
\]

This is the established 3D-to-2D perspective relationship described in MIT *Foundations of Computer Vision*, §5.3.1, and in Hartley and Zisserman, *Multiple View Geometry in Computer Vision*.

For three points (A), (B), and (C), applying the same mapping gives image points (a), (b), and (c). Correspondence is preserved by labeling: (A\to a), (B\to b), and (C\to c).

## Why Side-Length Ratios Are Not Generally Preserved

The physical distance between (P_i) and (P_j) is

\[
 d_{ij}=\sqrt{(X_i-X_j)^2+(Y_i-Y_j)^2+(Z_i-Z_j)^2}.
\]

The image distance is

\[
 \delta_{ij}=\sqrt{(x_i-x_j)^2+(y_i-y_j)^2}.
\]

Substitution gives

\[
 \delta_{ij}=f\sqrt{\left(\frac{X_i}{Z_i}-\frac{X_j}{Z_j}\right)^2+\left(\frac{Y_i}{Z_i}-\frac{Y_j}{Z_j}\right)^2}.
\]

The depth denominators differ when the points have different depths. Therefore, there is generally no single scale factor (s) such that (delta_{ij}=s d_{ij}) for all three sides. Without one common scale factor, side-length ratios are not generally preserved.

## Numerical Example

Use (f=1) and the physical points

\[
 A=(0,0,4),\quad B=(2,0,4),\quad C=(1,2,8).
\]

The image points are

\[
 a=(0,0),\quad b=(0.5,0),\quad c=(0.125,0.25).
\]

Physical side lengths:

\[
 AB=2,\quad AC=\sqrt{21}\approx4.583,\quad BC=\sqrt{21}\approx4.583.
\]

Image side lengths:

\[
 ab=0.5,
\]

\[
 ac=\sqrt{0.125^2+0.25^2}\approx0.280,
\]

\[
 bc=\sqrt{0.375^2+0.25^2}=\sqrt{0.203125}\approx0.451.
\]

The physical ratio (AB/AC\approx0.436), while the image ratio (ab/ac\approx1.789). The ratios differ, so the triangles are not similar in this example.

## Why Internal Angles Are Not Generally Preserved

An angle can be checked with dot products. At physical point (A), the vectors are

\[
 \overrightarrow{AB}=(2,0,0),\quad \overrightarrow{AC}=(1,2,4).
\]

Thus

\[
 \cos(\angle BAC)=\frac{\overrightarrow{AB}\cdot\overrightarrow{AC}}{|AB||AC|}=\frac{2}{2\sqrt{21}}=\frac{1}{\sqrt{21}},
\]

so (angle BAC\approx77.4^\circ).

In the image, the vectors at (a) are

\[
 \overrightarrow{ab}=(0.5,0),\quad \overrightarrow{ac}=(0.125,0.25).
\]

Therefore

\[
 \cos(\angle bac)=\frac{0.5\cdot0.125}{0.5\sqrt{0.125^2+0.25^2}}\approx0.447,
\]

so (angle bac\approx63.4^\circ). The angle changes under projection.

## Conditions That Can Preserve Similarity

Similarity may be preserved in special cases, including:

- The three physical points lie in a plane parallel to the image plane, so their camera-space depths are equal. The perspective mapping on that plane is then a uniform scale and translation in image coordinates.
- An orthographic or effectively orthographic camera model is appropriate. Orthographic projection applies a common scale under the stated model.
- A particular configuration happens to preserve a selected ratio or angle. This does not imply that all ratios and angles are preserved.

These are geometric conditions, not universal TPS requirements.

## Degenerate Projected Configurations

Three non-collinear physical points can project to a degenerate image configuration.

If two points lie on the same ray from the camera center, they have proportional camera-space coordinates and project to the same image point. For example, with (f=1), (A=(1,0,1)) and (B=(2,0,2)) both project to ((1,0)). A third point (C=(1,0,2)) is not on the physical line through (A) and (B), but projects to ((0.5,0)). The image points are coincident or collinear even though the physical points are non-collinear.

More generally, if the physical points lie in a plane passing through the camera center, their viewing rays lie in one plane and their image points can be collinear. Such a three-point projection exists, but it may not contain enough information for a particular TPS operation.

## Established Mathematics Versus TPS Interpretation

The perspective mapping, distance calculations, dot-product angle test, and special-case similarity statements are established geometry under the assumptions above.

The interpretation that a TPS reference should not assume similarity between a physical triangle and its image is consistent with this derivation. Whether a particular projected configuration is a valid TPS reference remains an operation-specific TPS question and is not resolved here.

## Supporting Sources

- MIT, *Foundations of Computer Vision*, §5.3.1, “Image Formation by Perspective Projection”: https://visionbook.mit.edu/imaging.html
- Richard Hartley and Andrew Zisserman, *Multiple View Geometry in Computer Vision*: https://robots.ox.ac.uk/~vgg/hzbook/hzbook1.html
- OpenStax, *Contemporary Mathematics*, §10.3, “Triangles”: https://openstax.org/books/contemporary-mathematics/pages/10-3-triangles

No experimental validation is claimed.
