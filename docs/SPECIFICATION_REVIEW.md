# TPS Specification Review

**Review scope:** Final technical review before academic paper development.

**Reviewed revision:** `54a18cd760d2baf8438278195e1001921e38c6d8`

**Review conclusion:** TPS is a coherent practical view-matching framework, but it is not yet independently implementable as a fully specified measurement procedure. The conceptual model is strong; the remaining work is concentrated in coordinate registration, reference-record semantics, operational measurement conventions, and validation.

## Finding Categories

- **Blocking:** Prevents an independent implementation from making a consistent TPS reference or comparison.
- **Clarification:** Wording or definition needs improvement but does not necessarily prevent a prototype.
- **Research:** Requires derivation, source review, or experiment.
- **Editorial:** Presentation or organization only.

## Findings

### Blocking 1 — Image coordinate frame is required but not operationally specified

- **File and section:** `docs/DEFINITIONS.md`, Definition 6 — TPS Reference, “Image Coordinate Frame”; `docs/GEOMETRY.md`, Geometry Principle 4 — Projection Equivalence; `research/derivations/IMAGE_REGISTRATION.md`
- **Description:** TPS requires a consistently registered image coordinate frame, but does not define the minimum recorded information needed to reproduce that frame. Origin, axis directions, pixel-center convention, crop, scale, rotation, mirroring, and any transformation record are discussed in research but are not part of an operational specification.
- **Why it matters:** Independent implementations can record the same image points in incompatible coordinate systems and still claim to have created equivalent references.
- **Recommended correction:** Approve a concise minimum coordinate-frame record, using the concepts already developed in `IMAGE_REGISTRATION.md`. Do not prescribe a file format or a universal normalization convention.

### Blocking 2 — Reference input and recovery records are not fully defined

- **File and section:** `SPECIFICATION.md`, “TPS Reference Requirements” and “Working Focal Length”; `docs/DEFINITIONS.md`, Definition 6 — TPS Reference; `docs/USE_CASES.md`, UC-001 Method
- **Description:** The specification lists the required data, but does not define how the recorded reference identifies the designated reference plane, the sensor-plane distance measurement, roll-corrected coordinates, active sensor width, or retained calculation inputs.
- **Why it matters:** An independent implementation cannot reliably reproduce the Working Focal Length calculation or determine whether two reference records use compatible inputs.
- **Recommended correction:** Define the minimum semantic contents of each input and record, while leaving storage format and hardware open.

### Clarification 1 — Working Focal Length status is ambiguous

- **File and section:** `SPECIFICATION.md`, “Working Focal Length”; `docs/DEFINITIONS.md`, Definition 6; `research/derivations/WORKING_FOCAL_LENGTH.md`
- **Description:** The specification presents the formula as the TPS calculation, while the derivation states that it is not an approved mathematical formulation and is not experimentally validated.
- **Why it matters:** Readers may interpret the formula as a validated optical law rather than an approved TPS convention based on an idealized derivation.
- **Recommended correction:** Label the formula in the specification as an approved TPS calculation convention based on stated assumptions, and retain its approximation and non-validation status.

### Clarification 2 — “Roll correction” and physical A–B alignment are distinct but underspecified

- **File and section:** `SPECIFICATION.md`, “Working Focal Length”; `docs/DEFINITIONS.md`, Definition 6; `research/derivations/WORKING_FOCAL_LENGTH.md`, “A–B Orientation”
- **Description:** The specification correctly says roll correction does not fix physical A–B misalignment, but does not state how roll is identified or what “aligned as closely as practical” means.
- **Why it matters:** Different implementations may apply different rotations or use different physical alignment assumptions while calculating the same named quantity.
- **Recommended correction:** Define roll correction as a coordinate-frame operation recorded with the reference. Keep physical alignment as an approximation and do not add a universal angular threshold.

### Clarification 3 — Focus distance terminology needs separation from Working Focal Length inputs

- **File and section:** `docs/DEFINITIONS.md`, Definition 6; `SPECIFICATION.md`, TPS Reference Requirements
- **Description:** “Focus distance” is a required reference item, while `D` is the sensor-plane-to-reference-plane distance used by the Working Focal Length calculation. The documents do not explicitly state whether these are the same recorded quantity or two distinct quantities.
- **Why it matters:** An implementation could substitute a lens-reported focus distance, a subject distance, or a sensor-plane measurement without preserving the intended convention.
- **Recommended correction:** State whether focus distance and `D` are synonymous for TPS or are separate fields. Preserve the sensor-plane convention if that remains approved.

### Clarification 4 — “Projection match,” “projection equivalence,” and “closest practical match” overlap

- **File and section:** `docs/DEFINITIONS.md`, Definition 7; `docs/GEOMETRY.md`, Geometry Principle 4; `SPECIFICATION.md`, “Matching Principle”
- **Description:** These sections describe related comparison states but do not establish a concise relationship between exact equivalence, practical matching, and the user-directed closest practical match.
- **Why it matters:** Implementations may report different outcomes using the same terms.
- **Recommended correction:** Adopt a short terminology hierarchy: equivalence describes comparison in a common frame; exact match uses equality; practical match uses an operator- or user-selected tolerance; closest practical match is an adjustment objective, not a universal pass/fail condition.

### Clarification 5 — Physical triangle replacement cases are not connected to reference validity

- **File and section:** `docs/CONSTRAINTS.md`, “Operating Cases”; `docs/DEFINITIONS.md`, Definition 5 — Three-Point Projection
- **Description:** The three operating cases are documented, but the specification does not state which reference data remain authoritative when the same triangle is relocated or a different triangle is used.
- **Why it matters:** A replacement triangle may preserve, alter, or fail the physical relationships needed by a particular operation.
- **Recommended correction:** Define operation-specific reference validity later. Do not promote triangle similarity to a universal requirement.

