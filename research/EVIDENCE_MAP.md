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
| Perspective projection does not generally preserve physical triangle shape. | Geometry Principle 1, `docs/GEOMETRY.md:9–64` | Established optical principle | MIT, §5.3.1; OpenStax, §10.3 | Partially supported | The sources support perspective scaling and triangle geometry, but a direct source-backed derivation of the full TPS wording remains outstanding. |
| Focal length affects field of view and image formation. | Observation 4, `docs/OBSERVATIONS.md:98–137`; Definition 4, `docs/DEFINITIONS.md:128–187` | Established optical principle | Edmund Optics, “Focal Length” and “Field of View” sections; MIT, §5.3.1 | Verified | Supports the general optical principle; it does not establish a Working Focal Length formula. |
| Image coordinates require a defined and consistently registered frame for comparison. | Definition 6, `docs/DEFINITIONS.md:282–319`; Geometry Principle 4, `docs/GEOMETRY.md:210–300` | Established production practice / TPS operational requirement | Brown, *A Survey of Image Registration Techniques*, abstract record only | Unverified | Brown’s record identifies registration as a cross-image matching task, but the full relevant source was inaccessible and the TPS minimum registration requirement remains unverified. |
| Repeatability and reproducibility require stated measurement conditions. | Definition 7, `docs/DEFINITIONS.md:321–389`; UC-001, `docs/USE_CASES.md:50–60` | Established measurement practice | NIST TN 1297, Appendix D1.1.2–D1.1.3 | Verified | NIST directly defines repeatability and reproducibility in relation to measurement conditions; it does not establish TPS tolerances. |
| A TPS reference contains points, correspondence, image-frame information, triangle measurements, focus distance, and Working Focal Length. | `SPECIFICATION.md:26–32`; Definition 6, `docs/DEFINITIONS.md:250–319` | TPS-specific requirement | No external source asserted as authority | Unverified | This is an approved TPS requirement. Its reproducibility and adequacy require TPS research and validation. |
| A projection match does not uniquely recover camera pose or the complete camera configuration. | Observation 6, `docs/OBSERVATIONS.md:176–211`; Geometry Principle 3, `docs/GEOMETRY.md:135–208`; UC-001, `docs/USE_CASES.md:39–48` | TPS-specific geometric claim | Hartley and Zisserman, author-hosted book record and selected material; MIT, §5.3.1 | Partially supported | The sources establish perspective-camera geometry and multiple-view context, but the exact three-point ambiguity claim requires a dedicated derivation or experiment. |
| UC-001 can be tested by recording, moving or removing the camera, attempting recovery, and measuring correspondence errors. | `docs/USE_CASES.md:50–60` | TPS-specific proposed experiment | NIST TN 1297 for measurement terminology | Needs experiment | No experimental result is claimed; the proposed protocol must be executed and documented before performance claims are made. |

## Evidence Boundaries

The external sources support general mathematics, optics, image-registration context, and measurement terminology. They do not by themselves validate the TPS kernel, TPS reference contents, Working Focal Length, projection-match criteria, or UC-001 outcomes.

The TPS-specific requirements remain subject to research, derivation, and experiments in this repository.
