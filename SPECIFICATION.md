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

Recovery uses the recorded three-point projection as a reference for comparison with the corresponding points in a live camera view. The user adjusts the camera to obtain the closest practical reproduction of the recorded view. The recorded reference points must be presented in registration with the live viewing frame. A transparent reference over a television monitor, registered celluloid or film, and a digital overlay such as a transparent PNG are possible representations; none is mandatory. An overlay represents the TPS reference for comparison but is not the complete TPS reference itself. A recovery record may preserve observed image coordinates and comparison information, but saving one is optional. The recovery camera need not be identical to the original camera.

### Matching Principle

The objective is the closest practical reproduction of the recorded view, evaluated through the match between corresponding three-point projections. Users refine the camera view through comparison with the TPS reference. TPS does not prescribe a universal numerical acceptance tolerance.

A projection match does not guarantee identical camera pose or complete scene alignment.

## 5. Geometric Model

See [docs/GEOMETRY.md](docs/GEOMETRY.md).

## 6. Mathematical Formulation

Reserved for review and development.

## 7. Validation

See [docs/VALIDATION.md](docs/VALIDATION.md).
