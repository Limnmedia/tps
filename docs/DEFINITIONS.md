# Definitions

## Review Statuses

- **Proposed:** Under discussion.
- **Approved:** Reviewed and accepted for the working draft.
- **Validated:** Supported by mathematical proof or appropriate testing.

## Definition 1 — Physical Point

**Plain-language definition:**

A point is a particular spot in the real world.

**Precise definition:**

A physical point is a specified location in three-dimensional Euclidean space, independent of the camera observing it.

**Classification:** Foundational geometric definition.

**Status:** Approved — Working Draft 0.1

**Explanation:**

A physical point identifies a location in the three-dimensional world.

It is not necessarily a physical object.

A visible mark, corner, or identifiable feature may represent a physical point.

The point exists independently of the camera used to observe it.

TPS uses three corresponding physical points, conventionally identified as A, B, and C.

This definition does not require:

- A particular coordinate system.
- A particular unit of measurement.
- A particular camera or lens.
- A physical marker attached to the location.
- Knowledge of the point's absolute coordinates.

A physical point must not be confused with its two-dimensional image projection.

## Definition 2 — Image Point

**Plain-language definition:**

An image point is where a spot in the real world appears in a picture.

**Precise definition:**

An image point is a location in a two-dimensional image coordinate system corresponding to the projection of a physical point through a camera.

**Classification:** Foundational projection geometry definition.

**Status:** Approved — Working Draft 0.1

**Explanation:**

A camera projects visible physical points into a two-dimensional image.

Each projected physical point has a corresponding location in that image.

This location is called an image point.

An image point can be represented using two image coordinates.

The image point and its corresponding physical point are related, but they are not the same geometric entity.

An image point:

- Is a location in image space.
- Is not necessarily a pixel.
- May have fractional image coordinates.
- Does not independently specify the physical point's distance from the camera.
- Does not require a particular image resolution or pixel coordinate convention.

A physical point exists in three-dimensional space.

Its image point exists in a two-dimensional image coordinate system.

TPS relates these two geometric entities.

## Definition 3 — Correspondence

**Plain-language definition:**

Each point in the real world is matched to where that same point appears in the image.

**Precise definition:**

Correspondence is the established association between a specific physical point and its projected location in a two-dimensional image.

**Classification:** Foundational geometric relationship.

**Status:** Approved — Working Draft 0.1

**Explanation:**

TPS establishes correspondence between three physical points and their projected image points.

By convention:

- Physical point A corresponds to image point a.
- Physical point B corresponds to image point b.
- Physical point C corresponds to image point c.

These associations identify which image point belongs to which physical point.

Correspondence must remain consistent when comparing two projections.

The identity of each point is preserved even when its projected image coordinates change.

Correspondence:

- Identifies which physical point produced each image point.
- Does not require knowledge of the camera's position.
- Does not require knowledge of camera orientation.
- Does not require knowledge of focal length.
- Does not establish physical distances or angles.
- Does not establish that matching three corresponding image points uniquely determines a camera configuration.

Correspondence must not be confused with proximity.

For example, image point a remains associated with physical point A, even if image point b happens to appear closer to A's previous image location.

## Definition 4 — Projection

**Plain-language definition:**

A camera turns the locations of points in the real world into locations in an image.

**Precise definition:**

Projection is the geometric mapping of physical points in three-dimensional space to corresponding locations in a two-dimensional image, according to a camera model.

**Classification:** Foundational geometric transformation.

**Status:** Approved — Working Draft 0.1

**Explanation:**

A physical point has a location in three-dimensional space.

A camera represents that physical point at a corresponding location in a two-dimensional image.

The geometric relationship between these locations is called projection.

Projection depends on the camera's position, orientation, and imaging properties.

TPS establishes correspondence between three physical points and their projected image points.

By convention:

- Physical point A → Image point a
- Physical point B → Image point b
- Physical point C → Image point c

The three-point relationship can be expressed as:

```text
Three physical points
        ↓
     Projection
        ↓
Three corresponding image points
```

This is a conceptual relationship, not yet a mathematical formula.

Projection:

- Maps physical points into image space.
- Depends on the camera model.
- Does not generally preserve physical distances.
- Does not generally preserve physical angles.
- Does not independently establish physical depth.
- Does not necessarily provide a unique inverse mapping from an image point to a physical point.

Projection must not be confused with correspondence.

Correspondence identifies which physical point is associated with which image point.

Projection describes the geometric mapping between those points.

TPS does not require a particular camera, software application, or recording medium.

## Definition 5 — Three-Point Projection

**Plain-language definition:**

A three-point projection is where three points appear in an image.

**Precise definition:**

A three-point projection is the ordered arrangement of three image points corresponding to three identified physical points.

**Classification:** TPS-specific geometric definition.

**Status:** Approved — Working Draft 0.1

**Explanation:**

TPS identifies three physical points conventionally labeled A, B, and C.

A camera projects these points into a two-dimensional image at corresponding locations a, b, and c.

The ordered arrangement of these three image points is called a three-point projection.

Correspondence is preserved:

- Physical point A → Image point a
- Physical point B → Image point b
- Physical point C → Image point c

The three-point projection describes the arrangement in image space, not the physical triangle itself.

### Order and Identity

The three image points are identified, not anonymous.

Their correspondence to A, B, and C must remain consistent when recording, comparing, or reproducing a three-point projection.

The term "ordered" establishes this consistent identity convention. It does not imply that the points must be arranged in a particular spatial order within the image.

### Degenerate Projections

Three non-collinear physical points may produce collinear or coincident image points under certain camera configurations.

