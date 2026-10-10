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
