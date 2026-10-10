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
