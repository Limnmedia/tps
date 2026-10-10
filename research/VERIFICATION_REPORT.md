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
