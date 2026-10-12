# TPS NotebookLM Research Package

Generated research artifact. The repository remains authoritative; included source documents are reproduced verbatim.

## Index

| Original file path | Document title | Document category |
|---|---|---|
| README.md | Three Point System (TPS) | Overview |
| CHANGELOG.md | Changelog | Project record |
| SPECIFICATION.md | Three Point System (TPS) Specification | Specification |
| docs/OBSERVATIONS.md | TPS Observations | Specification support |
| docs/DEFINITIONS.md | TPS Definitions | Specification support |
| docs/INVARIANTS.md | TPS Invariants | Specification support |
| docs/CONSTRAINTS.md | Physical Triangle Constraints | Specification support |
| docs/GEOMETRY.md | TPS Geometry | Specification support |
| docs/USE_CASES.md | TPS Use Cases | Specification support |
| docs/VALIDATION.md | TPS Validation | Specification support |
| docs/SPECIFICATION_REVIEW.md | TPS Specification Review | Specification review |
| research/BIBLIOGRAPHY.md | TPS Bibliography | Research |
| research/EVIDENCE_MAP.md | TPS Evidence Map | Research |
| research/VERIFICATION_REPORT.md | TPS Verification Report | Research |
| research/PRIOR_ART_REVIEW.md | TPS Prior-Art Review | Research |
| research/INTERDISCIPLINARY_PRIOR_ART.md | Interdisciplinary TPS Prior Art | Research |
| research/derivations/IMAGE_REGISTRATION.md | Image Registration | Research derivation |
| research/derivations/PHYSICAL_IMAGE_TRIANGLES.md | Physical and Image Triangles | Research derivation |
| research/derivations/WORKING_FOCAL_LENGTH.md | Working Focal Length | Research derivation |
| research/papers/PAPER_01_REVISED.md | The Three Point System: A Reference-Based Method for Camera-View Reproduction | Academic paper |

## Manifest

The package contains 20 source documents. `research/papers/PAPER_01_DRAFT.md` is excluded because it is an earlier duplicate of the revised paper. Git metadata, generated files, binary assets, and unrelated application code are excluded.

Included paths:

- README.md
- CHANGELOG.md
- SPECIFICATION.md
- docs/OBSERVATIONS.md
- docs/DEFINITIONS.md
- docs/INVARIANTS.md
- docs/CONSTRAINTS.md
- docs/GEOMETRY.md
- docs/USE_CASES.md
- docs/VALIDATION.md
- docs/SPECIFICATION_REVIEW.md
- research/BIBLIOGRAPHY.md
- research/EVIDENCE_MAP.md
- research/VERIFICATION_REPORT.md
- research/PRIOR_ART_REVIEW.md
- research/INTERDISCIPLINARY_PRIOR_ART.md
- research/derivations/IMAGE_REGISTRATION.md
- research/derivations/PHYSICAL_IMAGE_TRIANGLES.md
- research/derivations/WORKING_FOCAL_LENGTH.md
- research/papers/PAPER_01_REVISED.md

==================================================
SOURCE: README.md
==================================================
# Three Point System (TPS)

The Three Point System (TPS) is an open, implementation-independent specification for relating three physical points to their corresponding 2D image projections.

## TPS Kernel

"TPS connects three points in the physical world with where
those same three points appear in an image."

TPS is independent of software and hardware. It may be implemented using physical overlays, camera monitors, film, or software.

**Current specification status:** TPS Specification v0.1 — Candidate.

The candidate records approved specification material. Mathematical derivations remain in the research directory, and experimental validation is recorded separately. The candidate is not yet experimentally validated. See [SPECIFICATION.md](SPECIFICATION.md).

See the [primary use case](docs/USE_CASES.md).

==================================================
SOURCE: CHANGELOG.md
==================================================
# Changelog

## TPS Specification v0.1 — Candidate

- Established the current specification as the TPS Specification v0.1 Candidate for academic paper development.
- Recorded that the two previously identified blocking findings have been addressed.
- Preserved unresolved clarification and research findings.
- Confirmed the distinction between approved specification material, mathematical derivations, and experimental validation.
- Confirmed that the candidate is not yet experimentally validated.

## Working Draft 0.1

- Initialized the TPS specification working draft.

==================================================
SOURCE: SPECIFICATION.md
==================================================
# Three Point System (TPS) Specification

**Status:** TPS Specification v0.1 — Candidate

This candidate records the approved TPS specification baseline. Mathematical derivations remain documented in the research directory, and experimental validation remains separate. The candidate is not yet experimentally validated. The two blocking findings identified in the specification review have been addressed; the remaining clarification and research findings are preserved in [docs/SPECIFICATION_REVIEW.md](docs/SPECIFICATION_REVIEW.md).

## TPS Kernel

"TPS connects three points in the physical world with where
those same three points appear in an image."

## 1. Observations

See [docs/OBSERVATIONS.md](docs/OBSERVATIONS.md).

## 2. Definitions

See [docs/DEFINITIONS.md](docs/DEFINITIONS.md).

## 3. Invariants

See [docs/INVARIANTS.md](docs/INVARIANTS.md).

## 4. Assumptions and Constraints

See [docs/CONSTRAINTS.md](docs/CONSTRAINTS.md).

## TPS Reference Requirements

