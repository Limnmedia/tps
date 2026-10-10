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
