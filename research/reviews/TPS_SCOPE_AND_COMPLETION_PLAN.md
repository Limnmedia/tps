# TPS Scope and Completion Plan

**Repository:** `Limnmedia/tps`  
**Baseline reviewed:** `main` at the current synchronized repository state  
**Purpose:** Establish the smallest defensible path toward TPS Specification 1.0 and external technical review of Paper 1.

## 1. Repository purpose and scope

TPS is an open, implementation-independent method for recording and reproducing a camera view through correspondence between three identified physical reference points and their image projections:

```text
A → a
B → b
C → c
```

The repository has four responsibilities:

1. Define the TPS specification.
2. Document its mathematical foundations and assumptions.
3. Provide evidence of practical operation.
4. Support technical publication and independent implementation.

TPS is not a camera-pose solver, motion-control system, software application, or complete production pipeline. Camera recovery is an application of the TPS reference and correspondence system. LIMNTPS and LIMNTPS Align are implementations or supporting tools; their behavior does not define TPS.

The completion objective is therefore bounded: make the normative reference record and approved calculations sufficiently unambiguous for independent implementation, document their assumptions and limitations, complete the three planned physical demonstrations, and ensure Paper 1 describes the resulting contribution without overstating novelty or performance.

## 2. Document-authority hierarchy

### Normative

- `SPECIFICATION.md`
- Definitions, constraints, invariants, geometry, use-case, and validation statements explicitly incorporated by reference from the specification.

These documents define TPS terms, minimum reference contents, approved calculation conventions, recovery objective, and stated limitations. A research note or audit does not become normative merely because it is newer or more detailed.

### Supporting technical material

- `research/derivations/`
- `research/methods/`
- Measurement explanations and validation procedures/evidence.

This material explains, derives, tests, or operationalizes the specification. It may identify an ambiguity or propose a procedure, but it does not silently add requirements or redefine approved mathematics.

### Research and publication

- `research/papers/PAPER_01_REVISED.md`
- `research/BIBLIOGRAPHY.md`
- `research/EVIDENCE_MAP.md`
- `research/PRIOR_ART_REVIEW.md`
- `research/INTERDISCIPLINARY_PRIOR_ART.md`
- `research/reviews/`

These documents position TPS, assess prior art, record evidence boundaries, and prepare publication. They may distinguish established practice, proposed TPS organization, and unvalidated claims; they do not override the specification.

### Historical and exploratory

- Research notes, audits, proposed extensions, superseded investigations, and exploratory application material.

These records preserve reasoning and research history. They are not specification requirements unless deliberately reviewed and incorporated into the normative documents.

### Authority issues to clarify

The hierarchy is conceptually present but not stated in one repository-level policy document. Two wording issues could confuse readers:

- `research/README.md` says the specification states validated mathematical relationships, while `SPECIFICATION.md` says the candidate is not yet experimentally validated. The intended meaning appears to be approved conventions based on stated assumptions, not validated real-world performance.
- `docs/VALIDATION.md` remains a placeholder, while validation procedures exist in research methods and the physical-validation draft. The draft is supporting material, not an incorporated normative requirement.

These are documentation-clarity issues, not reasons to redesign the repository. A short authority statement can be added later if needed.

## 3. Established TPS baseline

The approved baseline should remain unchanged during this completion pass:

- There is one Base Pair: A–B.
- C is the third spatial reference point.
- A TPS reference preserves A/B/C identity, a/b/c image locations, explicit correspondence, physical triangle relationships, image-coordinate information, captured image dimensions, TPS Reference Distance, and Working Focal Length inputs/value as specified.
- The Working Focal Length equations remain the existing TPS calculation conventions under their stated assumptions.
- Recovery compares a registered reference with a live view and seeks the closest practical reproduction.
- Three-point agreement does not establish a unique camera pose, complete camera recovery, or whole-image agreement.
- No fixed camera-control sequence, alternative Base Pair, new geometric model, or universal acceptance threshold is required.

The three planned physical demonstrations are also bounded:

1. **Camera recovery:** record a view and TPS reference, move the camera, and recover the view on the same physical setup.
2. **View transfer:** transfer a recorded view to a second physical setup using TPS.
3. **Scale variation:** repeat view transfer with a declared physical-scale or capture-geometry change.

