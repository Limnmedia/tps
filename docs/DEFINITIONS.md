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
