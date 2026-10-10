# Derivation 2 — Image Registration

**Status:** Research derivation. This document does not add a normative TPS requirement or claim experimental validation.

## Purpose

This derivation describes how two recorded three-point projections can be expressed in a common image coordinate frame before their corresponding image locations are compared.

Registration makes coordinate descriptions comparable. It must not alter one projection in order to force nonmatching points to agree.

## Assumptions

1. Point correspondence is already known: (A\to a), (B\to b), and (C\to c).
2. Each recorded image has a declared coordinate frame and dimensions.
3. Any transformation used for registration is known, externally established, or independently justified.
4. The registration transformation is applied consistently to all three points in a record.
5. No transformation is selected solely because it makes three nonmatching projections coincide.
6. Tolerance and acceptance criteria are not assigned numerical values here.

## Pixel Coordinates

Let an image have width (W) and height (H), with a pixel-coordinate point (p=(u,v)). The coordinate convention must be stated, including origin, axis directions, and whether coordinates refer to pixel centers or boundaries.

For a simple full-frame convention, normalized coordinates are

\[
 n_x=\frac{u}{W},\qquad n_y=\frac{v}{H}.
\]

Other conventions are possible. The important requirement is that the convention is declared and used consistently.

## Resolution Changes

Suppose image 1 is (1920\times1080) and image 2 is (3840\times2160). Under full-frame scaling, a point at ((480,270)) in image 1 maps to ((960,540)) in image 2.

The normalized values are

\[
 (480/1920,270/1080)=(0.25,0.25),
\]

and

\[
 (960/3840,540/2160)=(0.25,0.25).
\]

Under this declared full-frame convention, the two coordinate descriptions refer to the same normalized location. This says nothing about whether the cameras, lenses, or physical scenes are otherwise equivalent.

## Cropping

If an image is cropped, the crop origin and scale must be recorded. For a crop whose upper-left point in the source frame is ((u_0,v_0)), a source point ((u,v)) has crop-frame coordinates

\[
 (u',v')=(u-u_0,v-v_0),
\]

before any additional resize or rotation. Without the crop parameters, a point's coordinates cannot be interpreted in the crop frame as a known transformation of the source frame.

## Rotation and Mirroring

Rotation changes the coordinate axes and origin relationship. A registered rotation must specify the center, angle, and resulting frame. Mirroring reverses one coordinate direction and must be explicitly declared. These operations may be represented by a coordinate transformation, but no particular transformation convention is prescribed here.

For a general two-dimensional affine registration, points may be represented in homogeneous coordinates and transformed as

\[
 \begin{pmatrix}u'\\v'\\1\end{pmatrix}
 =
 T
 \begin{pmatrix}u\\v\\1\end{pmatrix},
\]

where (T) is a declared transformation matrix. The matrix is a record of how frames correspond; it is not a permission to choose an arbitrary matrix after inspecting the mismatch.

## Comparing Three-Point Projections

Let (a_i,b_i,c_i) be the three points from record (i), and let (T_i) map record (i) into a common frame. The registered points are

\[
 \tilde a_i=T_i(a_i),\quad \tilde b_i=T_i(b_i),\quad \tilde c_i=T_i(c_i).

\]

An exact comparison checks equality of each corresponding pair in the common frame:

\[
 \tilde a_1=\tilde a_2,\quad \tilde b_1=\tilde b_2,\quad \tilde c_1=\tilde c_2.
\]

Practical matching may compare differences against an established tolerance, but this document does not define a numerical tolerance or an aggregate error rule.

## Registration Is Not Geometric Correction

Registration accounts for known differences between coordinate descriptions, such as resolution, crop origin, axis direction, or a declared frame rotation.

It must not be used to fit an arbitrary transformation to three nonmatching points. Such a fit can make any three non-collinear points agree by construction and would erase the very projection difference TPS is intended to compare.

Therefore:

- A registration transformation must be justified independently of the point mismatch being tested.
- The same declared transformation must be applied consistently to all corresponding points.
- A transformation that changes the geometric relationship under investigation is not neutral registration.
- A successful registered comparison does not establish a unique camera configuration.

## Numerical Example With a Crop

Let a source image contain point (a=(480,270)). A crop begins at ((100,50)), with no resize or rotation. The crop-frame coordinate is

\[
 a'=(480-100,270-50)=(380,220).
\]

If a second record reports ((380,220)) in that crop frame and the crop registration is documented, the two coordinates can be compared in the crop frame. This does not demonstrate that the image views or cameras are otherwise identical.

## Established Mathematics Versus TPS Interpretation

Coordinate normalization, affine coordinate transformations, and equality testing are established mathematical operations.

The requirement that registration not be chosen to force a TPS match is a TPS research interpretation intended to preserve the meaning of comparison. Its practical effectiveness and failure modes require experiments.

## Supporting Sources

- MIT, *Foundations of Computer Vision*, §5.3.1, “Image Formation by Perspective Projection,” including the relation between camera and image coordinate systems: https://visionbook.mit.edu/imaging.html
- Lisa Gottesfeld Brown, “A Survey of Image Registration Techniques,” *ACM Computing Surveys* 24(4), 1992, DOI: https://doi.org/10.1145/146370.146374. The full relevant article was not accessible during the current review.
- NIST Technical Note 1297, Appendix D1.1.2–D1.1.3, for repeatability and reproducibility terminology: https://www.nist.gov/pml/nist-technical-note-1297

No experimental validation is claimed.