Each produces an original image, a recovered image, TPS measurements, and operator observations. Registered visual comparison is the primary practical evidence. Numerical measurements support interpretation but do not create arbitrary pass/fail thresholds.

## 4. Genuine completion blockers — category A

These are the smallest issues that can prevent an independent implementation or make a technical description materially ambiguous. They should be resolved before declaring the specification complete.

### A1. TPS Reference Distance and focus-distance field semantics

**Affected files:** `SPECIFICATION.md`, `docs/DEFINITIONS.md`, `research/derivations/WORKING_FOCAL_LENGTH.md`  
**Issue:** The specification defines D as a sensor-plane-to-designated-reference-plane distance, while definitions and research discussions also refer to focus distance and possible midpoint targeting. The documents do not state unambiguously whether “focus distance” is a separate recorded field, whether D is measured to a point or plane in the operational procedure, or which endpoint construction an implementation must preserve.

**Why it blocks:** D appears in the approved Working Focal Length and AOV conventions. Two independent implementations could record different quantities under the same TPS field name and calculate different results.

**Smallest correction:** State explicitly that focus distance and D are separate fields or formally declare them synonymous. Then define the approved D endpoints and measurement direction in one normative sentence, while retaining the existing approximation caveat. Do not add a new geometric model or change the equations.

### A2. Reference validity for the second physical setup

**Affected files:** `docs/DEFINITIONS.md`, `docs/CONSTRAINTS.md`, `docs/USE_CASES.md`, supporting validation protocol  
**Issue:** The specification permits physical reference points, triangle measurements, and recovery, but does not give a concise rule for which reference information remains authoritative when a view is transferred to a second setup or when the physical triangle is reproduced.

**Why it blocks:** Test 2 cannot be independently implemented consistently unless the operator knows whether the second setup must reproduce the same A/B/C relationships, which fields are transferred unchanged, and which are newly measured. This is an operational reference-validity issue, not a requirement for triangle similarity in all TPS uses.

**Smallest correction:** Add a narrow operating-case statement: for view transfer, preserve point identity and declare the physical relationships and any changed scale or setup condition; do not imply that a different triangle is equivalent without documenting the relationship. Keep triangle similarity optional unless separately justified.

### A3. Incorporation status of physical validation evidence

**Affected files:** `docs/VALIDATION.md`, supporting physical-validation draft, `SPECIFICATION.md`  
**Issue:** The candidate specification and repository reviews correctly state that practical performance is unvalidated, but the public validation document is still a placeholder while a draft three-test protocol exists in research reviews.

**Why it blocks:** This blocks a claim of completed practical validation and weakens external review if the repository does not clearly identify the protocol, evidence location, and status. It does not block the mathematical definition of TPS 1.0 if the specification explicitly remains a candidate pending validation.

**Smallest correction:** Adopt or summarize the three-test protocol in the validation document, preserving its draft/non-normative status until results exist. Record original/recovered images, measurements, and observations as evidence. Do not claim that tests have been performed until the artifacts exist.

### Blocker boundary

A1–A2 are specification-completion blockers because they affect independent interpretation of a calculation or transfer procedure. A3 is a publication/evidence blocker for any claim that TPS has been physically validated; it is not a reason to invent additional tests or mathematical requirements. Camera tilt and roll remain recorded recovery measurements, not Working Focal Length inputs or completion blockers. No other current research question should be promoted to category A without showing a direct implementation ambiguity or an unsupported Paper 1 claim.

## 5. Minimum completion checklist

### Specification 1.0

- [ ] Confirm that `SPECIFICATION.md` remains the sole normative entry point.
- [ ] Resolve D versus focus-distance semantics and the approved D measurement convention.
- [ ] State the validity/recording rule for Test 2 view transfer and declared scale variation.
- [ ] Preserve the single A–B Base Pair, C, existing equations, existing assumptions, and implementation independence.
- [ ] Keep practical match, exact equivalence, and whole-image limitations distinct.
- [ ] Ensure research notes and audits are not silently incorporated as requirements.

### Physical evidence