A TPS reference must preserve the minimum contents defined in [Definition 6 — TPS Reference](docs/DEFINITIONS.md#definition-6--tps-reference). These contents include the identified physical points A, B, and C; their corresponding image locations a, b, and c; explicit correspondence; measured physical triangle relationships; the TPS Reference Distance (D); the actual captured image width and height; active physical sensor dimensions when known; an interpretable image coordinate frame; Working Focal Length and its calculation inputs; and the calculated horizontal angle of view (AOV).

The captured image dimensions are authoritative for that capture. They must not be replaced with the camera's native sensor pixel resolution. When physical sensor dimensions are recorded, they must correspond to the active imaging area represented by the capture.

TPS calculates and records the Working Focal Length when establishing the reference. Calculation inputs are retained for reproducibility and verification. Downstream applications may independently recalculate or reinterpret focal length, but the original TPS value remains preserved.

A three-point projection describes correspondence between physical points and image locations. A TPS reference preserves the information required to reproduce the recorded view. These are related but distinct concepts.

### TPS Reference Distance and Working Focal Length

The TPS Reference Distance (D) is the measured distance from the camera sensor plane to the designated physical reference plane. It is distinct from a lens focus-ring marking, an optical projection-center distance, or a manufacturer-reported focus distance. The sensor-plane convention is practical and makes the calculation approximate relative to ideal projection-center geometry.

When establishing a TPS reference, TPS calculates and records the following related quantities:

```text
f_px = |xB - xA| * D / AB

AOV_h = 2 * atan(AB * W_image / (2 * D * |xB - xA|))

f_mm = f_px * W_sensor / W_image
```

Here, `xA` and `xB` are roll-corrected horizontal image coordinates. `AB` is the measured physical A–B distance. `W_image` is the actual captured image width in pixels. `W_sensor` is the active physical sensor width in millimeters.

The calculation assumes that A and B are at approximately equal depth and that A–B is aligned as closely as practical with camera-horizontal. Roll correction accounts for image rotation; it does not correct physical A–B misalignment. The relationships share the assumptions and approximations documented in the [Working Focal Length Derivation](research/derivations/WORKING_FOCAL_LENGTH.md) and are not presented as universally exact optical identities.

`f_px` and `AOV_h` do not require physical sensor dimensions. `f_mm` requires the active physical sensor width. If physical sensor dimensions are unavailable, the TPS reference remains usable and can preserve `f_px` and `AOV_h` without calculating `f_mm`. The AOV is derived from the TPS geometry; it is not assumed as an independent camera specification and does not determine a missing physical sensor width.

Sensor-plane distance is a practical measurement convention. Relative to ideal projection-center geometry, the result is approximate. The Working Focal Length is not necessarily identical to the lens manufacturer's nominal focal length.

The calculated value and necessary inputs are preserved with the TPS reference. Downstream VFX applications may independently calculate or reinterpret focal length without overwriting the original TPS value. The complete derivation and limitations are documented in [Working Focal Length Derivation](research/derivations/WORKING_FOCAL_LENGTH.md).

### Recovery

Recovery compares the recorded three-point projection with the corresponding points in a live camera view. The user adjusts the camera to obtain the closest practical match. The recorded reference points must be presented in registration with the live viewing frame. A transparent reference over a television monitor, registered celluloid or film, and a digital overlay such as a transparent PNG are possible representations; none is mandatory. An overlay represents the TPS reference for comparison but is not the complete TPS reference itself. A recovery record may preserve observed image coordinates and comparison information, but saving one is optional. The recovery camera need not be identical to the original camera.

### Matching Principle

The objective is the closest practical match between corresponding three-point projections. Users refine the camera view through comparison with the TPS reference. TPS does not prescribe a universal numerical acceptance tolerance.

A projection match does not guarantee identical camera pose or complete scene alignment.

## 5. Geometric Model

See [docs/GEOMETRY.md](docs/GEOMETRY.md).

## 6. Mathematical Formulation

Reserved for review and development.

## 7. Validation

See [docs/VALIDATION.md](docs/VALIDATION.md).

==================================================
SOURCE: docs/OBSERVATIONS.md
==================================================
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

==================================================
SOURCE: docs/DEFINITIONS.md
==================================================
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

The minimum coordinate-frame information is:

- Image width and height.
- Coordinate origin.
- Axis directions.
- Coordinate units.
- Recorded positions of a, b, and c.
- Crop, rotation, or mirroring information when needed to interpret the coordinates.

The frame must be interpretable independently of the software that created it. TPS does not require a particular file format or universal coordinate convention.

A TPS reference preserves:

1. Three identified physical points: A, B, and C.
2. Their corresponding image locations: a, b, and c.
3. Explicit correspondence: A → a, B → b, and C → c.
4. Image coordinate-frame information sufficient to interpret and register the recorded locations.
5. Physical triangle geometry, including the measured relationships between A, B, and C.
6. TPS Reference Distance (D), measured from the camera sensor plane to the designated physical reference plane.
7. The actual captured image width and height in pixels. These dimensions are authoritative for the capture and must not be replaced by native sensor pixel resolution.
8. Active physical sensor dimensions in millimeters, when known, corresponding to the active imaging area represented by the capture.
9. Working Focal Length, its calculation inputs, and the calculated horizontal AOV.

The reference preserves the information required to reproduce the recorded view. It remains independent of any particular software, file format, or recording medium.

### Working Focal Length

TPS calculates the following related quantities once when establishing the reference:

```text
f_px = |xB - xA| * D / AB

AOV_h = 2 * atan(AB * W_image / (2 * D * |xB - xA|))

f_mm = f_px * W_sensor / W_image
```

Here, `xA` and `xB` are roll-corrected horizontal image coordinates. `AB` is the measured physical A–B distance. `D` is the TPS Reference Distance. `W_image` is the actual captured image width in pixels. `W_sensor` is the active physical sensor width in millimeters.

The calculation assumes that A and B are at approximately equal depth and aligned as closely as practical with camera-horizontal. Roll correction accounts for image rotation; it does not correct physical A–B misalignment. These relationships share the assumptions and approximations documented in the [Working Focal Length Derivation](../research/derivations/WORKING_FOCAL_LENGTH.md) and are not universally exact optical identities.

`f_px` and `AOV_h` do not require physical sensor dimensions. `f_mm` requires the active physical sensor width. If physical sensor dimensions are unavailable, the TPS reference remains usable. The AOV is derived from TPS geometry and does not independently determine a missing physical sensor width.

The calculated value is recorded in the TPS reference.

Downstream applications, including VFX pipelines, may independently recalculate or reinterpret focal length for their own requirements. The original TPS value remains preserved.

The calculation inputs needed for reproducibility and verification are retained.

Sensor-plane distance is a practical measurement convention. Relative to ideal projection-center geometry, the result is approximate. The Working Focal Length is not necessarily identical to the lens manufacturer's nominal focal length. See the [Working Focal Length Derivation](../research/derivations/WORKING_FOCAL_LENGTH.md) for the mathematical derivation and limitations.

The TPS Reference Distance is distinct from a lens focus-ring marking, an optical projection-center distance, and a manufacturer-reported focus distance.

### Recovery

Recovery compares the recorded three-point projection with the corresponding points in a live camera view. The user adjusts the camera to obtain the closest practical match, with the reference points presented in registration with the live viewing frame. A transparent reference over a television monitor, registered celluloid or film, or a digital overlay such as a transparent PNG may be used; none is mandatory. An overlay is a representation of the TPS reference, not the complete reference itself. A recovery record may preserve observed image coordinates and comparison information, but saving one is optional. The recovery camera need not be identical to the original camera.

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

==================================================
SOURCE: docs/INVARIANTS.md
==================================================
# Invariants

## Review Statuses

- **Proposed:** Under discussion.
- **Approved:** Reviewed and accepted for the working draft.
- **Validated:** Supported by mathematical proof or appropriate testing.

## Invariant 1 — Point Identity

**Plain-language statement:**

A is always A, B is always B, and C is always C.

**Precise statement:**

The identities of the three physical reference points and their corresponding image points must remain consistent throughout the recording, comparison, and reproduction of a TPS projection.

**Classification:** TPS correspondence invariant.

**Status:** Approved — Working Draft 0.1

**Explanation:**

TPS identifies three physical points:

A, B, and C.

Their corresponding image points are:

a, b, and c.

The relationships are:

- A → a
- B → b
- C → c

These identities must remain consistent.

As the camera moves, the image coordinates of a, b, and c may change.

However, their correspondence to A, B, and C must not change.

For example, image point a always represents physical point A, regardless of where it appears in the image.

Point identity:

- Is independent of image coordinates.
- Is independent of camera position.
- Is independent of camera orientation.
- Is independent of focal length.
- Must remain consistent across TPS references and subsequent projection comparisons.
- Does not require the physical points to remain stationary.

Physical point stability is a separate geometric constraint and will be examined later.

## Invariant 2 — Triangle Shape Under Similarity

**Plain-language statement:**

A triangle can change size without changing its shape.

**Precise statement:**

When a physical triangle is uniformly scaled, the ratios of its corresponding side lengths and its internal angles remain unchanged.

**Classification:** Conditional geometric similarity invariant.

**Status:** Approved — Working Draft 0.1

**Explanation:**

Three non-collinear physical points A, B, and C define a triangle.

The triangle may be translated, rotated, or uniformly scaled.

Translation and rotation preserve its physical side lengths and internal angles.

Uniform scaling changes all side lengths by the same scale factor while preserving their ratios and internal angles.

For example, an original triangle with side lengths 100 mm, 150 mm, and 200 mm can be uniformly scaled to side lengths 200 mm, 300 mm, and 400 mm. Both triangles have the same shape.

### Scope

This invariant describes the mathematical properties of geometrically similar triangles.

It does not establish that:

- TPS universally requires geometrically similar physical triangles.
- Uniform scaling guarantees a projection match.
- Triangle orientation is irrelevant.
- Triangle placement is irrelevant.
- Camera parameters can be ignored.
- Any arbitrary triangle can replace the original.

The conditions under which TPS can use a relocated, rotated, scaled, or differently shaped triangle remain subjects for geometric analysis.

### Practical Setup Note

The following is a proposed operating recommendation, not an invariant:

> Position the TPS triangle near the standard L2D reference location, within practical tolerances. Aim to keep the A–B side horizontal.

L2D is not defined here. Numerical placement tolerances are not introduced. This recommendation belongs to a future practical setup or recommended-practices section.

==================================================
SOURCE: docs/CONSTRAINTS.md
==================================================
# Physical Triangle Constraints

**Status:** Approved — Working Draft 0.1

## Core Principle

**Plain language:**

The three points must keep their intended relationship to one another.

**Precise statement:**

During a TPS projection-matching operation, the physical reference points must maintain the geometric relationships specified for that operation.

**Classification:** Operational constraint. This is not a mathematical invariant.

## Operating Cases

### 1. Same Triangle, Same Location

The original physical triangle remains in place. The camera is moved and its projection is recovered.

### 2. Same Triangle, Different Location

The original physical triangle is relocated. Its internal geometry is preserved.

The camera and triangle may have different positions and orientations in world space.

### 3. Different Triangle, Different Location

Another physical triangle is established at a different location.

Its geometric relationship to the original triangle must be explicitly specified.

Geometric similarity is one possible relationship, but is not yet established as universally required by TPS.

## Important Distinctions

- Physical point identity must remain consistent within each correspondence set.
- A replacement triangle may use different physical points, provided their correspondence to the reference identities is established.
- A TPS reference records image-point locations and correspondence.
- Matching a TPS reference does not necessarily recover the original camera pose.
- Matching three points does not guarantee matching the entire scene.
- The conditions permitting replacement triangles require further geometric investigation.

## Practical Setup

**Proposed — Recommended Practice**

Position the TPS triangle near the standard L2D reference location, within practical tolerances. Aim to keep the A–B side horizontal.

This remains a proposed recommendation, not a requirement. L2D and numerical tolerances are not defined here.

## Scope

This document describes operating conditions.

It does not establish:

- A universal triangle shape requirement.
- A universal triangle size requirement.
- A fixed world-space location.
- A required horizontal orientation.
- Unique camera pose recovery.
- Guaranteed projection matching from triangle similarity alone.

## Documentation

The repository maintains the following distinction:

- **Observations:** What can be observed.
- **Definitions:** What terms mean.
- **Invariants:** What remains mathematically unchanged under specified transformations.
- **Constraints:** What an operation requires or assumes.

==================================================
SOURCE: docs/GEOMETRY.md
==================================================
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

## Geometry Principle 3 — Projection Ambiguity

**Status:** Approved — Working Draft 0.1

**Classification:** Geometric principle.

### Plain-Language Statement

Different camera setups can make the same three points appear in the same places in an image.

### Precise Statement

Under perspective projection, distinct configurations of physical points and camera parameters can produce identical image coordinates for three corresponding points.

### Explanation

A TPS reference records the image locations of three corresponding physical points:

- A → a
- B → b
- C → c

Reproducing these image locations establishes a three-point projection match.

However, the same image coordinates may be produced by more than one physical and camera configuration.

Therefore, matching a TPS reference does not necessarily recover the original camera's:

- Position
- Orientation
- Focal length
- Complete physical configuration

### Example — Uniform Scaling

Consider a physical triangle observed through an ideal perspective camera.

If the positions of all three physical points relative to the camera's projection center are uniformly scaled by the same positive factor, their projected image coordinates remain unchanged, provided that:

- Camera orientation remains unchanged.
- Camera intrinsic parameters remain unchanged.
- Correspondence is preserved.
- The ideal perspective camera model applies.

This demonstrates that physically different configurations can produce identical three-point projections.

It also illustrates why a geometrically similar triangle may be useful when reproducing a reference at a different physical scale.

### Important Distinction

**Projection matching:** Reproducing the recorded image coordinates of three corresponding physical points.

**Camera reconstruction:** Determining the camera's physical position, orientation, and intrinsic parameters.

These are related but distinct objectives.

TPS establishes a method of recording and comparing three-point projections.

A projection match alone does not establish unique camera reconstruction.

Additional measurements or constraints may be required to determine a particular camera configuration.

### Scope

This principle does not establish:

- That all different triangles can reproduce the same projection.
- That triangle similarity alone guarantees a projection match.
- That every camera configuration has multiple solutions under every set of constraints.
- That camera reconstruction is impossible.
- That a three-point match guarantees alignment of the entire scene.
- A specific reconstruction algorithm.
- A focal-length calculation.
- A camera calibration procedure.

## Geometry Principle 4 — Projection Equivalence

**Status:** Approved — Working Draft 0.1

**Classification:** Geometric principle.

### Plain-Language Statement

Two TPS views match when A, B, and C appear in the same places in both images.

### Precise Statement

Two three-point projections are equivalent when their corresponding image points occupy identical locations in a common image coordinate frame.

### Explanation

A TPS reference records three corresponding image points:

- A → a
- B → b
- C → c

Two three-point projections are equivalent when their corresponding image-point locations agree after both are expressed in a common, consistently registered image coordinate frame.

This comparison requires:

- Consistent point correspondence.
- A defined image coordinate frame.
- Consistent registration between the reference and comparison frames.
- Equality of corresponding image-point locations.

### Image Coordinates

Distinguish between:

1. **Pixel coordinates**

   Positions expressed in the coordinate system of a particular raster image.

2. **Normalized image coordinates**

   Positions expressed relative to a defined image coordinate frame.

Different pixel dimensions do not necessarily prevent projection equivalence.

### Example

An image with 1920 × 1080 pixels may place point a at (480, 270). An image with 3840 × 2160 pixels may place point a at (960, 540). In both images, point a is located 25% of the way across and 25% of the way down the image.

These positions are equivalent under a consistent full-frame normalization convention.

This example demonstrates coordinate equivalence for one point. A complete three-point projection match requires equivalent positions for all three corresponding points.

### Important Distinctions

- Equal pixel coordinates are not required when image dimensions differ.
- Equal normalized coordinates alone do not establish equivalence unless the coordinate frames and their registration are defined consistently.
- Resizing, cropping, rotation, mirroring, and changes in image aspect ratio may alter the relationship between coordinate frames.
- Any transformations used to register the images must be explicitly defined.
- A projection match does not require identical image resolutions.
- A projection match does not require identical physical triangles, cameras, or lenses.
- Equivalence of three-point projections does not imply equivalence of the complete photographs.

### Exact and Practical Matching

Distinguish:

**Exact equivalence:** All three corresponding image-point locations agree in the common coordinate frame.

**Practical matching:** The corresponding locations agree within a specified tolerance.

Numerical tolerance is not established here, and the existing Projection Match definition is not redefined.

### TPS Implication

TPS references can be compared across different image representations when their coordinate frames are consistently registered.

Projection equivalence concerns the recorded locations of corresponding image points, not the uniqueness of the underlying physical configuration.

### Scope

This principle does not establish:

- A required image resolution.
- A required image aspect ratio.
- A universal normalization convention.
- An automatic crop-detection procedure.
- An image-registration algorithm.
- A numerical matching tolerance.
- Unique camera reconstruction.
- Equivalence of entire photographs.

==================================================
SOURCE: docs/USE_CASES.md
==================================================
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
- The physical triangle geometry, TPS Reference Distance, actual captured image dimensions, coordinate-frame information, and Working Focal Length can be recorded as part of the TPS reference.

## Method

1. Identify three physical reference points A, B, and C.
2. Establish their corresponding image points a, b, and c.
3. Record their correspondence and image locations in a consistently defined image coordinate frame.
4. Preserve the physical triangle geometry.
5. Record the TPS Reference Distance, measured from the camera sensor plane to the designated reference plane, and the actual captured image width and height.
6. Record the coordinate-frame information needed to interpret and register the image points, and preserve physical sensor dimensions when known.
7. Calculate the Working Focal Length and horizontal AOV once when establishing the TPS reference, and preserve the calculated values and necessary calculation inputs.
8. During recovery, present the recorded reference points in registration with the live viewing frame, establish the corresponding physical reference points, and adjust the camera view to obtain the closest practical match.

An overlay may be used for registration, including a transparent reference over a television monitor, registered celluloid or film, or a digital overlay such as a transparent PNG. These are examples, not mandatory technologies. A recovery record is optional.

## Expected Outcome

The recorded three-point projection is reproduced as the closest practical match available under the operating conditions. TPS does not prescribe a universal numerical acceptance tolerance.

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

==================================================
SOURCE: docs/VALIDATION.md
==================================================
# Validation

This document is a placeholder for experimental validation.

Mathematical verification and physical camera experiments are distinct forms of validation and will be documented separately.

==================================================
SOURCE: docs/SPECIFICATION_REVIEW.md
==================================================
# TPS Specification Review

**Review scope:** Final technical review before academic paper development.

**Reviewed revision:** `54a18cd760d2baf8438278195e1001921e38c6d8`

**Review conclusion:** TPS is a coherent practical view-matching framework, but it is not yet independently implementable as a fully specified measurement procedure. The conceptual model is strong; the remaining work is concentrated in coordinate registration, reference-record semantics, operational measurement conventions, and validation.

## Finding Categories

- **Blocking:** Prevents an independent implementation from making a consistent TPS reference or comparison.
- **Clarification:** Wording or definition needs improvement but does not necessarily prevent a prototype.
- **Research:** Requires derivation, source review, or experiment.
- **Editorial:** Presentation or organization only.

## Blocking Findings Status

The two blocking findings from this review are addressed by the current specification updates:

1. The minimum image coordinate-frame record is now defined in `docs/DEFINITIONS.md`, including image dimensions, origin, axes, units, point positions, and relevant crop, rotation, or mirroring information.
2. TPS reference and recovery semantics are now defined in `SPECIFICATION.md`, `docs/DEFINITIONS.md`, and `docs/USE_CASES.md`, including the reference contents, TPS Reference Distance, retained calculation inputs, registered live-view comparison, optional recovery records, and closest-practical-match objective.

The remaining findings are clarifications, research items, or editorial work and do not prevent the stated operational model from being understood.

## Findings

### Addressed — Former Blocking 1: Image coordinate frame

- **File and section:** `docs/DEFINITIONS.md`, Definition 6 — TPS Reference, “Image Coordinate Frame”; `docs/GEOMETRY.md`, Geometry Principle 4 — Projection Equivalence; `research/derivations/IMAGE_REGISTRATION.md`
- **Description:** Resolved. The minimum recorded coordinate-frame information is now specified without prescribing a file format or universal convention.
- **Why it matters:** Independent implementations now have the minimum semantic information needed to interpret and register recorded points.
- **Recommended correction:** No further blocking correction. Research may refine registration procedures later.

### Addressed — Former Blocking 2: Reference input and recovery records

- **File and section:** `SPECIFICATION.md`, “TPS Reference Requirements” and “Working Focal Length”; `docs/DEFINITIONS.md`, Definition 6 — TPS Reference; `docs/USE_CASES.md`, UC-001 Method
- **Description:** Resolved. The reference contents, TPS Reference Distance, captured-image dimensions, active sensor dimensions when known, frame semantics, calculations, and recovery comparison model are now defined.
- **Why it matters:** Independent implementations can identify the required reference information while retaining implementation independence.
- **Recommended correction:** No further blocking correction. Experimental validation remains necessary for practical performance and measurement limits.

### Clarification 1 — Working Focal Length status is ambiguous

- **File and section:** `SPECIFICATION.md`, “Working Focal Length”; `docs/DEFINITIONS.md`, Definition 6; `research/derivations/WORKING_FOCAL_LENGTH.md`
- **Description:** The specification presents the formula as the TPS calculation, while the derivation states that it is not an approved mathematical formulation and is not experimentally validated.
- **Why it matters:** Readers may interpret the formula as a validated optical law rather than an approved TPS convention based on an idealized derivation.
- **Recommended correction:** Label the formula in the specification as an approved TPS calculation convention based on stated assumptions, and retain its approximation and non-validation status.

### Clarification 2 — “Roll correction” and physical A–B alignment are distinct but underspecified

- **File and section:** `SPECIFICATION.md`, “Working Focal Length”; `docs/DEFINITIONS.md`, Definition 6; `research/derivations/WORKING_FOCAL_LENGTH.md`, “A–B Orientation”
- **Description:** The specification correctly says roll correction does not fix physical A–B misalignment, but does not state how roll is identified or what “aligned as closely as practical” means.
- **Why it matters:** Different implementations may apply different rotations or use different physical alignment assumptions while calculating the same named quantity.
- **Recommended correction:** Define roll correction as a coordinate-frame operation recorded with the reference. Keep physical alignment as an approximation and do not add a universal angular threshold.

### Clarification 3 — Focus distance terminology needs separation from Working Focal Length inputs

- **File and section:** `docs/DEFINITIONS.md`, Definition 6; `SPECIFICATION.md`, TPS Reference Requirements
- **Description:** “Focus distance” is a required reference item, while `D` is the sensor-plane-to-reference-plane distance used by the Working Focal Length calculation. The documents do not explicitly state whether these are the same recorded quantity or two distinct quantities.
- **Why it matters:** An implementation could substitute a lens-reported focus distance, a subject distance, or a sensor-plane measurement without preserving the intended convention.
- **Recommended correction:** State whether focus distance and `D` are synonymous for TPS or are separate fields. Preserve the sensor-plane convention if that remains approved.

### Clarification 4 — “Projection match,” “projection equivalence,” and “closest practical match” overlap

- **File and section:** `docs/DEFINITIONS.md`, Definition 7; `docs/GEOMETRY.md`, Geometry Principle 4; `SPECIFICATION.md`, “Matching Principle”
- **Description:** These sections describe related comparison states but do not establish a concise relationship between exact equivalence, practical matching, and the user-directed closest practical match.
- **Why it matters:** Implementations may report different outcomes using the same terms.
- **Recommended correction:** Adopt a short terminology hierarchy: equivalence describes comparison in a common frame; exact match uses equality; practical match uses an operator- or user-selected tolerance; closest practical match is an adjustment objective, not a universal pass/fail condition.

### Clarification 5 — Physical triangle replacement cases are not connected to reference validity

- **File and section:** `docs/CONSTRAINTS.md`, “Operating Cases”; `docs/DEFINITIONS.md`, Definition 5 — Three-Point Projection
- **Description:** The three operating cases are documented, but the specification does not state which reference data remain authoritative when the same triangle is relocated or a different triangle is used.
- **Why it matters:** A replacement triangle may preserve, alter, or fail the physical relationships needed by a particular operation.
- **Recommended correction:** Define operation-specific reference validity later. Do not promote triangle similarity to a universal requirement.

### Research 1 — Working Focal Length and real-lens geometry

- **File and section:** `research/derivations/WORKING_FOCAL_LENGTH.md`, “Sensor Plane, Projection Center, and Focus Distance” and “Conditions for Exactness Within the Ideal Model”
- **Description:** The derivation shows exactness only under an ideal central-projection model and identifies sensor-plane distance, finite focus, principal-plane offsets, unequal depths, tilt, and distortion as limitations.
- **Why it matters:** The practical quantity may be reproducible without being identical to nominal or effective optical focal length.
- **Recommended correction:** Validate the convention experimentally across representative lenses and distances before presenting it as a general optical result.

### Research 2 — Unequal depths and reference-plane tilt

- **File and section:** `research/derivations/WORKING_FOCAL_LENGTH.md`, “Unequal Point Depths” and “Reference-Plane Tilt”
- **Description:** The derivation identifies bias but does not establish an accepted correction or an operational validity boundary.
- **Why it matters:** Small physical departures from equal depth may materially affect the recorded value.
- **Recommended correction:** Measure sensitivity experimentally and document conditions under which the approximation is usable. Do not invent a tolerance in this review.

### Research 3 — Registration transformations and false agreement

- **File and section:** `research/derivations/IMAGE_REGISTRATION.md`, “Registration Is Not Geometric Correction”; `docs/GEOMETRY.md`, Geometry Principle 4
- **Description:** The research derivation correctly prohibits choosing a transformation solely to force three points to agree, but no independent registration protocol or test exists.
- **Why it matters:** Three non-collinear points can determine a fitting transformation, so unconstrained registration can erase the measured difference.
- **Recommended correction:** Develop controlled registration experiments using known frame changes and deliberately nonmatching projections.

### Research 4 — Match evaluation and measurement uncertainty

- **File and section:** `docs/DEFINITIONS.md`, Definition 7 — Projection Match; `docs/USE_CASES.md`, Proposed Validation; `docs/VALIDATION.md`
- **Description:** Exact and practical matching are distinguished, but no TPS error metric, uncertainty budget, or repeatability study exists.
- **Why it matters:** A practical match cannot be interpreted or compared across setups without documented measurement conditions.
- **Recommended correction:** Use repeatability and reproducibility studies to characterize measurement behavior. Keep acceptance tolerances user- or operation-specific unless later approved.

### Research 5 — Projection ambiguity statement

- **File and section:** `docs/GEOMETRY.md`, Geometry Principle 3; `research/VERIFICATION_REPORT.md`
- **Description:** The uniform-scaling example supports non-uniqueness under an ideal model, but the full scope of three-point ambiguity under varying constraints remains only partially supported.
- **Why it matters:** The statement must not be broadened into a general camera-reconstruction theorem.
- **Recommended correction:** Retain the current scope and develop a formal derivation limited to the stated assumptions.

### Editorial 1 — Repeated scope exclusions

- **File and section:** `docs/OBSERVATIONS.md`, Observation 6; `docs/DEFINITIONS.md`, Definitions 5–7; `docs/GEOMETRY.md`, Principles 1–4; `docs/CONSTRAINTS.md`
- **Description:** Camera-pose, calibration, and complete-scene exclusions recur throughout the documents.
- **Why it matters:** The repetition is protective but makes the specification longer and can obscure the normative concepts.
- **Recommended correction:** Keep one canonical scope statement in `SPECIFICATION.md` and use focused cross-references elsewhere.

### Editorial 2 — Mathematical content is split between specification and research

- **File and section:** `SPECIFICATION.md`, “Mathematical Formulation”; `docs/GEOMETRY.md`; `research/derivations/`
- **Description:** The specification says mathematical formulation is reserved, while it now contains an approved calculation and geometry principles supported by research derivations.
- **Why it matters:** Readers may not know which equations are normative, provisional, or explanatory.
- **Recommended correction:** Clarify the relationship between approved mathematical conventions and research derivations without adding new mathematics.

### Editorial 3 — Research derivation notation is not consistently typeset

- **File and section:** `research/derivations/PHYSICAL_IMAGE_TRIANGLES.md`; `research/derivations/IMAGE_REGISTRATION.md`
- **Description:** Some inline mathematical notation appears as parenthesized plain text rather than consistently formatted mathematical notation.
- **Why it matters:** It reduces readability and makes independent checking harder, especially in the derivations.
- **Recommended correction:** Normalize notation in research documents only; do not alter approved specification wording.

## Completeness Assessment

### Complete enough for academic paper framing

- Purpose and scope are clear.
- The physical point, image point, correspondence, projection, reference, and match vocabulary exists.
- Camera reconstruction is explicitly excluded as the TPS objective.
- The reference contents and Working Focal Length convention are recorded.
- Research derivations identify assumptions and limitations.

### Remaining limitations

- Practical matching has no common error or uncertainty description.
- Reference validity and failure conditions remain incomplete.
- Working Focal Length has no validated real-lens applicability boundary.

## Recommended Correction Order

1. Clarify terminology for equivalence, exact match, practical match, and closest practical match.
2. Run registration, repeatability, and Working Focal Length experiments.
3. Consolidate repeated scope language after the technical distinctions stabilize.

No new requirements are introduced by this review.

==================================================
SOURCE: research/BIBLIOGRAPHY.md
==================================================
# TPS Research Bibliography

This bibliography records sources relevant to TPS research. It distinguishes bibliographic identification from review of relevant source content.

Verification status:

- **Identified:** A bibliographic record was located.
- **Examined:** Relevant source content was reviewed.
- **Verified:** A specific claim was checked against the reviewed source content.

## Perspective Projection and Camera Geometry

### OpenCV — *Perspective-n-Point (PnP) pose computation*, version 4.10.0

- **Author or organization:** OpenCV
- **Publication year:** Documentation generated 2024; version 4.10.0
- **Publisher or institution:** Open Source Computer Vision
- **Stable URL:** https://docs.opencv.org/4.10.0/d5/d1f/calib3d_solvePnP.html
- **Access status:** Open
- **Relevant subject:** P3P, PnP, 3D–2D correspondences, reprojection error, camera pose, and multiple solutions
- **Verification status:** Examined; directly relevant. The documentation states that `solveP3P()` uses exactly three correspondences and may return up to four solutions. It is pose-estimation prior art, not TPS.

### OpenCV — *Perspective-n-Point (PnP) pose computation*

- **Author or organization:** OpenCV
- **Publication year:** Documentation version 4.8.0; page accessed during this review
- **Publisher or institution:** Open Source Computer Vision
- **Stable URL:** https://docs.opencv.org/4.8.0/d5/d1f/calib3d_solvePnP.html
- **Access status:** Open
- **Relevant subject:** 3D object points, corresponding 2D image projections, camera intrinsics, distortion, pose, and reprojection error
- **Verification status:** Examined; directly relevant to the correspondence and camera-pose prior art; not a TPS specification

### OpenCV — *Camera Calibration*

- **Author or organization:** OpenCV
- **Publication year:** Documentation version 4.11.0; page accessed during this review
- **Publisher or institution:** Open Source Computer Vision
- **Stable URL:** https://docs.opencv.org/4.11.0/dc/dbb/tutorial_py_calibration.html
- **Access status:** Open
- **Relevant subject:** Object points, image points, calibration patterns, intrinsic and extrinsic parameters, distortion, and image-size-dependent calibration
- **Verification status:** Examined; directly relevant to calibration prior art; not a TPS requirement

### Hartley and Zisserman — *Multiple View Geometry in Computer Vision*

- **Author:** Richard Hartley and Andrew Zisserman
- **Publication year:** 2000; second edition 2004
- **Publisher or institution:** Cambridge University Press; author-hosted Visual Geometry Group, University of Oxford
- **Stable URL:** https://robots.ox.ac.uk/~vgg/hzbook/hzbook1.html
- **Access status:** Open access to bibliographic page and selected chapters; book access varies
- **Relevant subject:** Projective geometry, camera projection, image correspondence, and multiple-view geometry
- **Verification status:** Examined; not used here as sole verification of a specific TPS claim

### MIT — *Foundations of Computer Vision, Chapter 5: Imaging*

- **Author or organization:** Massachusetts Institute of Technology
- **Publication year:** Not stated on the reviewed page
- **Publisher or institution:** MIT
- **Stable URL:** https://visionbook.mit.edu/imaging.html
- **Access status:** Open
- **Relevant subject:** Pinhole and perspective projection, 3D-to-2D mapping, image coordinates, depth, and focal length
- **Verification status:** Examined and verified for the general perspective-projection, depth, and image-coordinate claims cited in the evidence map; not verification of TPS-specific behavior

## Triangle Geometry and Similarity

### OpenStax — *Contemporary Mathematics, Section 10.3: Triangles*

- **Author or organization:** OpenStax
- **Publication year:** 2021 edition page; exact publication year not relied on here
- **Publisher or institution:** OpenStax, Rice University
- **Stable URL:** https://openstax.org/books/contemporary-mathematics/pages/10-3-triangles
- **Access status:** Open
- **Relevant subject:** Noncollinear points forming a triangle and triangle similarity by corresponding proportions
- **Verification status:** Examined and verified for the basic triangle-formation and similarity statements cited in the evidence map; not verification of TPS-specific triangle requirements

## Camera Optics and Focal Length

### Edmund Optics — *Understanding Focal Length and Field of View*

- **Author or organization:** Edmund Optics
- **Publication year:** Not stated on the reviewed page
- **Publisher or institution:** Edmund Optics technical resource
- **Stable URL:** https://www.edmundoptics.com/knowledge-center/application-notes/imaging/understanding-focal-length-and-field-of-view
- **Access status:** Open
- **Relevant subject:** Focal length, field of view, working distance, sensor size, and practical optical limitations
- **Verification status:** Examined and verified for the general focal-length and field-of-view relationship; not verification of the TPS Working Focal Length, which remains TPS-specific

## Image Coordinate Registration

### Brown — *A Survey of Image Registration Techniques*

- **Author:** Lisa Gottesfeld Brown
- **Publication year:** 1992
- **Publisher or institution:** ACM Computing Surveys, 24(4), 325–376; Columbia University affiliation listed in the record
- **DOI:** https://doi.org/10.1145/146370.146374
- **Access status:** Unknown / access to the full article was not confirmed
- **Relevant subject:** Registration of images acquired at different times, viewpoints, and sensors
- **Verification status:** Identified from the bibliographic record; full relevant content was not accessible and no claim is verified from it

## Visual Effects and Camera Matching

### Radke — *Computer Vision for Visual Effects*

- **Author:** Richard J. Radke
- **Publication year:** 2012
- **Publisher or institution:** Cambridge University Press
- **Stable URL:** https://www.cambridge.org/core/product/identifier/CBO9781139019682A034/type/BOOK_PART
- **Access status:** Open chapter record and summary; full book access varies
- **Relevant subject:** Feature matching, correspondence, tracking, and matchmoving for visual effects
- **Verification status:** Examined at the publisher chapter record; directly relevant for scope comparison, but not a verified source for a three-point TPS method

## Stop-Motion and Overlay Practice

### Dragonframe — *Using Dragonframe 2025*

- **Author or organization:** DZED Systems / Dragonframe
- **Publication year:** 2025 manual
- **Publisher or institution:** Dragonframe
- **Stable URL:** https://www.dragonframe.com/download/Using%20Dragonframe%202025.pdf
- **Access status:** Restricted by large-PDF retrieval during this review; indexed manual text was accessible
- **Relevant subject:** Onionskin transparency, Live View comparison, difference mode, and frame echo
- **Verification status:** Examined in indexed manual excerpts; directly relevant to overlay practice. Full manual review was not completed, so no broader claim is made.

### Dragonframe — *Camera Support*

- **Author or organization:** DZED Systems / Dragonframe
- **Publication year:** Current support page accessed during this review
- **Publisher or institution:** Dragonframe
- **Stable URL:** https://www.dragonframe.com/camera-support/
- **Access status:** Open
- **Relevant subject:** Low-resolution video assist, high-quality capture, tandem image sequences, and camera-specific live-view dimensions
- **Verification status:** Examined; directly relevant to coordinate-frame and resolution distinctions. It does not define TPS.

## Computer Vision Textbooks

### Szeliski — *Computer Vision: Algorithms and Applications*, Second Edition

- **Author:** Richard Szeliski
- **Publication year:** 2022
- **Publisher or institution:** Springer; author-hosted book site
- **Stable URL:** https://szeliski.org/Book/
- **Access status:** Open bibliographic page; electronic text available through the author's download process
- **Relevant subject:** Computer vision, camera geometry, image matching, and registration
- **Verification status:** Examined at the official book page; specific relevant chapters were not examined in this pass and are not used as verified evidence.

## VFX Camera Lineup and Survey

### Science-D-Visions — *3DEqualizer Technical Specification*

- **Author or organization:** Science-D-Visions
- **Publication year:** Not stated on the reviewed page
- **Publisher or institution:** Science-D-Visions
- **Stable URL:** https://www.3dequalizer.com/?item=tech_spec&site=start
- **Access status:** Open
- **Relevant subject:** Lineup Controls, survey points, distance and plane constraints, camera/lens parameters, manual and automatic camera consistency, and focal-length calculation
- **Verification status:** Examined; directly relevant to TPS prior art. It documents a broader software camera-lineup and matchmoving system, not the TPS specification.

### Mike Seymour — “3DEqualizer – German precision where VFX needs it”

- **Author:** Mike Seymour; interview with Rolf Schneider
- **Publication year:** 2014
- **Publisher or institution:** fxguide
- **Stable URL:** https://www.fxguide.com/quicktakes/3dequalizer-german-precision-where-vfx-needs-it/
- **Access status:** Open
- **Relevant subject:** Survey data, camera tracking, low-parallax shots, lens distortion, scale, and production camera matching
- **Verification status:** Examined; directly relevant for comparison with VFX survey and camera-tracking practice. It does not establish TPS.

## Visual Effects Society and Production Data

### Visual Effects Society — *The VES Handbook of Visual Effects: Industry Standard VFX Practices and Procedures*, Second Edition

- **Editors:** Jeffrey A. Okun and Susan Zwerman
- **Publication year:** 2014
- **Publisher or institution:** Visual Effects Society / Focal Press
- **Stable URL:** https://vesglobal.org/wp-content/uploads/2014/09/ves_handbook_release1.pdf
- **Access status:** The official release announcement is open; the complete handbook chapters were not accessible for this review
- **Relevant subject:** VFX production practices, camera work, surveying, tracking, lens data, and production procedures
- **Verification status:** Identified and examined through the official release announcement; handbook-specific chapters, authors, and page numbers were not verified

### Visual Effects Society — *On-Set VFX Data Collection and Usage Guide*

- **Author or organization:** Visual Effects Society Technology Committee; lead author Sheena Duggal, with Sam Richards, Jim Geduldick, and Jake Morrison; technical support by Jean-Francois Panisset
- **Publication year:** 2026 announcement and guide release
- **Publisher or institution:** Visual Effects Society
- **Stable URL:** https://vesglobal.org/press-releases/on-set-vfx-data-collection-and-usage-guide/
- **Access status:** Official announcement open; linked guide identified but its detailed contents were not examined in this pass
- **Relevant subject:** On-set data sets, capture workflows, stakeholders, handoffs, and production-data interoperability
- **Verification status:** Examined for the existence, purpose, authorship, and stated scope of the guide; no detailed camera-field claim is verified from the announcement

## VFX Interoperability

### VFX Reference Platform — Official Project

- **Author or organization:** VFX Reference Platform, in collaboration with the Visual Effects Society Technology Committee
- **Publication year:** Annual platform; current status page examined during this review
- **Publisher or institution:** VFX Reference Platform / Academy Software Foundation ecosystem
- **Stable URL:** https://vfxplatform.com/ and https://vfxplatform.com/about/
- **Access status:** Open
- **Relevant subject:** Tool and library versions, build targets, software interoperability, compatibility, and annual version management
- **Verification status:** Examined and verified for its stated interoperability scope; it is not a camera-geometry or camera-matching specification and does not establish TPS conformance or endorsement

## Interdisciplinary Prior Art

### Heritage and Repeat Photography: Techniques, Management, Applications, and Publications

- **Author:** Review article; author metadata recorded by the journal
- **Publication year:** 2022
- **Publisher or institution:** *Heritage*, MDPI, 5(4)
- **DOI:** https://doi.org/10.3390/heritage5040220
- **Access status:** Open
- **Relevant subject:** Rephotography, locating historical camera positions, image registration, and heritage comparison
- **Verification status:** Examined and verified for the general rephotography objective and registration challenges; not a TPS method

### Chow — “Photogrammetric Space Resection”

- **Author:** Carl Chow
- **Publication year:** 1950
- **Publisher or institution:** *Transactions of the American Society of Civil Engineers*, 115(1), pp. 235–259
- **DOI:** https://doi.org/10.1061/TACEAT.0006318
- **Access status:** Abstract and bibliographic record open; full article access varies
- **Relevant subject:** Three ground control points, image points, and camera exposure-station resection
- **Verification status:** Examined abstract and record; verified for the stated resection relationship, not for TPS's non-reconstruction objective

### Open AGH — *Basics of Photogrammetry*

- **Author or organization:** Open AGH educational platform
- **Publication year:** Not stated on the reviewed page
- **Publisher or institution:** AGH University of Science and Technology educational resource
- **Stable URL:** https://epodreczniki.open.agh.edu.pl/handbook/4795/module/4812/reader
- **Access status:** Open
- **Relevant subject:** Collinearity, perspective center, image points, and exterior orientation
- **Verification status:** Examined and verified for the general photogrammetric principles cited in the interdisciplinary review

### Beroiz, Cabral, and Sanchez — “Astroalign: A Python module for astronomical image registration”

- **Authors:** M. Beroiz, J. B. Cabral, B. Sanchez
- **Publication year:** 2020
- **Publisher or institution:** *Astronomy and Computing*, 32, article 100384
- **DOI:** https://doi.org/10.1016/j.ascom.2020.100384
- **Access status:** Abstract open; full article access varies
- **Relevant subject:** Matching three-point star asterisms and estimating image transformations without WCS information
- **Verification status:** Examined abstract and bibliographic record; verified for the three-point asterism registration claim

### Mohammadian et al. — “High accuracy, fiducial marker-based image registration of correlative microscopy images”

- **Authors:** Sajjad Mohammadian et al.
- **Publication year:** 2019
- **Publisher or institution:** *Scientific Reports*, 9, 3211
- **DOI:** https://doi.org/10.1038/s41598-019-40098-4
- **Access status:** Open
- **Relevant subject:** Fiducial markers, multimodal image registration, composed transformations, and accuracy assessment
- **Verification status:** Examined full open article; verified for the stated fiducial-registration method and scope

### Masci et al. — “Image registration and astrometric calibration for the Spitzer Space Telescope”

- **Authors:** F. Masci et al.
- **Publication year:** 2004
- **Publisher or institution:** *Publications of the Astronomical Society of the Pacific*, 116
- **Stable URL:** https://web.ipac.caltech.edu/staff/fmasci/home/sirtfwork/paper7R.pdf
- **Access status:** Open PDF located; full relevant text not examined in this pass
- **Relevant subject:** Astronomical image registration and reference-source alignment
- **Verification status:** Identified; specific claims remain unverified

### OpenCV — *Basic concepts of the homography explained with code*

- **Author or organization:** OpenCV
- **Publication year:** Documentation for OpenCV 3.0+
- **Publisher or institution:** Open Source Computer Vision
- **Stable URL:** https://docs.opencv.org/4.5.1/d9/dab/tutorial_homography.html
- **Access status:** Open
- **Relevant subject:** Planar homography and projective transformation between planes
- **Verification status:** Examined and verified for the general homography relationship; not a TPS requirement

### Australian Film Television & Radio School — *Stop Motion*

- **Author or organization:** Australian Film Television & Radio School
- **Publication year:** 2021 document version shown in the URL; exact publication date not relied on here
- **Publisher or institution:** AFTRS Media Lab
- **Stable URL:** https://medialab.aftrs.edu.au/wp-content/uploads/2021/07/AFTRS16_StopMotion.2021.pdf
- **Access status:** Open
- **Relevant subject:** Onion-skin overlays and aligning successive stop-motion frames
- **Verification status:** Examined, pp. 14–15; directly relevant to overlay practice, not camera-view recovery by three physical points

### Gasek — “Objects, People, and Places”

- **Author:** Tom Gasek
- **Publication year:** 2015
- **Publisher or institution:** Bloomsbury Visual Arts, in *Frame-by-Frame Stop Motion: The Guide to Non-Puppet Photographic Animation*
- **Stable URL:** https://www.bloomsburyvisualarts.com/app/downloadpdf?docIdS=b-9781315155166
- **Access status:** Restricted / chapter PDF accessible through publisher delivery during review
- **Relevant subject:** Camera stability, frame-grabber onion skinning, camera-bump recovery, and placement registration
- **Verification status:** Examined, Chapter 6, pp. 104–105; directly relevant to practical overlay-guided recovery, not a three-point TPS method

## Measurement Uncertainty and Repeatability

### Taylor and Kuyatt — *Guidelines for Evaluating and Expressing the Uncertainty of NIST Measurement Results*, NIST Technical Note 1297

- **Authors:** Barry N. Taylor and Chris E. Kuyatt
- **Publication year:** 1994
- **Publisher or institution:** National Institute of Standards and Technology
- **Stable URL:** https://www.nist.gov/pml/nist-technical-note-1297
- **Access status:** Open
- **Relevant subject:** Measurement uncertainty, repeatability, reproducibility, uncertainty components, and reporting
- **Verification status:** Examined and verified for the repeatability and reproducibility terminology cited in the evidence map

### JCGM — *Evaluation of Measurement Data — Guide to the Expression of Uncertainty in Measurement (JCGM 100:2008)*

- **Author or organization:** Joint Committee for Guides in Metrology
- **Publication year:** 2008
- **Publisher or institution:** JCGM / BIPM and member organizations
- **DOI:** https://doi.org/10.59161/JCGM100-2008E
- **Stable URL:** https://www.bipm.org/documents/20126/2071204/JCGM_100_2008_E.pdf
- **Access status:** Open for online access; copyright restrictions apply
- **Relevant subject:** Evaluation and expression of measurement uncertainty
- **Verification status:** Examined at the official bibliographic and access page; no TPS-specific claim is marked verified from this source in this draft

==================================================
SOURCE: research/EVIDENCE_MAP.md
==================================================
# TPS Evidence Map

This map relates current TPS statements to external evidence without treating external sources as proof of TPS-specific operational requirements.

Status labels:

- **Established mathematics:** General mathematical content supported by an examined source.
- **Established optical principle:** General camera or optics content supported by an examined source.
- **Established production practice:** General practice supported by an examined source.
- **TPS-specific hypothesis:** A TPS-specific claim requiring dedicated derivation or experiment.

## Evidence Map

| TPS claim | TPS location | Classification | Relevant source | Evidence status | Scope note |
|---|---|---|---|---|---|
| Three distinct noncollinear points form a triangle. | `docs/OBSERVATIONS.md:9–27`; Definition 1 in `docs/DEFINITIONS.md:9–43` | Established mathematics | OpenStax, *Contemporary Mathematics*, §10.3, “Identifying Triangles” | Verified | The source directly states the noncollinear-point construction; it does not establish any TPS operation. |
| Uniform scaling preserves corresponding side-length ratios and internal angles. | Invariant 2, `docs/INVARIANTS.md:60–97` | Established mathematics | OpenStax, *Contemporary Mathematics*, §10.3, similarity worked example | Verified | The source supports the general similarity relationship; it does not establish that TPS universally requires similar replacement triangles. |
| A physical point can be represented at a location in a two-dimensional image. | Observations 2–3, `docs/OBSERVATIONS.md:29–96`; Definitions 1–2, `docs/DEFINITIONS.md:9–83` | Established optical principle | MIT, *Foundations of Computer Vision*, §5.3.1, “Image Formation by Perspective Projection” | Verified | The source directly describes 3D points projecting to 2D image locations under a pinhole model. |
| Perspective projection depends on point depth and camera parameters. | Geometry Principle 2, `docs/GEOMETRY.md:66–133` | Established optical principle | MIT, *Foundations of Computer Vision*, §5.3.1 | Verified | Supports the ideal perspective model and depth dependence; it does not validate every real camera system. |
| Perspective projection does not generally preserve physical triangle shape. | Geometry Principle 1, `docs/GEOMETRY.md:9–64`; `research/derivations/PHYSICAL_IMAGE_TRIANGLES.md` | Established optical principle | MIT, §5.3.1; OpenStax, §10.3 | Partially supported | The derivation provides checkable calculations under an ideal pinhole model; formal promotion still requires review and validation. |
| Focal length affects field of view and image formation. | Observation 4, `docs/OBSERVATIONS.md:98–137`; Definition 4, `docs/DEFINITIONS.md:128–187` | Established optical principle | Edmund Optics, “Focal Length” and “Field of View” sections; MIT, §5.3.1 | Verified | Supports the general optical principle; it does not establish a Working Focal Length formula. |
| The proposed TPS Working Focal Length relationship is exact under an ideal equal-depth, horizontal A–B pinhole model. | Definition 6, `docs/DEFINITIONS.md:297–315`; `research/derivations/WORKING_FOCAL_LENGTH.md` | TPS-specific derivation based on established optics | MIT, §5.3.1; Edmund Optics, “Focal Length” and “Field of View” sections | Partially supported | The derivation verifies dimensional consistency and numerical behavior under explicit ideal assumptions. Sensor-plane distance, finite focus, unequal depths, tilt, and lens effects prevent treating it as a general exact real-lens formula. |
| Image coordinates require a defined and consistently registered frame for comparison. | Definition 6, `docs/DEFINITIONS.md:282–319`; Geometry Principle 4, `docs/GEOMETRY.md:210–300`; `research/derivations/IMAGE_REGISTRATION.md` | Established production practice / TPS operational requirement | Brown, *A Survey of Image Registration Techniques*, abstract record only; MIT, §5.3.1 | Partially supported | The derivation defines declared frame transformations and their limits; the TPS registration interpretation and practical failure modes remain unvalidated. |
| Repeatability and reproducibility require stated measurement conditions. | Definition 7, `docs/DEFINITIONS.md:321–389`; UC-001, `docs/USE_CASES.md:50–60` | Established measurement practice | NIST TN 1297, Appendix D1.1.2–D1.1.3 | Verified | NIST directly defines repeatability and reproducibility in relation to measurement conditions; it does not establish TPS tolerances. |
| A TPS reference contains points, correspondence, image-frame information, triangle measurements, focus distance, and Working Focal Length. | `SPECIFICATION.md:26–32`; Definition 6, `docs/DEFINITIONS.md:250–319` | TPS-specific requirement | No external source asserted as authority | Unverified | This is an approved TPS requirement. Its reproducibility and adequacy require TPS research and validation. |
| A projection match does not uniquely recover camera pose or the complete camera configuration. | Observation 6, `docs/OBSERVATIONS.md:176–211`; Geometry Principle 3, `docs/GEOMETRY.md:135–208`; UC-001, `docs/USE_CASES.md:39–48` | TPS-specific geometric claim | Hartley and Zisserman, author-hosted book record and selected material; MIT, §5.3.1 | Partially supported | The sources establish perspective-camera geometry and multiple-view context, but the exact three-point ambiguity claim requires a dedicated derivation or experiment. |
| UC-001 can be tested by recording, moving or removing the camera, attempting recovery, and measuring correspondence errors. | `docs/USE_CASES.md:50–60` | TPS-specific proposed experiment | NIST TN 1297 for measurement terminology | Needs experiment | No experimental result is claimed; the proposed protocol must be executed and documented before performance claims are made. |
| 3D physical points and corresponding image points are established inputs to camera-pose estimation. | `SPECIFICATION.md:26–80`; Definition 6 in `docs/DEFINITIONS.md` | Established computer-vision practice | OpenCV, “Perspective-n-Point (PnP) pose computation,” official documentation | Verified | The source directly describes object points, corresponding image projections, intrinsics, distortion, and reprojection-error pose estimation. It supports prior art, not TPS's non-solving objective. |
| Camera calibration commonly uses object points, image points, image size, and multiple views to estimate camera parameters. | `SPECIFICATION.md:26–80`; UC-001 | Established computer-vision practice | OpenCV, “Camera Calibration,” official documentation | Verified | The source describes calibration-pattern points and estimation of intrinsic/extrinsic parameters. TPS does not prescribe calibration. |
| Visual-effects workflows use image feature matching and tracking to relate images and estimate camera motion. | `docs/USE_CASES.md`; Geometry Principle 3 | Established production/computer-vision practice | Richard J. Radke, *Computer Vision for Visual Effects*, Chapters 4 and 6, publisher chapter record | Partially supported | The publisher record was examined and identifies feature matching, tracking, and matchmoving. Full chapter content was not used to verify a specific algorithm. |
| Semi-transparent overlays can help users align successive stop-motion frames and recover from camera bumps. | `docs/USE_CASES.md`, Recovery; `research/derivations/IMAGE_REGISTRATION.md` | Established production practice | AFTRS, *Stop Motion*, pp. 14–15; Gasek, Chapter 6, pp. 104–105 | Verified | These sources support overlay-guided visual alignment and camera-bump recovery practice, not TPS's exact three-point reference model. |
| TPS's combination of three correspondences, registered reference comparison, and camera-view matching is a distinct practical contribution. | TPS kernel and UC-001 | TPS-specific hypothesis | No source establishes this combination as original | Unverified / needs broader prior-art search | Existing PnP, matchmoving, registration, and onion-skin practices substantially overlap individual elements. No originality claim is made. |
| Exactly three 3D–2D correspondences can define a P3P pose problem with multiple possible solutions. | `SPECIFICATION.md:26–80`; Geometry Principle 3 | Established computer-vision method | OpenCV 4.10, “Perspective-n-Point (PnP) pose computation,” P3P section | Verified | The documentation states that `solveP3P()` uses exactly three correspondences and can return up to four solutions. This supports pose ambiguity and prior art, not a TPS recovery procedure. |
| Stop-motion software provides live/reference overlay and line-up tools. | `SPECIFICATION.md:26–80`; `docs/USE_CASES.md` | Established production practice | Dragonframe, *Using Dragonframe 2025*; Dragonframe Camera Support | Partially supported | Indexed manual excerpts support onionskin and Live View comparison; the camera-support page directly supports separate video-assist and high-resolution capture sequences. Full manual retrieval was limited. |
| Video-assist and final captures may have different image dimensions and therefore require explicit frame interpretation for comparison. | Definition 6; Geometry Principle 4 | Established production fact / TPS interpretation | Dragonframe Camera Support | Verified | The support page documents low-resolution video assist, high-quality capture, and camera-specific live-view dimensions. It does not prescribe TPS coordinate registration. |
| Szeliski's textbook is an authoritative source for relevant computer-vision background. | Research derivations and evidence map | Bibliographic source | Richard Szeliski, *Computer Vision: Algorithms and Applications*, 2nd ed. | Identified / not verified for specific claims | The official book page was examined, but relevant chapter text was not examined in this pass. |
| Survey points and physical geometry can be used to align a virtual camera to image footage. | `SPECIFICATION.md`; `docs/USE_CASES.md` | Established VFX practice | Science-D-Visions, 3DEqualizer Technical Specification; FXguide interview | Verified | 3DEqualizer documents manual and automatic lineup to surveyed geometry, survey point constraints, and camera/lens parameter adjustment. This is virtual camera lineup and matchmoving, not physical camera-view recovery. |
| 3DEqualizer substantially overlaps TPS's physical/image correspondence and camera alignment concepts. | TPS kernel and UC-001 | Prior-art interpretation | Science-D-Visions 3DEqualizer sources | Partially supported | The overlap is clear at the concept level. The reviewed materials do not document the complete TPS reference record or an implementation-independent physical overlay workflow. |
| No examined source establishes the complete TPS combination as original. | TPS kernel, Definition 6, UC-001 | TPS-specific originality hypothesis | OpenCV, Dragonframe, Szeliski, 3DEqualizer, FXguide | Unverified | The sources show substantial precedents for individual elements. Absence of a complete duplicate in this pass is not evidence of originality. |
| VFX production practice values systematic capture and handoff of on-set data. | `SPECIFICATION.md`; `docs/USE_CASES.md` | Established production practice | VES, *On-Set VFX Data Collection and Usage Guide* announcement | Partially supported | The official announcement establishes the guide's purpose, data-collection scope, stakeholders, and handoff goals. Its detailed camera-field contents were not examined. |
| The VES Handbook represents established VFX practices and procedures, including broad production coverage. | Prior-art review only | Established production context | VES official second-edition release announcement | Identified / not verified for specific claims | The announcement confirms the 2014 second edition, editors, and broad VFX scope. The handbook's relevant camera-survey and lineup chapters were inaccessible, so no page-level claim is made. |
| VFX software interoperability is addressed through shared tool and library version targets. | Implementation-independent TPS context | Established interoperability practice | Official VFX Reference Platform home and About pages | Verified | The platform explicitly defines tool/library versions to minimize incompatibilities and support integrated pipelines. It does not define camera geometry, image registration, or TPS reference semantics. |
| TPS implementations can remain portable without adopting a specific VFX platform version. | TPS implementation independence | TPS interpretation based on interoperability evidence | VFX Reference Platform official pages | Partially supported | The platform's scope is software/library compatibility. Portability is a TPS design implication, not a platform requirement or endorsement. |
| No verified VES or VFX Reference Platform publication formalizes the complete TPS workflow. | TPS kernel and UC-001 | TPS-specific prior-art finding | VES and VFX Reference Platform sources examined in this pass | Unverified / limited search | The VES handbook chapters and linked on-set guide details were not fully accessible. This finding must not be treated as evidence of originality. |
| Repeat photography seeks to relocate an earlier camera viewpoint and compare a new image with the earlier image. | `docs/USE_CASES.md`; Geometry Principle 4 | Established interdisciplinary practice | *Heritage and Repeat Photography*, *Heritage* 5(4), 2022 | Verified | The review supports the view-reproduction and registration objective. It does not establish TPS's three-point reference record or calculations. |
| Three known physical control points and their image points can support photogrammetric space resection. | `SPECIFICATION.md`; Geometry Principles 2–3 | Established photogrammetric method | Carl Chow, “Photogrammetric Space Resection,” 1950 | Verified | This is a close three-point physical/image precedent, but it reconstructs camera pose, unlike TPS's stated objective. |
| Perspective-center, object-point, and image-point collinearity underlies photogrammetric orientation. | `docs/GEOMETRY.md`; research derivations | Established photogrammetric mathematics | Open AGH, *Basics of Photogrammetry* | Verified | Supports the geometric foundation, not the TPS workflow. |
| Three-point image configurations can be matched to estimate an image transformation. | Geometry Principle 4; `research/derivations/IMAGE_REGISTRATION.md` | Established image-registration method | Beroiz, Cabral, and Sanchez, “Astroalign,” 2020 | Verified | Astroalign uses three-point star asterisms for registration. It does not use physical scene points or TPS calculations. |
| Fiducial markers establish correspondence and transformations between different imaging modalities. | Definition 6; Geometry Principle 4 | Established registration practice | Mohammadian et al., *Scientific Reports* 9, 3211, 2019 | Verified | Supports portable markers and registered overlays, not camera-view recovery. |
| Planar homography is a projective transformation between planes. | Geometry Principle 4; `research/derivations/IMAGE_REGISTRATION.md` | Established projective geometry | OpenCV homography tutorial | Verified | A full homography is distinct from TPS comparison and must not be used to force three nonmatching points into agreement. |
| Astronomy and microscopy use common reference points, fiducials, and coordinate frames for image comparison. | Definition 6; Geometry Principle 4 | Established registration practice | Masci et al. 2004; Mohammadian et al. 2019 | Partially supported | The microscopy source was examined; the Masci PDF was located but not fully examined in this pass. |
| No examined interdisciplinary source is clearly equivalent to the complete TPS workflow. | TPS kernel and UC-001 | TPS-specific prior-art finding | Rephotography, resection, Astroalign, fiducial registration, and homography sources | Unverified / limited search | Sources provide substantial precedents for individual elements. Absence of a complete duplicate is not evidence of originality. |

## Evidence Boundaries

The external sources support general mathematics, optics, image-registration context, and measurement terminology. They do not by themselves validate the TPS kernel, TPS reference contents, Working Focal Length, projection-match criteria, or UC-001 outcomes.

The TPS-specific requirements remain subject to research, derivation, and experiments in this repository.

==================================================
SOURCE: research/VERIFICATION_REPORT.md
==================================================
# TPS Research Verification Report

## Scope

This report reviews the claims mapped in [EVIDENCE_MAP.md](EVIDENCE_MAP.md) against the sources listed in [BIBLIOGRAPHY.md](BIBLIOGRAPHY.md). It does not alter approved TPS wording and does not treat general camera geometry as validation of TPS performance.

## Claim Counts

The evidence map contains 11 examined claim entries:

- **Verified:** 6
- **Partially supported:** 2
- **Unverified:** 2
- **Needs experiment:** 1

These counts describe the current evidence map, not the truth of the TPS-specific claims.

## 1. Verified Mathematical Foundations

### Triangle formation

TPS statement: “Three distinct noncollinear points form a triangle.”

Reference: OpenStax, *Contemporary Mathematics*, §10.3, “Identifying Triangles.” The reviewed section directly describes joining three noncollinear points with line segments to produce a triangle.

TPS references: `docs/OBSERVATIONS.md:9–27`; `docs/DEFINITIONS.md:9–43`.

Status: **Verified** as an established geometric fact. This does not validate a TPS procedure.

### Triangle similarity

TPS statement: “When a physical triangle is uniformly scaled, the ratios of its corresponding side lengths and its internal angles remain unchanged.”

Reference: OpenStax, *Contemporary Mathematics*, §10.3, similarity worked example. The reviewed material supports corresponding side proportions and similarity.

TPS reference: `docs/INVARIANTS.md:60–97`.

Status: **Verified** as general triangle similarity. The source does not establish that TPS universally requires similar replacement triangles.

## 2. Verified Optical Principles

### 3D-to-2D perspective projection

TPS statement: “The camera represents visible physical points as locations in a two-dimensional image coordinate system.”

Reference: MIT, *Foundations of Computer Vision*, §5.3.1, “Image Formation by Perspective Projection.” The reviewed section describes a pinhole camera projecting 3D coordinates to 2D projection-plane positions and relates camera coordinates to image coordinates.

TPS references: `docs/OBSERVATIONS.md:61–96`; `docs/DEFINITIONS.md:45–83`.

Status: **Verified** for the ideal pinhole/perspective model. Real-camera behavior and TPS performance remain separate questions.

### Depth and perspective

TPS statement: “Under an ideal perspective camera model, the projected position of a physical point depends on its position relative to the camera, including its depth along the camera's viewing direction.”

Reference: MIT, §5.3.1. The reviewed section explains depth-dependent perspective scaling and distinguishes perspective from orthographic projection.

TPS reference: `docs/GEOMETRY.md:66–133`.

Status: **Verified** for the ideal model stated by TPS.

### Focal length and field of view

TPS statement: “Changing a camera's focal length ... can change the projected image coordinates.”

Reference: Edmund Optics, “Focal Length” and “Field of View” sections; MIT, §5.3.1.

TPS references: `docs/OBSERVATIONS.md:98–137`; `docs/DEFINITIONS.md:128–187`.

Status: **Verified** for the general optical relationship. This does not verify a TPS Working Focal Length calculation.

## 3. Partially Supported Claims

### Physical and image triangles need not be similar

TPS statement: “Under perspective projection, the image of three non-collinear physical points does not generally preserve the side-length ratios or internal angles of the physical triangle.”

References: MIT, §5.3.1; OpenStax, §10.3.

TPS reference: `docs/GEOMETRY.md:9–64`.

Status: **Partially supported.** The reviewed sources establish perspective scaling and triangle geometry, but the exact TPS statement should receive a direct derivation in `research/derivations/` before being treated as fully evidenced.

### Projection matching is not camera reconstruction

TPS statement: “A projection match alone does not establish unique camera reconstruction.”

References: Hartley and Zisserman, author-hosted bibliographic and selected material; MIT, §5.3.1.

TPS references: `docs/GEOMETRY.md:135–208`; `docs/OBSERVATIONS.md:176–211`; `docs/USE_CASES.md:39–48`.

Status: **Partially supported.** The sources establish the relevant camera-geometry context, but the exact three-point ambiguity claim requires a TPS-specific derivation or experiment.

## 4. Unsupported or Unverified Claims

### Image registration requirement

TPS statement: “A TPS reference must establish an image coordinate frame ... [and] be registered consistently.”

Reference: Brown’s survey was bibliographically identified, but its full relevant content was not accessible during this review.

TPS references: `docs/DEFINITIONS.md:282–319`; `docs/GEOMETRY.md:210–300`.

Status: **Unverified.** The requirement is approved TPS wording, not externally verified evidence.

### Complete TPS reference contents

TPS statement: A TPS reference preserves points, correspondence, image-frame information, measured triangle geometry, focus distance, and Working Focal Length.

TPS references: `SPECIFICATION.md:26–32`; `docs/DEFINITIONS.md:250–319`.

Status: **Unverified externally.** No reviewed source establishes these as TPS requirements. Their adequacy and reproducibility require original TPS research.

## 5. Claims Requiring Original Experiments

### UC-001 performance

TPS statement: A recorded view can be reproduced after the camera is moved, removed, or replaced, with correspondence errors measured against the reference.

TPS reference: `docs/USE_CASES.md:50–60`.

Status: **Needs experiment.** The document describes a proposed experiment, not a result. The experiment must specify changed conditions and report measurement uncertainty before performance conclusions are drawn.

## 6. Contradictions or Questionable Assumptions

- No direct contradiction was found between the reviewed sources and approved TPS wording.
- Image registration is treated as an approved TPS requirement but remains externally unverified because the relevant source was inaccessible.
- Working Focal Length is a TPS-specific recorded value; the reviewed optics sources do not define or validate it.
- Triangle similarity is correctly conditional in `docs/INVARIANTS.md` and `docs/CONSTRAINTS.md`; it must not be promoted to a universal TPS requirement.
- General projective-geometry literature must not be treated as proof that every TPS reference or UC-001 recovery will succeed.

## 7. Recommended Research Priorities

1. Retrieve and examine an accessible full source on image registration and coordinate-frame registration.
2. Write a derivation for the physical/image triangle claim under the ideal perspective model.
3. Define the Working Focal Length inputs and reproducibility record without yet asserting a formula.
4. Design and run UC-001 repeatability and changed-condition experiments.
5. Record uncertainty, repeatability, and reproducibility conditions for image-point measurements.

No new TPS requirements are introduced by this report.

==================================================
SOURCE: research/PRIOR_ART_REVIEW.md
==================================================
# TPS Prior-Art Review

**Scope:** External literature review supporting Paper 1 of the Three Point System.

**Status:** Research document. It does not modify or add to the TPS specification.

## 1. Research Scope

This review examines established methods involving physical points, image correspondences, camera alignment, view reproduction, image registration, overlays, visual effects, and stop-motion. It does not claim that TPS is novel. The comparison is limited to publicly identifiable methods and sources whose relevant content was examined.

The central question is whether TPS contributes a distinct practical organization of known techniques: recording three identified physical points and their image locations, then using a registered reference to guide a later closest-practical view match without requiring camera solving.

## 2. Search Method

Sources were sought in projective geometry, computer vision, photogrammetry, visual effects, image registration, and stop-motion production. Priority was given to official university, standards, publisher, and software-documentation sources, with open access where available.

Each source is classified as:

- **Identified:** A bibliographic record was located.
- **Examined:** Relevant source content was accessible and reviewed.
- **Directly relevant:** The examined content addresses a TPS concept or a closely related method.
- **Inaccessible:** A record was located, but the relevant full content was not confirmed.

## 3. Established Mathematical Foundations

### Perspective projection and physical/image correspondence

MIT's *Foundations of Computer Vision*, §5.3.1, describes perspective image formation from 3D points to 2D image coordinates. OpenCV's official Perspective-n-Point documentation describes object points, corresponding image projections, camera intrinsics, and reprojection error.

These sources directly support the general relationship between physical points and image points. They do not establish the TPS reference, its three-point operating choice, or the Working Focal Length convention.

### Pose estimation and calibration

OpenCV's `solvePnP` documentation states that pose estimation uses 3D object points and corresponding 2D image projections, together with camera intrinsics and distortion coefficients, to estimate rotation and translation by minimizing reprojection error. OpenCV's calibration tutorial describes obtaining object points and image points from calibration patterns and estimating intrinsic and extrinsic parameters across multiple views.

This is the closest established computational analogue to TPS's point correspondence. It differs fundamentally in objective: PnP and calibration solve for camera or object parameters, while TPS records and compares a three-point view and does not require unique pose recovery.

## 4. Existing Camera-Matching Techniques

Radke's *Computer Vision for Visual Effects*, Chapter 4, explains matching and tracking image features across different perspectives and times; its Chapter 6 is dedicated to matchmoving. The publisher's chapter description identifies feature matching as a basis for relating images and tracking camera motion.

This is directly relevant to the broader camera-view-reproduction problem. Matchmoving generally uses many image features, temporal sequences, and 3D reconstruction or camera-path estimation. TPS is narrower: three identified correspondences, a recorded reference, and manual or practical view matching without requiring a solved camera path.

Perspective-n-point methods are also substantially overlapping prior art when the physical 3D coordinates and camera intrinsics are known. They should not be described as TPS implementations, because their goal is parameter estimation rather than implementation-independent reference matching.

## 5. Image Registration and Overlays

Brown's 1992 survey is a foundational bibliographic source for image registration across different times, viewpoints, and sensors, but the full relevant article was not accessible during this review. It is therefore identified, not examined or verified here.

The TPS research derivation on image registration is consistent with the established distinction between declaring a coordinate transformation and fitting a transformation merely to force three points into agreement. The latter would erase the measured difference TPS intends to compare. This is a TPS interpretation requiring further protocol and experiment, not a claim that TPS invented image registration.

## 6. Stop-Motion and VFX Applications

The Australian Film Television and Radio School stop-motion material, pp. 14–15 of the reviewed PDF, describes an onion-skin effect in which translucent frames are projected over one another so that a user can align successive drawings. This directly supports the use of transparent overlays for practical visual alignment, but it concerns frame-to-frame animation rather than recovery of a camera view from three physical point correspondences.

Gasek's *Frame-by-Frame Stop Motion*, Chapter 6, pp. 104–105 in the examined chapter PDF, describes camera stability, frame-grabber onion skinning, coaxing a bumped camera back into place, and ghosted frames for placement registration. This is a close practical precedent for overlay-guided recovery after camera movement. It does not define TPS's three-point reference contents or its Working Focal Length.

The literature therefore supports overlays and camera stability as established production practices. It does not show that TPS's exact three-point reference procedure is an established named method.

## 7. Historical Precedents

Traditional animation's translucent-paper onion skin and modern stop-motion frame-grabber overlays are historical and contemporary precedents for comparing a current view with a recorded visual reference. The reviewed sources establish the practice at a general level.

The present review did not verify a historical camera-view method using exactly three physical points, explicit A→a/B→b/C→c correspondence, and a sensor-plane reference distance. That absence is not evidence of originality; it identifies a search gap.

## 8. Comparison with TPS

| Existing method | Overlap with TPS | Important difference |
|---|---|---|
| Perspective projection | Physical points map to image points. | General mathematical model, not a recovery workflow. |
| Camera calibration | Uses known physical points and image measurements. | Estimates intrinsics/extrinsics, usually from patterns and multiple views. |
| PnP / pose estimation | Uses corresponding 3D and 2D points. | Solves pose and requires camera-model inputs; TPS does not solve cameras. |
| Image registration | Places image measurements in a common frame. | General registration may estimate transformations; TPS forbids using registration to force a match. |
| Matchmoving | Reproduces or explains camera motion from image evidence. | Typically uses many features, sequences, and camera reconstruction. |
| Onion-skin overlays | Compares a live/current frame with a recorded frame. | Usually frame-to-frame or placement alignment, not a three-point physical/image reference. |

The strongest overlap is conceptual and operational: known correspondences, a registered visual reference, and iterative adjustment to recover a desired view. The strongest difference is scope: TPS intentionally packages a minimal three-point method while excluding camera reconstruction as its objective.

## 9. Potential TPS Contribution

The following may constitute a practical contribution, but are hypotheses rather than established novelty claims:

1. A simple, explicit three-point correspondence record intended for physical, photographic, overlay, or software use.
2. An implementation-independent recovery workflow centered on comparing three registered image locations.
3. A deliberate separation between view matching and camera reconstruction.
4. Preservation of physical triangle measurements and a TPS-specific Working Focal Length record alongside the image correspondence.

The first three items combine established concepts in a constrained workflow. The fourth is TPS-specific in its formulation but remains mathematically approximate and experimentally unvalidated. A formal novelty claim requires a broader patent and academic search, especially in cinematography, optical viewfinders, matchmoving, photogrammetry, and production engineering.

## 10. Research Gaps

- Search for prior methods using exactly three physical reference points and a live registered overlay for camera-view recovery.
- Search historical optical viewfinders, alignment frames, and cinematography manuals for physical registration techniques.
- Compare TPS with planar fiducials, calibration targets, and minimal pose-estimation methods without treating them as equivalent.
- Experimentally measure recovery repeatability under camera movement, replacement cameras, crop changes, and lens changes.
- Test the Working Focal Length convention against real lenses and the sensor-plane distance approximation.
- Establish how three-point matching behaves when the replacement physical triangle is relocated, scaled, or replaced.
- Do not treat lack of evidence in this review as evidence of TPS originality.

## 11. References

The complete bibliographic records and access statuses are maintained in [BIBLIOGRAPHY.md](BIBLIOGRAPHY.md). The most directly relevant examined sources are:

1. OpenCV, “Perspective-n-Point (PnP) pose computation,” 4.8.0 documentation.
2. OpenCV, “Camera Calibration,” 4.11.0 documentation.
3. Richard J. Radke, *Computer Vision for Visual Effects*, Chapters 4 and 6, Cambridge University Press, 2012; publisher chapter record examined.
4. Australian Film Television & Radio School, *Stop Motion*, pp. 14–15, open educational PDF.
5. Tom Gasek, “Objects, People, and Places,” in *Frame-by-Frame Stop Motion*, Chapter 6, pp. 104–105; chapter PDF examined, publisher access restricted.
6. Richard Hartley and Andrew Zisserman, *Multiple View Geometry in Computer Vision*.
7. MIT, *Foundations of Computer Vision*, §5.3.1.

## Independent Research Addendum

This addendum records the targeted external pass requested after the initial review. It is evidence about prior art and established practice, not a change to TPS requirements.

### OpenCV — Perspective-n-Point Pose Computation

The examined OpenCV 4.10 documentation states that pose computation uses 3D–2D point correspondences, camera intrinsics, and distortion parameters to estimate rotation and translation by minimizing reprojection error. Its P3P section states that `solveP3P()` uses exactly three 3D–2D correspondences and can return up to four solutions. The documentation also distinguishes P3P/AP3P input behavior in `solvePnP()` and notes that generic PnP can expose multiple solutions.

This directly establishes that three corresponding physical/image points are part of an existing camera-pose problem and that three correspondences do not necessarily identify a unique camera pose. It does not establish TPS: P3P assumes a pose-estimation objective and camera-model inputs, while TPS records and compares image locations and expressly does not require camera reconstruction.

### Dragonframe — *Using Dragonframe 2025*

The accessible indexed text from the examined Dragonframe 2025 manual describes onionskin transparency, dissolving a previous frame over Live View, difference mode, and frame-echo controls. Direct retrieval of the large PDF was limited by the source endpoint, so this source is treated as examined for the indexed manual sections but not as a complete manual review.

The material establishes an existing stop-motion practice of comparing a live view with a recorded frame using transparency or difference display. It does not establish physical point identities, measured triangle geometry, TPS Reference Distance, Working Focal Length, AOV, or a camera-independent TPS reference record.

### Dragonframe — Camera Support

The examined camera-support page states that Dragonframe creates a low-resolution live video-assist sequence and a high-quality capture sequence, keeps them in tandem, and may use live view for animation while capturing full-resolution stills. It also lists camera-specific live-view dimensions, including examples where live view is 960 × 640 or 1920 × 1280.

This is directly relevant to TPS coordinate-frame registration: a live comparison image and a final capture may not share dimensions or representation. It supports the need to distinguish the actual captured image frame from a video-assist frame. It does not define TPS registration or the TPS minimum reference contents.

### Szeliski — *Computer Vision: Algorithms and Applications*, Second Edition

The author's examined book page identifies the 2022 second edition, its computer-vision course basis, and the official electronic edition. The specific downloadable chapter text was not available in the reviewed page, so no chapter-specific mathematical claim is marked verified from this source.

The source is relevant as an authoritative textbook reference for camera geometry, image formation, registration, and matching, but this pass does not claim to have examined those specific chapters. It does not establish TPS or a three-point recovery workflow.

### Science-D-Visions — 3DEqualizer Technical Specification

The examined technical specification lists Lineup Controls for manual camera alignment to surveyed line geometry, dragging lineup-only points, extracting survey data from vertices, lines, and faces, and matching a camera in the current frame to tracked survey points. It also lists automatic camera-consistency operations involving rotation, translation, focal length, and camera position, as well as survey point types, distance constraints, camera constraints, adjustable lens parameters, and focal-length calculation from perspective grid shots.

These are clear precedents for:

- physical survey data associated with image-tracked points;
- physical-to-image correspondence;
- manual camera alignment;
- automatic camera alignment and consistency operations;
- use of distance constraints and lens/camera parameters.

The operational objective differs from TPS. 3DEqualizer is a software system for matchmoving, survey alignment, camera solving, lens modeling, and production tracking. TPS is an implementation-independent method for recording and recovering a three-point image view without requiring a solved virtual camera, a 3D scene reconstruction, or a particular software system.

The reviewed specification does not document a workflow that is substantially identical to the complete TPS operational model, including the TPS Reference Distance convention, the approved Working Focal Length and AOV record, and physical overlay or live-view recovery independent of camera-solving software. It does, however, substantially overlap the underlying correspondence and camera-lineup concepts. This reduces the basis for broad originality claims.

### FXguide — 3DEqualizer interview

The examined interview describes the value of precise survey data, including LIDAR, total-station data, and reference frames; use of survey to reduce tracking effort and address low-parallax shots; and the need to optimize lens distortion, focal length, scale, and other camera parameters. It also describes camera-tracking workflows and the distinction between monoscopic scale ambiguity and more constrained stereoscopic work.

This supports the conclusion that surveyed physical geometry and image tracking are established VFX practice. It does not establish TPS's manual, implementation-independent, three-point reference-and-recovery objective.

### Addendum conclusion

The closest technical precedents are P3P/PnP for three-point physical/image correspondence and pose ambiguity, 3DEqualizer for survey-based camera lineup and parameter adjustment, and Dragonframe for overlay-guided live/reference comparison. TPS's possible contribution is the combination and restriction of these ideas into a small, implementation-independent view-recovery method with preserved physical measurements and TPS-specific recorded calculations. That combination remains a research hypothesis, not a demonstrated novel contribution.

## VES and VFX Interoperability Addendum

### Visual Effects Society publications

The official VES release for the second edition of *The VES Handbook of Visual Effects: Industry Standard VFX Practices and Procedures* identifies the handbook as a practical guide covering VFX techniques and practices from pre-production through post-production. The examined release identifies Jeffrey A. Okun and Susan Zwerman as editors and confirms the 2014 second-edition publication announcement. The handbook's complete relevant chapters were not accessible during this pass. No chapter, author, or page-level claim about camera surveying, lens measurement, camera reports, markers, or lineup methods is therefore marked verified here.

The VES On-Set VFX Data Collection and Usage Guide announcement was examined on the official VES site. It describes a shared playbook for on-set data sets, capture methods, practical applications, stakeholders, handoffs, and workflow automation, and identifies Sheena Duggal as lead author with contributions from Sam Richards, Jim Geduldick, and Jake Morrison. The announcement establishes the existence and production-data purpose of the guide. It does not, by itself, verify a specific camera-survey field list or a three-point physical camera-recovery procedure.

The relevant VES practice overlap with TPS is organizational and operational: preserve useful on-set camera and reference information so that departments and downstream workflows can use it. This supports the general value of recording camera, lens, physical-reference, and image-reference data. It does not establish the TPS Reference Distance, Working Focal Length, AOV, or the TPS three-point method.

### VFX Reference Platform

The official VFX Reference Platform pages were examined. They define annual sets of tool and library versions intended to provide consistent build targets, minimize incompatibilities between software packages, ease integrated-pipeline support, and encourage interoperability. The project addresses software and library compatibility, versioning, and pipeline integration; it is not a camera-geometry, camera-matching, or image-registration specification.

For TPS, the implication is limited and practical. An implementation may use portable data structures, declared units, image-coordinate conventions, and documented interchange fields without depending on a particular VFX Reference Platform year. TPS should not claim conformance to the platform, adopt its version matrix as a requirement, or imply endorsement by the VFX Reference Platform or its maintainers.

### Comparison with TPS

| VES/VFX practice | Overlap with TPS | Difference or limitation |
|---|---|---|
| On-set camera and VFX data collection | Preserves production information for later use and handoff. | Publicly examined VES material here does not verify a three-point physical-camera recovery workflow. |
| Camera survey and matchmoving practice | Uses physical measurements, camera/lens data, and image evidence. | Conventional VFX workflows generally support virtual camera solving, tracking, and downstream reconstruction. TPS matches a view without making camera solving its objective. |
| VES Handbook | Represents established professional practice and procedures. | Relevant handbook chapters and pages were inaccessible; no specific handbook claim is verified. |
| VFX Reference Platform | Supports software interoperability and portable implementation choices. | It standardizes software/library environments, not TPS geometry, reference contents, or camera alignment. |

The review found no verified published VES or VFX Reference Platform source that formalizes the complete TPS workflow. This is not evidence of originality. The closest precedents remain P3P/PnP, VFX survey and matchmoving, 3DEqualizer lineup, and Dragonframe reference overlays.


==================================================
SOURCE: research/INTERDISCIPLINARY_PRIOR_ART.md
==================================================
# Interdisciplinary TPS Prior Art

**Status:** Research review. This document does not modify the TPS specification or claim originality.

## Scope and evidence standard

This review asks which established methods help an operator reproduce a previously recorded view using physical references, image comparison, or physical-to-image correspondence. It spans rephotography, photogrammetry, surveying, registration, fiducials, astronomy, microscopy, projective geometry, animation, and VFX.

Evidence is classified as:

- **Verified:** Relevant source content was examined and supports the stated description.
- **Partially supported:** The source supports the general method, but not every comparison or TPS interpretation.
- **Identified:** A source was located but the relevant content was not fully examined.
- **Needs research:** The method or historical claim requires additional source review or experiment.

## Method comparisons

### Repeat photography / rephotography

- **Field:** Landscape research, cultural heritage, and visual anthropology.
- **Authoritative source:** “Heritage and Repeat Photography: Techniques, Management, Applications, and Publications,” *Heritage* 5(4), 2022. DOI and open article: https://doi.org/10.3390/heritage5040220
- **Date or period:** 2022 review of earlier practice.
- **Technical principle:** Locate an earlier camera position and produce a new image for comparison; registration may be performed after capture.
- **Operational objective:** Measure or communicate change between historical and current views.
- **Similarities to TPS:** Previously recorded view, camera-view reproduction, image comparison, registration, and practical field repositioning.
- **Differences from TPS:** Rephotography commonly relies on landmarks, site records, maps, or image registration; it does not establish the TPS three-point physical/image record or TPS calculations.
- **Evidence status:** Verified for the review's description of rephotography objectives and registration challenges. No claim is made about a universal rephotography protocol.

### Photogrammetric space resection

- **Field:** Photogrammetry and surveying.
- **Authoritative source:** Carl Chow, “Photogrammetric Space Resection,” *Transactions of the American Society of Civil Engineers* 115(1), 1950, pp. 235–259, DOI: https://doi.org/10.1061/TACEAT.0006318
- **Date or period:** 1950.
- **Technical principle:** Known object/control points and their image coordinates constrain the exterior orientation of a photograph or camera.
- **Operational objective:** Determine camera position and orientation from control-point observations.
- **Similarities to TPS:** Three physical points, three corresponding image points, relative physical quantities, and camera-view geometry.
- **Differences from TPS:** Space resection is explicitly a camera-reconstruction method. TPS uses correspondence to compare/reproduce a view and does not require solving the camera pose.
- **Evidence status:** Verified from the publisher abstract and bibliographic record. The source is a very close mathematical precedent for the physical-to-image relationship, but not a TPS workflow.

### Basic photogrammetric resection / collinearity

- **Field:** Photogrammetry education and geodesy.
- **Authoritative source:** Open AGH, *Basics of Photogrammetry*, “Basics of Photogrammetry” module: https://epodreczniki.open.agh.edu.pl/handbook/4795/module/4812/reader
- **Date or period:** Current open educational material; publication date not relied upon.
- **Technical principle:** The perspective center, object point, and image point are collinear; exterior orientation uses camera position and orientation parameters.
- **Operational objective:** Convert between image and object space and determine camera orientation.
- **Similarities to TPS:** Physical/image point correspondence and explicit camera/image coordinate relationships.
- **Differences from TPS:** The educational method is oriented toward photogrammetric measurement and camera orientation, not operator-guided view recovery without camera solving.
- **Evidence status:** Verified for collinearity and exterior-orientation concepts.

### Planar homography and projective registration

- **Field:** Computer vision and projective geometry.
- **Authoritative source:** OpenCV, “Basic concepts of the homography explained with code”: https://docs.opencv.org/4.5.1/d9/dab/tutorial_homography.html
- **Date or period:** OpenCV 3.0+ tutorial; access date not used as a publication claim.
- **Technical principle:** A planar projective transformation maps points between planes up to scale; corresponding points can estimate the transformation.
- **Operational objective:** Align or warp planar image content and support pose reasoning.
- **Similarities to TPS:** Image-coordinate registration and planar reference geometry.
- **Differences from TPS:** A full homography generally requires at least four point correspondences and transforms image data. TPS does not fit an arbitrary transformation to force three points to agree and does not define a planar warp as its operation.
- **Evidence status:** Verified for the stated homography principle. The distinction from TPS is an interpretation consistent with the repository's registration derivation.

### Astronomical triangle matching and registration

- **Field:** Astronomy and astronomical image processing.
- **Authoritative source:** M. Beroiz, J. B. Cabral, and B. Sanchez, “Astroalign: A Python module for astronomical image registration,” *Astronomy and Computing* 32, 2020, article 100384, DOI: https://doi.org/10.1016/j.ascom.2020.100384
- **Date or period:** 2020.
- **Technical principle:** Match three-point star asterisms to estimate a linear transformation between images without requiring world-coordinate-system information.
- **Operational objective:** Register stellar images for stacking, difference imaging, and mosaics.
- **Similarities to TPS:** Explicit three-point configurations, correspondence, image registration, and comparison without a full camera model.
- **Differences from TPS:** Astroalign uses triangles as image features and estimates a transformation automatically; TPS identifies physical points and uses the recorded image locations to guide view recovery. Astroalign does not preserve TPS physical triangle measurements, D, Working Focal Length, or AOV.
- **Evidence status:** Verified from the article abstract and bibliographic record. This is one of the closest non-film precedents for three-point image registration, but it is not a physical-camera recovery method.

### Fiducial-marker registration in microscopy

- **Field:** Correlative microscopy and industrial-style multimodal registration.
- **Authoritative source:** Sajjad Mohammadian et al., “High accuracy, fiducial marker-based image registration of correlative microscopy images,” *Scientific Reports* 9, 3211, 2019, DOI: https://doi.org/10.1038/s41598-019-40098-4
- **Date or period:** 2019.
- **Technical principle:** Fiducial markers visible across modalities establish transformations between images with different resolution and contrast; multiple transformations can be composed.
- **Operational objective:** Register fluorescence and electron microscopy images accurately.
- **Similarities to TPS:** Physical or visible reference markers, correspondence, registered image frames, overlay comparison, and portable coordinate relationships.
- **Differences from TPS:** The method is multimodal microscopy registration and seeks accurate transformation estimation, not camera-view reproduction by an operator. It also uses marker systems and image transformations beyond TPS's minimal conceptual scope.
- **Evidence status:** Verified from the open article abstract and full text.

### Astronomy image registration with reference sources

- **Field:** Astrometry.
- **Authoritative source:** F. Masci et al., “Image registration and astrometric calibration for the Spitzer Space Telescope,” *Publications of the Astronomical Society of the Pacific* 116, 2004; open PDF: https://web.ipac.caltech.edu/staff/fmasci/home/sirtfwork/paper7R.pdf
- **Date or period:** 2004.
- **Technical principle:** Match common point sources, estimate offsets or transformations, and place images in a common reference frame.
- **Operational objective:** Combine images and measure motions or positions consistently.
- **Similarities to TPS:** Reference points, common coordinate frames, image registration, and uncertainty-aware comparison.
- **Differences from TPS:** The objective is astrometric measurement and image combination, not physical-camera repositioning or view recovery.
- **Evidence status:** Identified and source record located; the PDF was not fully examined in this pass. Specific claims remain unverified.

### Optical surveying and instrument resection

- **Field:** Land surveying and geodetic instrument setup.
- **Authoritative source:** The reviewed photogrammetric resection literature and surveying references treat resection as determining an unknown station from known control points and observed directions or image relationships.
- **Date or period:** Historical and continuing surveying practice.
- **Technical principle:** Known control points constrain an observer or instrument station.
- **Operational objective:** Establish instrument location and orientation relative to control.
- **Similarities to TPS:** Three-point reference geometry and repeatable aiming/alignment.
- **Differences from TPS:** Survey resection solves the observer's position/orientation. It is therefore a close physical precedent but not evidence that TPS's non-solving objective is novel.
- **Evidence status:** Partially supported by the examined resection sources; a dedicated instrument-manual review remains needed.

### Traditional animation and registration pins

- **Field:** Hand-drawn and cel animation, film registration.
- **Authoritative source:** Registration-pin historical record located in the reviewed search; authoritative archival manual not examined in this pass.
- **Date or period:** Historical film and animation practice.
- **Technical principle:** Physical pins or peg bars hold successive image media in a repeatable spatial relationship.
- **Operational objective:** Preserve frame-to-frame registration during drawing, exposure, copying, or compositing.
- **Similarities to TPS:** Physical registration, overlays, and repeatable image-frame alignment.
- **Differences from TPS:** Registration pins stabilize media rather than reproduce a camera view from three physical scene points.
- **Evidence status:** Identified; needs authoritative historical-manual verification.

## Cross-domain answers

### A. Methods sharing TPS's operational objective

Repeat photography and some stop-motion or optical-overlay practices most closely share the operator objective of returning to a previously recorded view through visual comparison. Photogrammetric resection shares the geometric information but changes the objective to camera reconstruction.

### B. Shared measurements

Photogrammetry and VFX surveying preserve physical control-point coordinates, image coordinates, camera orientation, focal length, and sometimes lens or distance data. These overlap TPS's physical triangle measurements, correspondence, image frame, TPS Reference Distance, and Working Focal Length inputs. The sources do not establish TPS's exact combination or its sensor-plane convention.

### C. Reconstruction requirements

Space resection, P3P/PnP, VFX matchmoving, and surveying resection generally reconstruct or estimate camera/instrument pose. Repeat photography and overlay-guided animation can operate through visual alignment without explicitly solving pose. TPS belongs operationally closer to the latter while using measurements associated with the former.

### D. Portable reference data

Photogrammetric control-point records, fiducial-marker coordinate systems, astronomical reference frames, and VFX survey packages all demonstrate the value of preserving identifiers, coordinates, units, and frame conventions. This supports the general importance of portable reference data but does not prescribe a TPS file format.

### E. Potentially equivalent methods

No examined source documents a method that is clearly equivalent to the complete TPS workflow: three identified physical points; three corresponding image locations; a registered reference; preserved physical triangle measurements; TPS Reference Distance; Working Focal Length and AOV; and operator-guided recovery without camera reconstruction. Astroalign is equivalent to a three-point image-registration subproblem, and photogrammetric space resection is equivalent to the physical/image geometry but has the opposite operational objective. These are substantial precedents, not complete duplicates.

### F. Mathematical limitations to acknowledge

- Three physical/image correspondences can support camera-pose calculations, but pose may be non-unique under perspective models.
- Three image points do not generally determine a full planar projective transformation; arbitrary registration can create false agreement.
- Perspective projection does not generally preserve physical triangle shape.
- Unequal point depths, reference-plane tilt, lens distortion, crop, scaling, and differing image frames affect comparison.
- Fiducial or feature correspondence must preserve identity; proximity is not sufficient.
- Rephotography and visual overlays demonstrate practical alignment, not proof of recovered camera pose.

## Research conclusion

The interdisciplinary record shows that TPS is assembled from well-established elements: rephotography, physical control points, projective geometry, fiducial registration, overlays, and camera surveying. The potentially distinct contribution is their deliberately minimal combination for practical camera-view reproduction without requiring camera reconstruction, together with a portable reference record. That contribution remains a hypothesis requiring broader prior-art search, especially historical manuals and patents, and experimental comparison against existing workflows.


==================================================
SOURCE: research/derivations/IMAGE_REGISTRATION.md
==================================================
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

==================================================
SOURCE: research/derivations/PHYSICAL_IMAGE_TRIANGLES.md
==================================================
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

==================================================
SOURCE: research/derivations/WORKING_FOCAL_LENGTH.md
==================================================
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
- `D`: measured distance from the camera sensor plane to the designated reference plane, in millimeters.
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

The proposed `D` is measured from the camera sensor plane. In an ideal pinhole derivation, depth is measured from the projection center. In a real lens, the relevant optical reference is associated with principal planes or an effective projection center, not necessarily the physical sensor plane or the entrance pupil.

Therefore, using sensor-plane distance in the proposed relationship is an approximation unless the chosen optical model establishes that the sensor-plane measurement is the intended object distance for the calculation.

For a finite-focus thin-lens model, the image distance is not generally identical to the focal length. A more complete model distinguishes object distance, image distance, and principal-plane locations. The current proposed relationship does not specify those quantities, so it should not be described as an exact real-lens formula.

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

==================================================
SOURCE: research/papers/PAPER_01_REVISED.md
==================================================
# The Three Point System: A Reference-Based Method for Camera-View Reproduction

**Christopher Weinberg**
**LIMNMEDIA**

## 1. Abstract

The Three Point System (TPS) is an implementation-independent method for recording and reproducing a camera view. Its central principle is: “TPS connects three points in the physical world with where those same three points appear in an image.” A TPS reference identifies three physical points, records their corresponding image locations, preserves the physical relationships among the points, and retains information needed to interpret and register the image coordinates. It may also preserve a measured TPS Reference Distance, a Working Focal Length, and a derived horizontal angle of view.

TPS is deliberately narrower than camera calibration, photogrammetric resection, or visual-effects matchmoving. It does not attempt to solve for a unique camera position, orientation, or complete camera model. Instead, it gives an operator a portable visual reference and a small set of physical measurements with which to seek the closest practical reproduction of a previously recorded three-point view. The method can be implemented with a physical overlay, a monitor, photographic or film media, or software.

The geometric foundations of TPS are established principles of perspective projection and correspondence. Related practices exist in multiple disciplines, including photogrammetry, rephotography, image registration, visual effects, fiducial registration, astronomy, and stop-motion production. This paper defines the reference, describes the recording and recovery operations, and derives the associated camera quantities under stated assumptions. Practical performance remains to be evaluated.

## 2. Introduction

Reproducing a camera view is a common practical problem. A camera may be moved, removed, replaced, or unavailable when a scene must be photographed again. The problem appears in independent filmmaking, visual effects, stop-motion, architectural documentation, rephotography, education, and other settings. Existing solutions range from careful physical measurements and motion-control systems to camera calibration, feature tracking, and full matchmoving pipelines. These approaches can be effective, but they may require specialized equipment, software, or technical expertise.

TPS addresses a more limited question: how can an operator record enough information about a view to seek that view again later using three identifiable physical reference points and their image locations? The intended answer is not a camera-solving algorithm. It is a reference-based method for view matching.

The TPS kernel states the relationship directly: “TPS connects three points in the physical world with where those same three points appear in an image.” The physical points are conventionally labeled A, B, and C. Their corresponding image points are a, b, and c. The identities are preserved as A→a, B→b, and C→c, even when the image coordinates change.

This distinction between identity and location is fundamental. A point can move in an image when the camera moves, rotates, changes focal length, or changes other imaging conditions. The image point remains associated with the same physical point. Conversely, three image locations alone do not reveal a unique three-dimensional camera configuration. Multiple physical and camera configurations can produce the same three-point projection under appropriate conditions.

TPS therefore has two layers. The first is geometric: physical points are projected into image space, and correspondence can be compared. The second is operational: a reference is recorded and later presented in registration with a live view so that a user can adjust the camera. The first layer rests on established mathematics. The practical effectiveness of the second layer requires experiments.

## 3. Related Work

### Photogrammetric resection and PnP

Photogrammetry provides a close mathematical precedent. In space resection, known control points and their image coordinates are used to determine the exterior orientation of a photograph or camera. Chow’s 1950 paper discusses three ground control points and their photograph coordinates as a basis for determining the position and orientation of a photograph [1]. Open educational photogrammetry material similarly describes the collinearity of the perspective center, object point, and image point, together with exterior-orientation parameters [2].

Perspective-n-point methods provide a modern computer-vision counterpart. OpenCV documents P3P as a pose problem using exactly three 3D–2D correspondences, with up to four possible solutions [3]. The same documentation describes PnP as estimating rotation and translation from object points, image projections, camera intrinsics, and distortion parameters. These methods establish that physical/image point correspondence is a standard input to camera pose estimation, and that three correspondences do not necessarily imply a unique pose.

TPS overlaps this geometry but has a different objective. Resection and PnP seek camera or object parameters. TPS does not require the operator to solve for a camera pose. It uses correspondence to compare a recorded view with a live view and to guide adjustment toward a practical match. Thus, TPS should not be described as a simplified PnP solver.

### Repeat photography

Repeat photography, or rephotography, seeks to make a new photograph from an earlier viewpoint, often to document landscape or cultural change. A review in *Heritage* describes locating the original camera position, producing a new image, and addressing the registration of old and new images [4]. This shares TPS’s operational goal more closely than camera resection does: the desired outcome is a comparable view rather than a complete camera model.

The difference is that rephotography commonly uses landmarks, historical records, maps, field judgment, or post-capture image registration. The reviewed literature does not establish the TPS record of three identified physical points, explicit A→a/B→b/C→c correspondence, physical triangle measurements, or TPS calculations. TPS can be understood as a constrained and formalized reference strategy within the larger problem of repeat photography.

### Image registration and homography

Image registration establishes a common coordinate relationship between images. OpenCV’s homography tutorial describes a planar projective transformation between planes [5]. In a full projective transformation, the transformation model has more degrees of freedom than three point pairs can determine. TPS therefore distinguishes registration from geometric correction. A known crop, rotation, scale, or coordinate transformation may be applied to make two records interpretable in the same frame. An arbitrary transformation chosen because it makes three nonmatching projections coincide would remove the difference TPS is meant to measure.

Astroalign is a particularly relevant interdisciplinary precedent. Beroiz, Cabral, and Sanchez describe matching three-point star asterisms to find transformations between astronomical images without relying on world-coordinate-system information [6]. This demonstrates an established three-point image-registration technique. It differs from TPS because its triangles are image features rather than identified physical scene points, and its output is an estimated image transformation rather than an operator-guided physical camera recovery.

Fiducial-marker registration in microscopy provides another related precedent. Mohammadian and colleagues describe visible markers and composed transformations for registering fluorescence and electron-microscopy images with different resolution and contrast [7]. The work supports the general value of stable correspondences, registered frames, and overlay comparison. It does not establish TPS’s camera-view objective or its physical triangle record.

### VFX camera surveying and lineup

Visual-effects matchmoving systems use tracked image features, survey data, camera and lens parameters, and optimization to reconstruct a virtual camera and scene relationship. 3DEqualizer documents manual and automatic camera lineup to surveyed geometry, survey points, distance constraints, focal-length controls, and lens parameters [8]. A related industry interview discusses the use of LIDAR, total-station data, reference frames, and lens-distortion models in production camera tracking [9].

These practices substantially overlap TPS’s use of physical measurements and image correspondences. They differ in scale and purpose. A VFX pipeline generally seeks a virtual camera, tracked scene, lens model, or renderable production solution. TPS seeks a portable reference for a human or application to reproduce a view and does not require the recovery of a unique virtual camera.

### Stop-motion overlays

Stop-motion workflows commonly compare a live camera view with a previous frame. The Australian Film Television & Radio School describes onion-skin transparency as a way to see a prior frame over the live image and align the next drawing [10]. Gasek describes frame-grabber onion skinning and ghosted frames for placement registration after a camera bump [11]. Dragonframe documentation similarly describes onionskin, Live View comparison, line-up layers, and difference display [12].

These are close operational precedents for registered visual comparison. They demonstrate that an overlay can guide an operator without requiring a camera solution. They do not, in the sources examined, define a reference consisting of three identified physical points together with physical triangle measurements, TPS Reference Distance, Working Focal Length, and AOV.

## 4. TPS Method

TPS begins by identifying three distinct, non-collinear physical points. A point is a specified location in three-dimensional Euclidean space; it need not be a separate physical object. A corner, mark, or identifiable feature may represent one. The points are labeled A, B, and C.

The camera observes the points and produces image points a, b, and c. Correspondence is explicit:

```text
A → a
B → b
C → c
```

The reference preserves both the identities and the image locations. The physical triangle and image triangle are related but are not assumed to be geometrically similar. Under perspective projection, physical side-length ratios and angles are not generally preserved in the image.

A TPS reference preserves at least the following information:

1. The three identified physical points A, B, and C.
2. Their image locations a, b, and c.
3. Explicit correspondence.
4. Measured physical triangle relationships, including AB and other relationships relevant to the operation.
5. The TPS Reference Distance, D.
6. The actual captured image width and height in pixels.
7. Active physical sensor dimensions when known and applicable to the captured imaging area.
8. Image coordinate-frame information sufficient to interpret and register the recorded points.
9. The Working Focal Length, its inputs, and the calculated horizontal AOV.

The image coordinate frame must state image dimensions, coordinate origin, axis directions, coordinate units, point positions, and relevant crop, rotation, or mirroring information when needed. No particular file format or software convention is required. The purpose is interpretability across implementations.

The TPS Reference Distance is measured from the camera sensor plane to the designated physical reference plane. It is not automatically equivalent to a lens focus-ring marking, a manufacturer-reported focus distance, or an ideal optical projection-center distance. The sensor-plane convention is practical and approximate.

## 5. Mathematical Foundations

Under an ideal perspective camera, a physical point with camera coordinates `(X,Y,Z)` projects to image-plane coordinates

```text
x = f X / Z
y = f Y / Z
```

where `f` is the model focal length. This mapping explains why image position depends on camera position, orientation, intrinsic parameters, and point depth. It also explains why the physical triangle need not resemble the image triangle.

If A, B, and C have different depths, each point is scaled by a different denominator. A single scale factor therefore does not generally relate all physical side lengths to all image side lengths. Similarity can occur in special cases, such as a triangle on a plane parallel to the image plane under an ideal model, or under an orthographic approximation. Similarity is not a universal TPS requirement.

Correspondence is a different concept from similarity. TPS preserves which image point belongs to which physical point. It does not claim that A, B, and C and a, b, and c have equal distances or angles. Three physical points can also produce a collinear or coincident image configuration under certain viewing geometries. Such a projection exists, although it may be unusable for a particular operation.

Registration also has a limited role. Two records may use different resolutions, crops, rotations, or coordinate conventions. A declared transformation can place them in a common frame. That transformation must be known or independently justified. It must not be selected solely to force a mismatch into agreement.

## 6. Working Focal Length and AOV

TPS records a Working Focal Length when establishing a reference. The approved calculations are:

```text
f_px = |xB - xA| * D / AB

AOV_h = 2 * atan(AB * W_image / (2 * D * |xB - xA|))

f_mm = f_px * W_sensor / W_image
```

Here, `xA` and `xB` are roll-corrected horizontal image coordinates; `AB` is the measured physical distance between A and B; `D` is the TPS Reference Distance; `W_image` is the actual captured image width in pixels; and `W_sensor` is the active physical sensor width in millimeters.

The ideal pinhole relationship is `image separation = focal length × physical separation / Z`, where `Z` is the segment’s depth measured along the camera optical axis from the projection center. TPS substitutes the measured sensor-plane-to-reference-plane distance `D` for `Z` as a practical approximation. This substitution is most defensible when A and B lie approximately in the designated reference plane, that plane is approximately perpendicular to the optical axis, and the difference between sensor plane and projection center is small relative to the working distance. The second equation follows from the ideal pinhole model: the half-width of the image corresponds to half the horizontal field angle. Substituting `f_px = |xB-xA|D/AB` gives the equivalent form `AOV_h = 2 atan(W_image/(2 f_px))`. The third converts pixel focal length to millimeters using the active sensor width and captured image width.

These calculations require assumptions. A and B should be at approximately equal depth, and the physical A–B segment should be aligned as closely as practical with camera-horizontal. Roll correction accounts for image rotation; it does not correct physical A–B misalignment. Lens distortion, unequal depth, reference-plane tilt, crop ambiguity, resampling, finite-focus effects, and the sensor-plane distance convention can introduce error.

`f_px` and `AOV_h` do not require physical sensor dimensions. `f_mm` does. If active sensor dimensions are unavailable, the reference remains usable with the pixel calculation and AOV retained while the millimeter calculation is omitted. The AOV is derived from TPS geometry; it does not independently determine a missing sensor width. The Working Focal Length is a TPS measurement convention and is not necessarily identical to a manufacturer’s nominal focal length or a laboratory effective focal length.

These equations are dimensionally consistent under the stated ideal geometry. Their application to real cameras is approximate and remains experimentally unvalidated.

## 7. Recording and Recovering a View

### Establishing the reference

Consider a stop-motion set that must be photographed again after the camera has been removed. Before the original setup is disturbed, the operator chooses three identifiable points on the set, A, B, and C, that can be identified again. The points need not be dedicated markers: suitable corners or set features may serve, provided their identities are unambiguous and they retain their intended geometric relationships for the recovery operation. The operator identifies their image locations a, b, and c in a captured reference image and records the physical triangle measurements. A and B should be selected with the Working Focal Length assumptions in mind; the general correspondence method does not require the whole triangle to be parallel to the image plane.

The reference also preserves the image's actual pixel dimensions, coordinate origin and axis conventions, and any information needed to interpret crop, rotation, or mirroring. The operator measures the TPS Reference Distance D from the sensor plane to the designated physical reference plane and records the measurement convention. Active physical sensor dimensions are included when known, and only when they correspond to the active imaging area represented by the capture. When establishing the TPS reference, the Working Focal Length and horizontal AOV are calculated and retained with their inputs. If active sensor dimensions are unavailable, `f_px` and `AOV_h` are retained and `f_mm` is omitted. These values describe the original reference; they are not a substitute for the three correspondences.

### Recovering the view

When the set is revisited, the operator identifies the same physical points. The recorded image points are displayed in a coordinate frame registered to the current live camera image. A transparent reference can be placed over a television monitor showing the live view; a registered celluloid or film reference can be aligned with an optical or projected view; or a digital overlay, such as a transparent PNG, can be composited over a live feed. The overlay is one representation of the reference, not the complete TPS record.

The operator adjusts the physical camera while observing the positions of A, B, and C relative to a, b, and c. Camera position, orientation, focal length, crop, and other imaging parameters that affect the projection or image coordinate frame may each affect the observed positions. The reference helps the operator recognize the remaining differences, but TPS does not prescribe an adjustment order or claim that a particular mismatch uniquely identifies its cause. The objective is the closest practical reproduction of the recorded three-point projection, judged in the context of the shot.

The physical measurements provide a durable description of the reference triangle and a way to check or re-establish the recorded triangle measurements if the set is disturbed. D and the derived camera quantities provide additional context for re-establishing the setup, particularly when the original lens settings are unavailable. None of these measurements alone determines the recovery camera's pose. If the set points themselves have moved, the original correspondence no longer describes the same physical geometry until that change has been resolved.

A replacement camera may have different sensor dimensions, image resolution, lens behavior, or controls. In that case the live image and recorded point positions must still be compared in an appropriately registered frame; matching raw pixel coordinates from unlike images is not meaningful without a justified mapping. TPS does not require identical camera equipment, but it does not guarantee that two different optical systems can reproduce the same projection over the entire scene.

## 8. Assumptions and Limitations

TPS assumes that point identities remain consistent within a correspondence set. The physical points must remain visible and maintain the intended geometric relationships for the operation. If a different triangle is used, its correspondence and geometric relationship to the reference must be established separately. Triangle similarity is one possible relationship, not a universal requirement.

Three-point matching is limited. A match of a, b, and c does not prove that the original camera position, orientation, focal length, or complete configuration has been recovered. It does not guarantee that other scene points project to the same locations or that the complete image matches. OpenCV’s P3P documentation provides a direct mathematical reminder: exactly three 3D–2D correspondences can yield up to four pose solutions [3].

The reference can also be geometrically degenerate. If projected points are coincident or collinear, the three-point record may not contain enough information for a particular operation. Point correspondence must not be inferred from proximity alone. A point that moves across the image remains associated with its original physical identity.

The Working Focal Length calculation has additional limitations. D is measured from the sensor plane rather than an ideal projection center. A and B may have unequal depth. The reference plane may be tilted. Lens distortion and focus breathing may affect the relation between image separation and focal length. The active sensor width may be unknown or may not correspond to the captured image area. These limitations mean that the recorded value is best treated as a reproducible TPS quantity under stated conditions, not as a universal optical truth.

Finally, practical matching involves measurement uncertainty and operator judgment. A visual match can be useful without being mathematically exact. Exact coordinate equality and practical agreement within a user- or operation-specific tolerance must remain distinct.

## 9. Discussion

TPS sits between two established traditions. One tradition solves geometry: photogrammetric resection, P3P/PnP, camera calibration, homography, and matchmoving estimate transformations, camera parameters, or scene structure. The other tradition guides practical alignment: repeat photography, stop-motion onion skin, reference overlays, and fiducial registration help an operator compare one view with another.

TPS uses information from both traditions but adopts neither objective completely. It borrows the precision of explicit point identity, physical measurement, and declared image coordinates. It borrows the accessibility of a registered visual comparison. It does not require a 3D reconstruction, a solved camera, a calibration pattern, a proprietary software package, or a particular recording medium.

This combination may be useful for independent animators, students, small productions, educators, and production environments where the desired result is a repeatable view rather than a complete camera asset. Its possible contribution is organizational and operational: define a small reference containing physical and image information, preserve it independently of technology, and use it to guide recovery.

The component techniques are established; this paper characterizes their particular use as a portable reference workflow. Comparative performance and originality are open questions rather than demonstrated results.

## 10. Future Validation

A first practical demonstration can test the complete TPS workflow without establishing a universal performance threshold. Record a reference image and the three identified physical points, their measured triangle, image coordinates, coordinate frame, D, and available camera quantities. Remove or move the camera, then attempt recovery using a registered reference overlay. Preserve the recovered image and compare the three reference-point positions, together with several visible scene features outside the triangle. Report the observed differences, setup conditions, and any operator adjustments without treating three-point agreement as proof of full-image agreement.

Later work could compare repeatability across operators or camera systems and separately evaluate Working Focal Length against independently measured optical parameters. Those studies are extensions, not prerequisites for presenting the reference method. No experimental result is asserted here.

## 11. Conclusion

TPS is a reference-based method for camera-view reproduction. It connects three identified physical points with the locations where those points appear in an image. A TPS reference preserves correspondence, image coordinates, physical triangle measurements, coordinate-frame information, a measured TPS Reference Distance, and related Working Focal Length and AOV information when available.

The method is independent of software, hardware, operating system, file format, and recording medium. Recovery compares a registered reference with a live view and adjusts toward the closest practical match; three-point agreement does not establish a unique camera configuration or complete scene alignment.

The mathematical foundations and many operational components have clear precedents. Photogrammetric resection and P3P establish related physical/image geometry. Rephotography establishes the goal of returning to a prior view. Fiducial registration, astronomy, homography, VFX surveying, and stop-motion overlays establish related methods of correspondence, registration, and practical alignment. The possible contribution of TPS is the constrained, portable combination of these ideas for view matching without camera solving. That possibility remains to be tested and compared, not asserted as established originality.

## 12. References

[1] Carl Chow, “Photogrammetric Space Resection,” *Transactions of the American Society of Civil Engineers* 115(1), 1950, pp. 235–259. DOI: https://doi.org/10.1061/TACEAT.0006318.

[2] Open AGH, *Basics of Photogrammetry*, “Basics of Photogrammetry” module. https://epodreczniki.open.agh.edu.pl/handbook/4795/module/4812/reader.

[3] OpenCV, “Perspective-n-Point (PnP) pose computation,” version 4.10.0 documentation. https://docs.opencv.org/4.10.0/d5/d1f/calib3d_solvePnP.html.

[4] “Heritage and Repeat Photography: Techniques, Management, Applications, and Publications,” *Heritage* 5(4), 2022. https://doi.org/10.3390/heritage5040220.

[5] OpenCV, “Basic concepts of the homography explained with code.” https://docs.opencv.org/4.5.1/d9/dab/tutorial_homography.html.

[6] M. Beroiz, J. B. Cabral, and B. Sanchez, “Astroalign: A Python module for astronomical image registration,” *Astronomy and Computing* 32, 2020, article 100384. DOI: https://doi.org/10.1016/j.ascom.2020.100384.

[7] Sajjad Mohammadian et al., “High accuracy, fiducial marker-based image registration of correlative microscopy images,” *Scientific Reports* 9, 3211, 2019. DOI: https://doi.org/10.1038/s41598-019-40098-4.

[8] Science-D-Visions, *3DEqualizer Technical Specification*. https://www.3dequalizer.com/?item=tech_spec&site=start.

[9] Mike Seymour, “3DEqualizer – German precision where VFX needs it,” *fxguide*, 2014. https://www.fxguide.com/quicktakes/3dequalizer-german-precision-where-vfx-needs-it/.

[10] Australian Film Television & Radio School, *Stop Motion*, pp. 14–15. https://medialab.aftrs.edu.au/wp-content/uploads/2021/07/AFTRS16_StopMotion.2021.pdf.

[11] Tom Gasek, “Objects, People, and Places,” in *Frame-by-Frame Stop Motion: The Guide to Non-Puppet Photographic Animation*, Chapter 6, pp. 104–105. Publisher chapter PDF: https://www.bloomsburyvisualarts.com/app/downloadpdf?docIdS=b-9781315155166.

[12] DZED Systems, *Using Dragonframe 2025*. https://www.dragonframe.com/download/Using%20Dragonframe%202025.pdf.

[13] MIT, *Foundations of Computer Vision*, §5.3.1, “Image Formation by Perspective Projection.” https://visionbook.mit.edu/imaging.html.