These are still three-point projections. However, they may not contain sufficient geometric information for a particular TPS operation.

Therefore, distinguish:

- **Three-point projection:** The three corresponding image locations.
- **Valid TPS reference:** A three-point projection satisfying the conditions required for the intended TPS operation.

The validity conditions will be established later under assumptions, constraints, and geometric analysis.

A three-point projection:

- Exists in two-dimensional image space.
- Preserves the identity of corresponding points.
- Does not preserve physical distances or angles in general.
- Does not independently establish camera position.
- Does not independently establish focal length.
- Does not necessarily reproduce the entire image.
- May be geometrically degenerate.

## Definition 6 — TPS Reference

**Plain-language definition:**

A TPS reference remembers where three points appeared in an image.

**Precise definition:**

A TPS reference is a recorded three-point projection that preserves the correspondence and image locations of three identified physical points for subsequent comparison or reproduction.

**Classification:** TPS-specific operational definition.

**Status:** Approved — Working Draft 0.1

**Explanation:**

A TPS reference preserves the relationship between three identified physical points and their corresponding locations in an image.

By convention:

- Physical point A → Image point a
- Physical point B → Image point b
- Physical point C → Image point c

The reference preserves the identities and image locations of a, b, and c.

These recorded locations can later be compared against another camera projection.

A TPS reference may be recorded using physical marks, transparent overlays, photographic media, digital coordinates, or other suitable methods.

The reference is information, not a particular recording technology.

### Image Coordinate Frame

A TPS reference must establish an image coordinate frame in which its recorded point locations are meaningful.

The reference must be registered consistently when comparing or reproducing a projection.

For example:

- A transparent overlay may be registered against a camera monitor.
- Three marks may be placed directly on a fixed display surface.
- A digital reference may use a defined image coordinate system.
- Photographic media may use physical registration marks or another repeatable alignment method.

The specific registration methods and their accuracy requirements will be defined later.

A TPS reference preserves:

1. Three identified physical points: A, B, and C.
2. Their corresponding image locations: a, b, and c.
3. Explicit correspondence: A → a, B → b, and C → c.
4. Image coordinate-frame information sufficient to interpret and register the recorded locations.
5. Physical triangle geometry, including the measured relationships between A, B, and C.
6. Focus distance, measured from the camera sensor plane to the designated reference plane.
7. Working Focal Length.

The reference preserves the information required to reproduce the recorded view. It remains independent of any particular software, file format, or recording medium.

### Working Focal Length

TPS calculates the Working Focal Length once when establishing the reference using:

```text
f_TPS = (|xB - xA| / W_image) * W_sensor * (D / AB)
```

Here, `xA` and `xB` are horizontal image coordinates after accounting for recorded camera roll. `W_image` is the captured image width in pixels. `W_sensor` is the active physical sensor width in millimeters. `D` is the measured sensor-plane-to-reference-plane distance in millimeters. `AB` is the measured physical A–B distance in millimeters.

The calculation assumes that A and B are at approximately equal depth and aligned as closely as practical with camera-horizontal. Roll correction accounts for image rotation; it does not correct physical A–B misalignment.

The calculated value is recorded in the TPS reference.

Downstream applications, including VFX pipelines, may independently recalculate or reinterpret focal length for their own requirements. The original TPS value remains preserved.

The calculation inputs needed for reproducibility and verification are retained.

Sensor-plane distance is a practical measurement convention. Relative to ideal projection-center geometry, the result is approximate. The Working Focal Length is not necessarily identical to the lens manufacturer's nominal focal length. See the [Working Focal Length Derivation](../research/derivations/WORKING_FOCAL_LENGTH.md) for the mathematical derivation and limitations.

A TPS reference must not be confused with the physical triangle itself.

The reference records the image-space relationship, not the physical geometry.

## Definition 7 — Projection Match

**Plain-language definition:**

A projection matches when the three points appear in the same places as the reference.

**Precise definition:**

A projection match occurs when the three corresponding image points occupy the same locations as those recorded in a TPS reference, within a specified tolerance and a consistently registered image coordinate frame.

**Classification:** TPS-specific operational definition.

**Status:** Approved — Working Draft 0.1

**Explanation:**

A TPS reference records the image locations of three identified physical points: A, B, and C.

Their corresponding image points are a, b, and c.

A projection match occurs when a subsequent camera projection places these three image points at the same locations as the reference, either exactly or within an established tolerance.

The comparison must use a consistently registered image coordinate frame.

### Types of Match

1. **Exact Match**

   All three corresponding image points occupy precisely the same image coordinates as the reference.

   This is the ideal mathematical condition.

2. **Practical Match**

   All three corresponding image points agree with their reference locations within a specified tolerance.

   This accommodates measurement uncertainty, equipment limitations, and physical adjustment errors.

Both describe the same underlying TPS correspondence principle.

### Tolerance

A practical match requires an established tolerance.

The tolerance must be defined in terms appropriate to the image coordinate frame and measurement method.

Examples of possible measurement methods include:

- Visual alignment using a physical overlay.
- Alignment using registration marks.
- Numerical comparison of image coordinates.
- Software-assisted measurement.

Numerical tolerances are not established here.

Tolerance definitions, error metrics, and acceptance criteria belong to later mathematical analysis and validation.

A projection match:

- Preserves correspondence between A, B, and C.
- Requires consistent image registration.
- Compares image-space locations.
- Does not require matching physical coordinate systems.
- Does not independently establish a unique camera position.
- Does not require identical focal lengths.
- Does not guarantee reproduction of the entire image.
- Does not guarantee that unrelated physical points project to identical image locations.

A practical match must not be described as mathematically exact.