- [ ] Finalize the concise three-test protocol without adding physical cases.
- [ ] Perform Test 1: same-setup camera recovery.
- [ ] Perform Test 2: second-setup view transfer.
- [ ] Perform Test 3: declared physical-scale or image-gate variation, with the two cases distinguished.
- [ ] Preserve original and recovered images, registered comparisons, TPS measurements, and operator observations.
- [ ] Report numerical measurements as supporting evidence, without inventing a universal tolerance.
- [ ] State clearly which tests were performed and which remain planned.

### Paper 1

- [ ] Describe the practical problem, TPS reference, mathematical foundation, related methods, evidence status, assumptions, and limitations.
- [ ] Keep the contribution methodological and organizational; do not require mathematical novelty.
- [ ] Align Related Work with the existing prior-art audit, especially the substantial overlap with P3P/PnP, VFX lineup, registration, rephotography, and overlays.
- [ ] Describe physical validation only to the extent supported by completed evidence.
- [ ] Keep virtual camera-path registration, production philosophy, and broader creative implications as scoped applications or future work.
- [ ] Remove or qualify any wording that could imply a unique pose, whole-image recovery, demonstrated superiority, or established originality.

### Attribution

- [x] Paper 1 identifies **Christopher Weinberg** and **LIMNMEDIA**.
- [x] The README and contributing guidance identify LIMNMEDIA as developing/maintaining the open specification and distinguish TPS from LIMNTPS and LIMNTPS Align.
- [x] Git commit authorship is separate metadata and currently records Christopher Weinberg; no Git-history change is required.
- [ ] If external publication adds coauthors, affiliations, or contributor roles, record those in the paper and publication metadata separately from repository commit authorship.

## 6. Category B — nonblocking work

These improvements may increase clarity or reviewability but do not prevent the bounded specification or Paper 1 from proceeding:

- Add a short document-authority statement to `research/README.md` or the top-level README.
- Replace the validation placeholder with the already drafted three-test protocol and evidence template.
- Add a concise terminology hierarchy for projection, equivalence, exact match, practical match, and closest practical match.
- Add the existing OpenCV camera-calibration source to Paper 1’s Related Work citations if the calibration comparison remains substantive.
- Cross-reference the Related Work audit and context synchronization audit from research navigation material.
- Normalize notation or headings in research documents where it improves readability.

These changes should remain editorial or incorporative. They should not add alternative Base Pairs, new equations, universal tolerances, or new production requirements.

## 7. Category C — explicitly deferred work

The following are outside the minimum completion path:

- Broad patent, historical optical-viewfinder, cinematography-manual, and proprietary production prior-art searches beyond the existing bounded audit.
- Claims of originality, non-obviousness, superiority, or priority.
- Real-lens characterization of Working Focal Length across many lenses, focus states, distances, distortion profiles, or sensor formats beyond what is needed to document the current limitation.
- A universal error metric, uncertainty budget, or acceptance threshold.
- Automatic camera solving, PnP implementation, optimization, Jacobian-based software assistance, or motion-control integration.
- Virtual camera-path registration and transformation of complete six-degree-of-freedom paths.
- Broader production philosophy, diegetic continuity, stop-motion theory, or a general theory of production practice.
- Product features in LIMNTPS or LIMNTPS Align.
- Repository reorganization unless the authority hierarchy becomes impossible to navigate without it.

These may be valuable future research or applications, but none is required to finish defining the current TPS method or prepare Paper 1 for a technically honest external review.

## Recommended completion order

1. Resolve A1–A3 with explicit, minimal normative wording.
2. Keep the existing equations and definitions unchanged except for clarifying field semantics and recorded conventions.
3. Adopt the three-test physical validation protocol as supporting material and perform the tests when practical.
4. Update Paper 1 only to reflect completed evidence and the bounded methodological contribution.
5. Perform a final authority, attribution, citation, and limitation review before external technical submission.

## Conclusion

TPS is close to a defensible documentation-completion path. The repository already contains the core definitions, correspondence model, calculation conventions, scope exclusions, prior-art context, and a simple three-test validation plan. The remaining work should be limited to a few implementation-critical conventions, explicit evidence status, and careful publication wording.

The guiding boundary is simple: a documented limitation is not an unfinished specification, a proposed experiment is not completed evidence, and a research note is not a requirement. The path to TPS Specification 1.0 is to resolve only the ambiguities that would cause independent implementations to diverge, then document the three planned demonstrations without expanding the system.
