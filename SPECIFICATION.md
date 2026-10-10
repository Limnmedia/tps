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

### Working Focal Length

When establishing a TPS reference, TPS calculates the Working Focal Length using:

```text
f_TPS = (|xB - xA| / W_image) * W_sensor * (D / AB)
```

Here, `xA` and `xB` are the horizontal image coordinates of A and B after accounting for recorded camera roll. `W_image` is the captured image width in pixels. `W_sensor` is the active physical sensor width in millimeters. `D` is the measured sensor-plane-to-reference-plane distance in millimeters. `AB` is the measured physical A–B distance in millimeters.

The calculation assumes that A and B are at approximately equal depth and that A–B is aligned as closely as practical with camera-horizontal. Roll correction accounts for image rotation; it does not correct physical A–B misalignment.

Sensor-plane distance is a practical measurement convention. Relative to ideal projection-center geometry, the result is approximate. The Working Focal Length is not necessarily identical to the lens manufacturer's nominal focal length.

The calculated value and necessary inputs are preserved with the TPS reference. Downstream VFX applications may independently calculate or reinterpret focal length without overwriting the original TPS value. The complete derivation and limitations are documented in [Working Focal Length Derivation](research/derivations/WORKING_FOCAL_LENGTH.md).

### Matching Principle

The objective is the closest practical match between corresponding three-point projections. Users refine the camera view through comparison with the TPS reference. TPS does not prescribe a universal numerical acceptance tolerance.

A projection match does not guarantee identical camera pose or complete scene alignment.

## 5. Geometric Model

See [docs/GEOMETRY.md](docs/GEOMETRY.md).

## 6. Mathematical Formulation

Reserved for review and development.

## 7. Validation

See [docs/VALIDATION.md](docs/VALIDATION.md).
