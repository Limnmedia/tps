# Working Focal Length Derivation

**Status:** Research derivation. The proposed relationship is not an approved mathematical formulation or experimentally validated TPS result.

## Proposed Relationship

```text
f_TPS = (|xB - xA| / W_image) * W_sensor * (D / AB)
```

Definitions:

- `xA`, `xB`: horizontal image coordinates of A and B, in pixels.
- `W_image`: captured image width, in pixels.
- `W_sensor`: active physical sensor width, in millimeters.
- `D`: measured distance from the camera sensor-plane mark toward the estimated midpoint of Base Pair A–B, in millimeters. Focus distance is a separate camera/lens measurement.
- `AB`: measured physical distance between A and B, in millimeters.

## Derivation Under an Ideal Model

Assume a pinhole camera whose projection center and image plane are separated by focal length `f`. Let a physical point have camera coordinates `(X, Y, Z)`. Its ideal image-plane coordinates are

```text
x = f X / Z
y = f Y / Z
```

Assume A and B lie on a reference plane perpendicular to the viewing direction and at the same depth `Z = D`. Assume their physical segment is parallel to the image's horizontal axis, so `AB = |XB - XA|`. Then

```text
|xB - xA| = f |XB - XA| / D
                 = f AB / D
```

The image-plane separation in millimeters is not the pixel separation. Under a linear full-width sensor mapping,

```text
delta_sensor = (|xB_pixels - xA_pixels| / W_image) * W_sensor
```

Combining the two relationships gives

```text
delta_sensor = f AB / D
```

and therefore

```text
f = delta_sensor * D / AB
  = (|xB - xA| / W_image) * W_sensor * (D / AB)
```

Under these ideal assumptions, the proposed relationship is the pinhole focal length expressed in the same physical length units as `W_sensor`, `D`, and `AB`.

The derivation uses horizontal image separation, not the full two-dimensional distance between image points. It therefore requires the physical A–B segment to contribute its measured length to the camera-horizontal direction in the stated geometry.

## Dimensional Consistency

The pixel ratio `|xB - xA| / W_image` is dimensionless. `W_sensor` has units of millimeters, and `D / AB` is dimensionless. Therefore:

```text
units(f_TPS) = 1 * mm * (mm / mm) = mm
```

The proposed relationship is dimensionally consistent.

Dimensional consistency does not prove geometric validity. It only shows that the units are compatible.

## Numerical Verification Under the Ideal Assumptions

Use:

```text
W_image  = 4000 pixels
|xB-xA|  = 1000 pixels
W_sensor = 36 mm
D        = 2000 mm
AB       = 100 mm
```

Then

```text
delta_sensor = (1000 / 4000) * 36 mm = 9 mm
f_TPS        = 9 mm * (2000 mm / 100 mm)
             = 180 mm
```

Forward checking gives

```text
f_TPS * AB / D = 180 mm * 100 mm / 2000 mm = 9 mm
```

The recovered sensor separation equals the measured 9 mm under the ideal equal-depth model.

## Unequal Point Depths

If A and B do not have the same depth, the proposed relationship does not generally recover the focal length. For example, let

```text
A = (0, 0, 2000 mm)
B = (100, 0, 2100 mm)
f = 100 mm
```

The exact horizontal image-plane separation is

```text
|xB-xA| = 100 mm * 100 mm / 2100 mm = 4.7619 mm
```

If the formula uses `D = 2000 mm` for A and `AB = 100 mm`, it infers

```text
f_TPS = 4.7619 mm * (2000 mm / 100 mm) = 95.238 mm
```

The true model focal length is 100 mm. The discrepancy is caused by using one reference depth while B is at another depth. The error is not a measurement-unit issue.

## A–B Orientation

The formula uses horizontal image separation and the full physical distance `AB`. These are equal-scale quantities only under a suitable orientation assumption.

If A–B is not parallel to the camera-horizontal direction, only its camera-horizontal component contributes to `|xB-xA|`. If the segment is tilted in depth, its endpoints can also have unequal depths. In either case, substituting the full physical length `AB` into a horizontal-separation formula can produce a biased result.

A two-dimensional image distance between a and b would answer a different question. Replacing horizontal separation with the full image distance does not repair unequal depths or arbitrary orientation; it changes the proposed relationship and is not done here.

## Reference-Plane Tilt

If the designated reference plane is tilted relative to the image plane, points on the plane generally have different depths. Even if A–B is physically straight and measured accurately, the perspective scale can vary along the segment. The equal-depth derivation then does not apply.

A plane parallel to the image plane is a special case in which all points on that plane share the same camera depth under the ideal model. A tilted plane requires a more complete geometric treatment and cannot be silently substituted into this formula.

## Sensor Plane, Projection Center, and Focus Distance

