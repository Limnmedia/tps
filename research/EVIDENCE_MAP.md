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
| Three distinct noncollinear points form a triangle. | `docs/OBSERVATIONS.md:9–27`; Definition 1 in `docs/DEFINITIONS.md:9–43` | Established mathematics | OpenStax, *Contemporary Mathematics*, §10.3 | Verified | Supports the general geometric fact, not any TPS operation. |
| Uniform scaling preserves corresponding side-length ratios and internal angles. | Invariant 2, `docs/INVARIANTS.md:60–97` | Established mathematics | OpenStax, *Contemporary Mathematics*, §10.3 | Verified for triangle similarity | Does not establish that TPS universally requires similar replacement triangles. |
| A physical point can be represented at a location in a two-dimensional image. | Observations 2–3, `docs/OBSERVATIONS.md:29–96`; Definitions 1–2, `docs/DEFINITIONS.md:9–83` | Established optical principle | MIT, *Foundations of Computer Vision*, Chapter 5 | Verified | The source describes pinhole and perspective models; TPS remains implementation-independent. |
| Perspective projection depends on point depth and camera parameters. | Geometry Principle 2, `docs/GEOMETRY.md:66–133` | Established optical principle | MIT, *Foundations of Computer Vision*, Chapter 5 | Verified | Supports the ideal perspective model only; it does not validate every real camera system. |
| Perspective projection does not generally preserve physical triangle shape. | Geometry Principle 1, `docs/GEOMETRY.md:9–64` | Established optical principle | MIT, *Foundations of Computer Vision*, Chapter 5; OpenStax, §10.3 | Examined support; TPS claim remains to be formally derived | The sources support perspective scaling and triangle geometry, but no source was used as a complete proof of the exact TPS wording. |
| Focal length affects field of view and image formation. | Observation 4, `docs/OBSERVATIONS.md:98–137`; Definition 4, `docs/DEFINITIONS.md:128–187` | Established optical principle | Edmund Optics, *Understanding Focal Length and Field of View*; MIT, Chapter 5 | Verified for the general optical principle | Does not establish a Working Focal Length formula. |
| Image coordinates require a defined and consistently registered frame for comparison. | Definition 6, `docs/DEFINITIONS.md:282–319`; Geometry Principle 4, `docs/GEOMETRY.md:210–300` | Established production practice / TPS operational requirement | Brown, *A Survey of Image Registration Techniques* | TPS-specific requirement; source identified but not examined | Registration is a recognized image-processing problem, but the TPS minimum registration requirement needs its own specification and validation. |
| Repeatability and reproducibility require stated measurement conditions. | Definition 7, `docs/DEFINITIONS.md:321–389`; UC-001, `docs/USE_CASES.md:50–60` | Established measurement practice | NIST TN 1297, Appendix D1 | Verified | Supports terminology and the need to state changed conditions; it does not establish TPS tolerances. |
| A TPS reference contains points, correspondence, image-frame information, triangle measurements, focus distance, and Working Focal Length. | `SPECIFICATION.md:26–32`; Definition 6, `docs/DEFINITIONS.md:250–319` | TPS-specific requirement | No external source asserted as authority | Not externally verified | This is an approved TPS requirement. Its reproducibility and adequacy require TPS research and validation. |
| A projection match does not uniquely recover camera pose or the complete camera configuration. | Observation 6, `docs/OBSERVATIONS.md:176–211`; Geometry Principle 3, `docs/GEOMETRY.md:135–208`; UC-001, `docs/USE_CASES.md:39–48` | TPS-specific geometric claim | Hartley and Zisserman, *Multiple View Geometry*; MIT, Chapter 5 | Hypothesis requiring TPS derivation and validation | The sources establish camera geometry as a field, but no source was used here to prove the exact three-point ambiguity claim. |
| UC-001 can be tested by recording, moving or removing the camera, attempting recovery, and measuring correspondence errors. | `docs/USE_CASES.md:50–60` | TPS-specific proposed experiment | NIST TN 1297 for measurement terminology | Proposed experiment | No experimental result is claimed. |

## Evidence Boundaries

The external sources support general mathematics, optics, image-registration context, and measurement terminology. They do not by themselves validate the TPS kernel, TPS reference contents, Working Focal Length, projection-match criteria, or UC-001 outcomes.

The TPS-specific requirements remain subject to research, derivation, and experiments in this repository.
