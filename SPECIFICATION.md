# Three Point System (TPS) Specification

**Status:** Working Draft 0.1

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

A TPS reference must preserve the minimum contents defined in [Definition 6 — TPS Reference](docs/DEFINITIONS.md#definition-6--tps-reference). These contents include the three identified physical points, their corresponding image locations and explicit correspondence, image coordinate-frame information, measured physical triangle relationships, focus distance, and Working Focal Length.

TPS calculates and records the Working Focal Length when establishing the reference. Calculation inputs are retained for reproducibility and verification. Downstream applications may independently recalculate or reinterpret focal length, but the original TPS value remains preserved.

A three-point projection describes correspondence between physical points and image locations. A TPS reference preserves the information required to reproduce the recorded view. These are related but distinct concepts.

## 5. Geometric Model

See [docs/GEOMETRY.md](docs/GEOMETRY.md).

## 6. Mathematical Formulation

Reserved for review and development.

## 7. Validation

See [docs/VALIDATION.md](docs/VALIDATION.md).