The proposed `D` is measured from the camera sensor-plane mark toward the estimated midpoint of Base Pair A–B. In an ideal pinhole derivation, depth is measured from the projection center. In a real lens, the relevant optical reference is associated with principal planes or an effective projection center, not necessarily the physical sensor plane or the entrance pupil.

Therefore, using sensor-plane distance in the proposed relationship is an approximation unless the chosen optical model establishes that the sensor-plane measurement is the intended object distance for the calculation.

Focus distance is a separate camera/lens measurement and is not the TPS Reference Distance. For a finite-focus thin-lens model, the image distance is not generally identical to the focal length. A more complete model distinguishes object distance, image distance, and principal-plane locations. The current proposed relationship does not specify those quantities, so it should not be described as an exact real-lens formula.

The sensor-plane convention may nevertheless define a reproducible TPS quantity. That quantity is a TPS Working Focal Length, not automatically the manufacturer's nominal focal length or a laboratory-calibrated effective focal length.

## Working Focal Length Versus Nominal Focal Length

Manufacturer-stated focal length is a lens specification under the manufacturer's conventions and conditions. The TPS Working Focal Length is calculated from the recorded image separation, sensor width, measured physical separation, and recorded distance convention.

They may differ because of:

- Sensor-plane distance versus principal-plane or projection-center distance.
- Finite focus and focus breathing.
- Lens distortion.
- Sensor crop or an incorrect active sensor width.
- Point-depth differences or reference-plane tilt.
- Image-coordinate conventions and measurement uncertainty.

The proposed relationship does not establish that either value is the unique or universally correct focal length for a camera system.

## Conditions for Exactness Within the Ideal Model

The relationship is exact within the stated pinhole model only when all of the following hold:

1. The camera is modeled by a central perspective projection.
2. `D` is the distance from the projection center to the common A–B plane.
3. A and B have equal depth.
4. A–B is parallel to the camera-horizontal direction used by `xA` and `xB`.
5. The physical length `AB` is measured along that segment.
6. `W_sensor` is the active sensor width corresponding to the captured image width `W_image`.
7. Pixel coordinates are linearly mapped across the active sensor width.
8. Lens distortion, crop ambiguity, resampling distortion, and rolling-shutter effects are absent or negligible.
9. A and B are correctly identified and measured.

The relationship is an approximation when sensor-plane distance substitutes for projection-center distance, when the lens is focused at finite distance, or when real optical and image-processing effects are non-negligible.

## Invalid or Unreliable Conditions

The calculation is invalid or unreliable when:

- A and B have materially different depths and no depth correction is made.
- The reference plane is tilted and the equal-depth approximation is used.
- A–B is not aligned with the camera-horizontal direction while full `AB` is used.
- The active sensor width is unknown, cropped, or does not correspond to the captured image width.
- The image has been resized, cropped, rotated, mirrored, or otherwise transformed without documented registration.
- Lens distortion materially affects the measured locations.
- The lens has focus-dependent focal behavior not represented by the model.
- The sensor-plane distance is used as though it were the projection-center distance without an accepted optical approximation.
- Point correspondence or physical measurements are uncertain.

## Uncertainty and Limitations

The calculated value inherits uncertainty from image coordinates, image width, active sensor width, distance `D`, physical distance `AB`, and model assumptions. A relative uncertainty analysis is not developed here because the uncertainty model and measurement protocol have not yet been approved.

Repeat measurements should state their conditions. NIST Technical Note 1297 distinguishes repeatability under the same measurement conditions from reproducibility under changed conditions. Those terms provide useful measurement vocabulary but do not establish TPS acceptance criteria.

No numerical tolerance, uncertainty budget, or experimental performance claim is established by this derivation.

## Established Mathematics Versus TPS Interpretation

The pinhole projection relationship, the equal-depth reduction, unit analysis, and the numerical checks are established mathematical consequences of the stated ideal model.

The name “Working Focal Length,” the sensor-plane distance convention, the choice to preserve the calculated value in a TPS reference, and the use of this relationship for TPS are TPS-specific interpretations. They require further review and validation.

## Supporting Sources

- MIT, *Foundations of Computer Vision*, §5.3.1, “Image Formation by Perspective Projection”: https://visionbook.mit.edu/imaging.html
- Richard Hartley and Andrew Zisserman, *Multiple View Geometry in Computer Vision*: https://robots.ox.ac.uk/~vgg/hzbook/hzbook1.html
- Edmund Optics, “Understanding Focal Length and Field of View,” especially the “Focal Length” and “Field of View” sections: https://www.edmundoptics.com/knowledge-center/application-notes/imaging/understanding-focal-length-and-field-of-view
- NIST Technical Note 1297, Appendix D1.1.2–D1.1.3: https://www.nist.gov/pml/nist-technical-note-1297

No experimental validation is claimed.
