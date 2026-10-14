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

### Transfer to a Second Physical Setup

The original TPS reference remains unchanged during transfer. It preserves the original A/B/C correspondence, image locations, physical measurements, image frame, and recorded camera-reference information.

On a second physical setup, the operator identifies the corresponding A, B, and C points and measures their actual physical relationships. Differences in scale or point arrangement must be recorded and must not be silently treated as equivalent to the original geometry. The recorded image correspondences then guide registered camera-view comparison and recovery.

An identical physical triangle is not required unless a specific operation explicitly requires it. This operating case does not define a scale-conversion formula or camera-pose solution.

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
