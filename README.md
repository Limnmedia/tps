# Three Point System (TPS)

**An open camera-view reference method and emerging standard by LIMNMEDIA.**

**Record the view. Move the camera. Find the view again.**

The Three Point System (TPS) is an open, implementation-independent method for establishing and preserving correspondence between three identified physical reference points and their locations in an image. That correspondence provides a geometric reference for comparing and reproducing a recorded camera view.

TPS was created by Christopher Weinberg. LIMNMEDIA develops and maintains the open specification.

TPS is intended for artists, students, independent animators, stop-motion teams, and VFX technicians who need a practical way to preserve a camera view after a camera has moved, been removed, or been replaced.

> **TPS connects three points in the physical world with where those same three points appear in an image.**

TPS is a view-matching method. It is not a camera-pose solver and does not claim that matching three points uniquely recovers a camera or aligns an entire scene.

## The Problem

A camera setup may need to be reproduced days, weeks, or months after the original work. The camera may have moved, been removed, or become unavailable. Detailed camera measurements and specialized tracking systems are not always practical or available.

TPS preserves a small, portable reference that can help an operator work back toward the original view.

Imagine an animator photographing a miniature set. The camera must be removed so the set can be modified. Weeks later, the animator needs to photograph the scene from approximately the same view. TPS provides a recorded reference to guide the camera back toward that view.

## The Idea

Three physical points are identified as **A**, **B**, and **C**. Their corresponding locations in the image are recorded as **a**, **b**, and **c**:

```text
Physical space:  A, B, C
                       ↓ projection
Image space:      a, b, c
```

The identities remain associated:

```text
A → a
B → b
C → c
```

The physical triangle and the image triangle are related, but they are not assumed to have the same shape, lengths, or angles.

## How It Works

1. Identify three physical reference points.
2. Record their correspondence and image locations in a defined image coordinate frame.
3. Measure and record the physical relationships among A, B, and C, along with the information needed to interpret their image locations.
4. Measure the TPS Reference Distance and calculate the Working Focal Length using the recorded geometry.
5. Present the reference in registration with a later live camera view.
6. Adjust the camera while comparing the live locations of A, B, and C with the recorded three-point image relationship.

A and B provide a useful initial alignment reference. C supplies additional geometric information that can reveal differences not apparent from A and B alone.

The objective is the closest practical three-point projection match. A physical overlay, monitor, film reference, or software display may be used, but TPS does not require a particular technology.

## Why TPS?

- **Accessible:** designed to support practical camera work without requiring a complete tracking or reconstruction pipeline.
- **Portable:** the reference is information, not a particular application, file format, camera, or recording medium.
- **Interoperable by design:** TPS defines physical measurements and image correspondences independently of a particular tool or workflow.
- **Understandable:** the central operation can be explained directly in physical and image-space terms.

TPS does not guarantee a unique camera position, identical camera pose, pixel-perfect alignment, or complete scene reproduction. Those limits are part of the project’s technical documentation.

## The LIMNMEDIA Ecosystem

LIMNMEDIA is developing TPS as an open standard alongside tools such as **LIMNTPS** and **LIMNTPS Align**.

The distinction is important:

- **TPS** is the implementation-independent specification and research project.
- **LIMNTPS** and **LIMNTPS Align** are software implementations or tools that may support TPS workflows.

Software behavior does not define the TPS specification.

## Project Status

The current baseline is **TPS Specification v0.1 — Candidate**.

The candidate records approved specification material. Mathematical derivations, prior-art research, and experimental plans are kept separately. The candidate is not yet experimentally validated.

## Documentation

Start here:

- [TPS Specification](SPECIFICATION.md)
- [Primary use case: recovering a camera view](docs/USE_CASES.md)
- [Definitions](docs/DEFINITIONS.md)
- [Observations](docs/OBSERVATIONS.md)
- [Invariants](docs/INVARIANTS.md)
- [Constraints](docs/CONSTRAINTS.md)
- [Geometry](docs/GEOMETRY.md)
- [Validation](docs/VALIDATION.md)
- [Specification review](docs/SPECIFICATION_REVIEW.md)

Research and technical foundations:

- [Research overview](research/README.md)
- [Bibliography](research/BIBLIOGRAPHY.md)
- [Evidence map](research/EVIDENCE_MAP.md)
- [Prior-art review](research/PRIOR_ART_REVIEW.md)
- [Interdisciplinary prior art](research/INTERDISCIPLINARY_PRIOR_ART.md)
- [Research derivations](research/derivations/)
- [Paper 1 — revised draft](research/papers/PAPER_01_REVISED.md)

## Get Involved

TPS is an evolving specification. Useful contributions include:

- Clear technical corrections.
- Real-world use cases and workflow observations.
- Independent validation results.
- Prior-art references and evidence.
- Questions about terminology, geometry, or implementation independence.

Please see [CONTRIBUTING.md](CONTRIBUTING.md) before opening an issue or proposing a change.

## About LIMNMEDIA

LIMNMEDIA develops accessible tools and open technical methods connecting physical production, image-making, and practical creative workflows.

Learn more at [limnmedia.com](https://limnmedia.com/).