### Research 1 — Working Focal Length and real-lens geometry

- **File and section:** `research/derivations/WORKING_FOCAL_LENGTH.md`, “Sensor Plane, Projection Center, and Focus Distance” and “Conditions for Exactness Within the Ideal Model”
- **Description:** The derivation shows exactness only under an ideal central-projection model and identifies sensor-plane distance, finite focus, principal-plane offsets, unequal depths, tilt, and distortion as limitations.
- **Why it matters:** The practical quantity may be reproducible without being identical to nominal or effective optical focal length.
- **Recommended correction:** Validate the convention experimentally across representative lenses and distances before presenting it as a general optical result.

### Research 2 — Unequal depths and reference-plane tilt

- **File and section:** `research/derivations/WORKING_FOCAL_LENGTH.md`, “Unequal Point Depths” and “Reference-Plane Tilt”
- **Description:** The derivation identifies bias but does not establish an accepted correction or an operational validity boundary.
- **Why it matters:** Small physical departures from equal depth may materially affect the recorded value.
- **Recommended correction:** Measure sensitivity experimentally and document conditions under which the approximation is usable. Do not invent a tolerance in this review.

### Research 3 — Registration transformations and false agreement

- **File and section:** `research/derivations/IMAGE_REGISTRATION.md`, “Registration Is Not Geometric Correction”; `docs/GEOMETRY.md`, Geometry Principle 4
- **Description:** The research derivation correctly prohibits choosing a transformation solely to force three points to agree, but no independent registration protocol or test exists.
- **Why it matters:** Three non-collinear points can determine a fitting transformation, so unconstrained registration can erase the measured difference.
- **Recommended correction:** Develop controlled registration experiments using known frame changes and deliberately nonmatching projections.

### Research 4 — Match evaluation and measurement uncertainty

- **File and section:** `docs/DEFINITIONS.md`, Definition 7 — Projection Match; `docs/USE_CASES.md`, Proposed Validation; `docs/VALIDATION.md`
- **Description:** Exact and practical matching are distinguished, but no TPS error metric, uncertainty budget, or repeatability study exists.
- **Why it matters:** A practical match cannot be interpreted or compared across setups without documented measurement conditions.
- **Recommended correction:** Use repeatability and reproducibility studies to characterize measurement behavior. Keep acceptance tolerances user- or operation-specific unless later approved.

### Research 5 — Projection ambiguity statement

- **File and section:** `docs/GEOMETRY.md`, Geometry Principle 3; `research/VERIFICATION_REPORT.md`
- **Description:** The uniform-scaling example supports non-uniqueness under an ideal model, but the full scope of three-point ambiguity under varying constraints remains only partially supported.
- **Why it matters:** The statement must not be broadened into a general camera-reconstruction theorem.
- **Recommended correction:** Retain the current scope and develop a formal derivation limited to the stated assumptions.

### Editorial 1 — Repeated scope exclusions

- **File and section:** `docs/OBSERVATIONS.md`, Observation 6; `docs/DEFINITIONS.md`, Definitions 5–7; `docs/GEOMETRY.md`, Principles 1–4; `docs/CONSTRAINTS.md`
- **Description:** Camera-pose, calibration, and complete-scene exclusions recur throughout the documents.
- **Why it matters:** The repetition is protective but makes the specification longer and can obscure the normative concepts.
- **Recommended correction:** Keep one canonical scope statement in `SPECIFICATION.md` and use focused cross-references elsewhere.

### Editorial 2 — Mathematical content is split between specification and research

- **File and section:** `SPECIFICATION.md`, “Mathematical Formulation”; `docs/GEOMETRY.md`; `research/derivations/`
- **Description:** The specification says mathematical formulation is reserved, while it now contains an approved calculation and geometry principles supported by research derivations.
- **Why it matters:** Readers may not know which equations are normative, provisional, or explanatory.
- **Recommended correction:** Clarify the relationship between approved mathematical conventions and research derivations without adding new mathematics.

### Editorial 3 — Research derivation notation is not consistently typeset

- **File and section:** `research/derivations/PHYSICAL_IMAGE_TRIANGLES.md`; `research/derivations/IMAGE_REGISTRATION.md`
- **Description:** Some inline mathematical notation appears as parenthesized plain text rather than consistently formatted mathematical notation.
- **Why it matters:** It reduces readability and makes independent checking harder, especially in the derivations.
- **Recommended correction:** Normalize notation in research documents only; do not alter approved specification wording.

## Completeness Assessment

### Complete enough for academic paper framing

- Purpose and scope are clear.
- The physical point, image point, correspondence, projection, reference, and match vocabulary exists.
- Camera reconstruction is explicitly excluded as the TPS objective.
- The reference contents and Working Focal Length convention are recorded.
- Research derivations identify assumptions and limitations.

### Not complete enough for independent conformance

- Coordinate-frame records are not fully specified.
- Reference input semantics are not fully specified.
- Practical matching has no common error or uncertainty description.
- Reference validity and failure conditions remain incomplete.
- Working Focal Length has no validated real-lens applicability boundary.

## Recommended Correction Order

1. Clarify reference-record semantics and coordinate-frame information.
2. Clarify focus distance versus `D`.
3. State the status of the Working Focal Length formula as a TPS convention under assumptions, not a universal optical identity.
4. Establish terminology for equivalence, exact match, practical match, and closest practical match.
5. Run registration, repeatability, and Working Focal Length experiments.
6. Consolidate repeated scope language after the technical distinctions stabilize.

No new requirements are introduced by this review.
