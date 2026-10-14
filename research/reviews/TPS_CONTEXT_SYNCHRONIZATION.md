# TPS Context Synchronization Audit

**Scope:** Synchronize recent design context with the existing TPS specification, Paper 1, mathematical derivations, validation material, and Related Work audit.  
**Status:** Research and documentation audit; not a specification amendment.  
**Files reviewed:** `SPECIFICATION.md`, `research/papers/PAPER_01_REVISED.md`, `docs/USE_CASES.md`, `docs/VALIDATION.md`, `docs/DEFINITIONS.md`, `research/methods/TPS_CAMERA_LINEUP_GEOMETRY.md`, `research/methods/TPS_LINEUP_MATHEMATICAL_VERIFICATION.md`, `research/methods/TPS_PHYSICAL_LINEUP_PROCEDURE_REVIEW.md`, and `research/reviews/PAPER_01_RELATED_WORK_AUDIT.md`.

## Executive summary

The recent design discussions add useful operational context, but most of it belongs in research methods and validation material rather than in the normative specification. The existing repository already contains much of the conceptual distinction: TPS preserves physical/image correspondence; recovery is a practical view-matching application; mathematical verification, physical camera recovery, and production workflow are separate concerns.

The main synchronization gaps are:

- The sequential lineup procedure is documented in research methods, but its operator-facing order and status as a conditional heuristic are not yet consolidated into a validation protocol.
- The intended reference-distance target—an estimated midpoint of the A–B Base Pair—is more specific than the current normative wording, which says “designated physical reference plane.” The distinction must be resolved before any normative edit.
- The inclinometer procedure is mentioned in research material, but the exact instrument orientation and angle convention remain open for author verification.
- The four mathematical test cases—horizontal, vertical, diagonal, and gate-scaling—are not presently summarized as calculation exercises separate from physical camera recovery.
- The repository’s validation material already supports separating original/recovered images, point residuals, and off-triangle observations. It should explicitly make the images and visual registration the primary evidence for an observational procedure, without treating numerical residuals as a universal acceptance threshold.
- Virtual camera-path registration is present as a research-method concern for moving cameras, but the distinction between recovering one view and transforming a complete six-degree-of-freedom virtual camera path is not yet consolidated in a public research document.
- Production origins and the use of existing scene features versus deliberate markers appear in Paper 1 and definitions, but the broader production philosophy should remain outside the mathematical specification, primarily in workflow/education or a future book.

The practical next step is a small documentation pass centered on a validation protocol and a research-method clarification. No immediate change to the normative specification is required, and none is recommended until the reference-distance and inclinometer conventions are confirmed.

## Classification used in this audit

- **Established practice or mathematics:** Supported by existing mathematical documentation, production references, or a clearly stated camera/measurement principle. This status does not validate TPS performance.
- **Proposed TPS formalization:** A TPS-specific organization, convention, workflow, or record requirement built from established components but not thereby established as novel or experimentally superior.
- **Unvalidated:** A performance, repeatability, convergence, or interoperability claim that requires controlled physical or virtual experiments.
- **Open author decision:** A convention whose exact meaning is not sufficiently settled for normative use.

## 1. Sequential TPS lineup methodology

### Context supplied

The proposed sequence is: establish tilt and reference distance, align A/B, introduce C, then refine the image registration through observation. The method is intended as a practical, sequential geometric procedure rather than a camera-pose calculation.

### Already documented

- `TPS_CAMERA_LINEUP_GEOMETRY.md` describes an A-side/base-pair procedure, registration of A/B, a C phase, iterative refinement, and observation of residuals.
- `TPS_LINEUP_MATHEMATICAL_VERIFICATION.md` states that the A–B → C sequence is mathematically plausible as a staged operator heuristic, but not universally optimal, uniquely determined, or proven to converge.
- The physical lineup procedure review describes restoring tilt, optical state, roll condition, Working Focal Length, and the D relationship as initial conditions, followed by observation of A/B residuals and then C.
- `SPECIFICATION.md` defines recovery as registered comparison with a live camera view and does not prescribe a universal adjustment sequence.
- Paper 1 already states that A–B can provide initial alignment, C adds information, controls are coupled, and no fixed sequence is required.

### Missing or inconsistent

- The sequence is distributed across research-method files rather than represented as a single validation protocol with inputs, observations, actions, and outputs.
- “Establish tilt and reference distance” may sound like a solved geometric initialization. Existing method notes correctly describe these as practical initial conditions, not a recovered pose.
- “Refine the image registration through observation” needs careful wording. Registration of the reference frame should be declared or independently established; the operator should refine camera alignment while observing registered residuals, not fit a transformation merely to force mismatching points to agree.
- The current materials do not define a required order, and the mathematical verification explicitly warns that A/B-first and C-second are a proposed heuristic rather than a theorem.

### Recommended placement

**Primary:** `docs/VALIDATION.md` or a dedicated research validation protocol.  
**Secondary:** `research/methods/TPS_PHYSICAL_LINEUP_PROCEDURE_REVIEW.md` for operator detail.  
**Paper 1:** one concise description in the method/recovery section, labeled as a proposed workflow and not a universal sequence.  
**Specification:** retain only the current non-prescriptive recovery objective unless the procedure is later approved as normative.

### Classification

The underlying projection and coupled-control principles are established. The sequential A–B → C organization is a **proposed TPS formalization**. Its usability, convergence, and superiority over other adjustment orders are **unvalidated**.

## 2. Measurement conventions

### Context supplied

The intended convention is that reference distance is measured from a mark on the camera sensor plane toward the estimated midpoint of the Base Pair. Tilt and roll are measured with an inclinometer held square to the camera.

### Already documented

- `SPECIFICATION.md` defines the TPS Reference Distance as measured from the camera sensor plane to a designated physical reference plane and explicitly distinguishes it from focus distance, projection-center distance, and a manufacturer-reported focus distance.
- `docs/DEFINITIONS.md` repeats the sensor-plane convention and states that the value is practical and approximate.
- `TPS_PHYSICAL_LINEUP_PROCEDURE_REVIEW.md` says that D is measured from a sensor-plane mark to a practical reference location associated with A–B, and lists A, B, midpoint, or estimated midpoint as possible targets.
- `TPS_LINEUP_MATHEMATICAL_VERIFICATION.md` identifies the estimated A–B midpoint as a clarified operator convention but warns that it does not automatically establish a slanted hypotenuse or an optical-axis distance.
- The methods documents discuss tilt and roll measurement, instrument orientation, camera roll, and the need to declare an inclinometer procedure.

### Missing or inconsistent

- The normative specification says “designated physical reference plane,” while the recent context says “estimated midpoint of the Base Pair.” A point target and a plane target are not automatically the same measurement. This is a real convention discrepancy, not merely editorial wording.
- “Toward the estimated midpoint” does not yet state whether D is a straight tape distance, an axis-parallel distance, or a sensor-plane-to-plane distance. The methods document lists this as open author verification.
- “Held square to the camera” is not yet defined in relation to the camera body, image plane, optical axis, gravity, or the instrument’s own reference axes. It should not be promoted to normative language without that definition.
- The existing derivation warns that a tilt triangle using D as a hypotenuse is conditional. The measurement convention must not silently change the approved Working Focal Length equations.

### Recommended placement

**Primary:** research-method procedure plus a measurement-convention appendix or validation protocol.  
**Specification:** only after the endpoints, axes, instrument orientation, and D semantics are author-confirmed and tested.  
**Paper 1:** describe the convention as a practical measurement under stated assumptions; do not present it as a universal optical distance.  
**Education:** provide a diagram and operator example after the normative meaning is settled.

### Classification

Sensor-plane measurement and the distinction from nominal focus distance are established/documented TPS conventions. The midpoint target and square-inclinometer procedure are **proposed formalizations** that currently include an **open author decision**. Their measurement uncertainty and usefulness are **unvalidated**.

## 3. Mathematical test cases and physical validation

### Context supplied

There is one Base Pair: A–B. C is the third spatial reference point. The horizontal, vertical, diagonal, and gate-scaling cases are mathematical exercises for checking calculations and assumptions. They are not four physical camera setups, alternative Base Pairs, or separate physical recovery protocols.

### Already documented

- `docs/VALIDATION.md` explicitly separates mathematical verification from physical camera experiments but is currently a placeholder.
- `docs/USE_CASES.md` proposes the relevant physical experiment: record a reference, move or remove the camera, attempt recovery, and compare the result.
- `TPS_CAMERA_LINEUP_GEOMETRY.md` and `TPS_LINEUP_MATHEMATICAL_VERIFICATION.md` contain mathematical checks and proposed operator observations, but do not establish four physical setups.
- The mathematical verification report states that the staged lineup needs experiments and that whole-image agreement is not implied by three-point agreement.

### Missing or inconsistent

- The four mathematical cases are not presently documented together as calculation exercises with their assumptions and expected outputs.
- The physical recovery procedure is not a four-case matrix. It is one procedure using the one Base Pair A–B and third point C.
- The current methods document lists numerical metrics, but the recent context correctly emphasizes that original and recovered images are the primary evidence for an observational procedure. Numerical measurements should characterize the evidence, not replace visual registration or impose an unsupported universal threshold.
- “Gate scaling” may still require a mathematical definition in the calculation notes, but it should not be turned into an additional physical recovery setup unless separately requested and defined.

### Recommended placement

**Mathematical cases:** keep the four cases in the mathematical verification or calculation notes, with their assumptions and expected outputs.  
**Physical validation:** replace the placeholder in `docs/VALIDATION.md` with one simple protocol: record a TPS reference, move the camera, recover the view, and compare the original and recovered images.  
**Research methods:** retain geometry-specific observations and optional numerical descriptors without converting them into additional physical setups.  
**Paper 1:** summarize the physical recovery design and its limits; do not report results until experiments exist.  
**Specification:** link to validation requirements without embedding the experimental procedure in the candidate baseline.  
**Education:** explain the single Base Pair and C workflow with a practical example.

### Simplified physical validation

1. Record one TPS reference containing A, B, C, their correspondence, physical measurements, image coordinates, and applicable camera-reference information.
2. Move or remove the camera while preserving or documenting the physical reference points.
3. Recover the view using registered visual comparison and the proposed lineup observations.
4. Compare the original and recovered images, including A/B/C and visible scene features outside the triangle.
5. Preserve the images, registration information, observations, and optional numerical descriptors. Do not impose a universal numerical tolerance that has not been validated.

### Classification

The distinction between mathematical verification and physical recovery is **established repository practice**. The four mathematical cases are **proposed calculation exercises**. The single moved-camera recovery procedure is a **proposed physical validation protocol**. Accuracy, repeatability, reproducibility, and the evidentiary value of the procedure are **unvalidated**.

## 4. Validation evidence and observational acceptance

### Context supplied

Original and recovered images are the primary evidence. Measurements constrain the initial lineup; visual registration completes it. The procedure should not be forced into artificial numerical precision requirements when the operational result is observational.

### Already documented

- `SPECIFICATION.md` defines recovery as registered live-view comparison and the objective as the closest practical reproduction of the recorded view.
- Paper 1 states that recovery uses a registered reference, camera adjustment, and practical comparison; it also says that three-point agreement does not establish whole-image agreement.
- `TPS_CAMERA_LINEUP_GEOMETRY.md` requires examination of scene features outside A/B/C and recommends recording point residuals and whole-image observations.
- The methods document explicitly says to define acceptable tolerances per shot and not invent a universal TPS threshold.
- `docs/VALIDATION.md` states that mathematical verification and physical camera experiments are distinct, but does not yet provide the evidence hierarchy.

### Missing or inconsistent

- The repository does not yet state in one place that original/recovered image pairs are primary evidence and numerical measures are supporting descriptors.
- “Visual registration completes it” should not imply that subjective judgment replaces declared frame registration or physical measurements. The intended distinction is that measurements establish initial conditions and the final practical judgment is made by comparing registered images.
- A protocol is needed for preserving original and recovered images, metadata, overlay/difference views, point annotations, and observations outside the triangle.
- The term “observational procedure” needs an explicit reporting model: what the operator saw, what was adjusted, what remained mismatched, and whether the result was operationally acceptable for the stated shot.

### Recommended placement

**Primary:** `docs/VALIDATION.md`, with an image/evidence reporting template.  
**Research methods:** define optional numerical descriptors and uncertainty reporting.  
**Paper 1:** state that images and registered comparison are the practical evidence while accuracy claims remain unvalidated.  
**Specification:** retain the closest-practical-match language and no universal tolerance; do not require subjective acceptance as a normative mathematical criterion.

### Classification

Registered visual comparison and measurement-assisted setup are **established operational practices**. The evidence hierarchy and observational acceptance model are a **proposed TPS validation formalization**. The relationship between three-point residuals, visual whole-image agreement, and operator acceptance is **unvalidated**.

## 5. Virtual camera-path registration

### Context supplied

Recovering a single camera view is distinct from using a six-degree-of-freedom camera position to transform an entire virtual camera path into stage coordinates.

### Already documented

- `TPS_CAMERA_LINEUP_GEOMETRY.md` warns that one reference frame may be insufficient for a whole motion-control path and recommends sampling multiple frames and examining A/B/C and other scene features along the path.
- The same document distinguishes manual camera, motion-control crane, and Blender/Maya implementations. It states that TPS does not require a common origin, automatic PnP solve, or a specific DCC.
- Paper 1 and the specification focus primarily on reproducing a recorded view and explicitly avoid claiming complete camera-pose recovery.
- The Related Work audit distinguishes TPS from VFX matchmoving, which generally seeks a solved virtual camera, tracked scene, lens model, or renderable production solution.

### Missing or inconsistent

- The repository does not yet define “virtual camera-path registration” as a separate application or state whether it is in scope for TPS, a future implementation, or a research extension.
- A six-degree-of-freedom camera transform for one pose is not automatically a validated transform for an entire path. The path also requires frame timing, lens state, pivot/rig kinematics, coordinate origins, scale, and possibly distortion conventions.
- “Transform an entire virtual camera path into stage coordinates” can sound like a solved camera reconstruction or scene-registration claim. It should be framed as a possible implementation/application requiring path-level validation.
- The current specification’s view objective and the path-level objective should not be conflated.

### Recommended placement

**Primary:** future implementation/research method or a separate virtual-production application note.  
**Validation:** a moving-camera protocol with multiple sampled frames, path continuity, and off-triangle features.  
**Paper 1:** at most a brief scope distinction in Discussion or Future Validation; do not make it a core TPS requirement.  
**Specification:** do not add it to the candidate baseline until path semantics and validation are defined.

### Classification

Six-degree-of-freedom camera transforms and path registration are **established concepts** in camera/graphics workflows. Applying them to TPS as a whole-path registration workflow is a **proposed extension**. Path-level accuracy, continuity, and scene-coordinate recovery are **unvalidated**.

## 6. Production origins and workflow context

### Context supplied

TPS accommodates existing scene features as well as deliberately placed markers. Its software independence is intentional. The broader production philosophy belongs primarily in the book, not the mathematical specification.

### Already documented

- `docs/DEFINITIONS.md` allows a physical point to be a corner, mark, or identifiable feature and separately describes a physical marker; it does not require dedicated markers.
- Paper 1’s recording section says that points need not be dedicated markers and may be suitable corners or set features if their identities are unambiguous and their intended relationships remain usable.
- The specification states that no particular file format, software convention, overlay technology, or camera is mandatory, and that the recovery camera need not be identical to the original.
- Paper 1 contains a production-context section that distinguishes professional experience from formal TPS development and avoids studio endorsement or ownership claims.
- The README and specification distinguish TPS from LIMNTPS and LIMNTPS Align implementations.

### Missing or inconsistent

- The exact distinction between “existing scene feature” and “deliberately placed marker” is spread across definitions, Paper 1, and workflow documents rather than summarized in one operational note.
- The phrase “software independence” is clear as a design objective, but cross-tool interoperability remains unvalidated. The Related Work audit already recommends treating portability as proposed design intent rather than demonstrated performance.
- Production philosophy, historical origins, and broader claims about how artists should work should not be inserted into the mathematical specification. Paper 1 can retain a bounded production-context paragraph; a future book can carry the wider philosophy and examples.
- The repository should avoid implying that professional production origins constitute prior art, studio endorsement, or proof of technical performance.

### Recommended placement

**Specification:** retain the implementation-independent reference requirements and marker/feature neutrality; avoid broader philosophy.  
**Paper 1:** retain concise production context and the feature-versus-marker distinction where it explains the practical problem.  
**Education:** provide examples of corners, set features, and placed markers.  
**Future book:** hold the broader production philosophy, history, and workflow narratives.  
**Research/validation:** test whether feature type, visibility, repeatability, and physical stability affect recovery.

### Classification

Using existing features or placed markers is a **proposed workflow accommodation** grounded in ordinary production practice. Software independence is a **TPS design objective/formalization**. Cross-tool portability, production usefulness, and any connection between professional origins and improved performance are **unvalidated** or outside the specification’s scope.

## Cross-cutting terminology and scope guardrails

The following hierarchy should remain stable:

```text
Physical/image correspondence
        ↓
TPS reference and preserved measurement context
        ↓
Registered geometric comparison
        ↓
Iterative physical camera alignment
        ↓
Practical reproduction of a recorded view
```

This hierarchy should not be collapsed into:

```text
Three correspondences → unique camera pose → complete image/path recovery
```

The latter implication is not established and is expressly inconsistent with the current specification and research limitations. P3P/PnP and conventional VFX matchmoving remain relevant prior art because they share inputs or operational elements, but their camera-solving and scene/path objectives differ from TPS’s stated reference-and-view objective. That is a methodological distinction, not by itself a claim of mathematical novelty.

Recommended vocabulary:

- Use **recorded view** for the practical objective.
- Use **projection** for the mathematical relationship between physical points and image locations.
- Use **physical camera recovery** for the manual or physical-camera application.
- Use **virtual camera-path registration** only for a separately scoped path-level application.
- Use **visual registration** for comparison in a declared common image frame; do not use it to mean arbitrary fitting that forces agreement.
- Use **Base Pair** only for the single A–B pair. Its role in the Working Focal Length calculation and lineup procedure should not be mistaken for an alternative three-point configuration; C remains the third spatial reference point.

## Smallest necessary documentation changes

1. Expand `docs/VALIDATION.md` from its placeholder into a validation protocol containing the four cases, original/recovered image evidence, declared frame registration, optional numerical descriptors, and no universal tolerance.
2. Add a short cross-reference in the physical lineup method that identifies the A–B → C sequence as a proposed, conditional operator heuristic and points to the validation protocol.
3. Resolve the D endpoint and inclinometer orientation convention before changing `SPECIFICATION.md` or `docs/DEFINITIONS.md`. Until then, keep the normative “designated physical reference plane” wording and mark the midpoint procedure as an operational proposal.
4. Add a separate research note or application subsection for virtual camera-path registration if that work is to continue; do not fold it into the core three-point recovery requirement.
5. Keep feature-versus-marker accommodation and software independence in the specification at the narrow information/implementation level; place broader production philosophy in educational material or the future book.
6. Add a limited Paper 1 cross-reference only after the validation protocol exists. Do not add performance or originality claims based on the synchronization discussion alone.

## Open decisions before normative changes

- Is D measured to a point near the estimated A–B midpoint, to a designated plane, or by another explicitly defined construction?
- Is D a straight-line measurement, an optical-axis measurement, or a sensor-plane-to-plane measurement for each approved equation?
- What does “inclinometer held square to the camera” mean operationally, and how are camera roll and instrument axes recorded?
- What assumptions and expected outputs define the horizontal, vertical, diagonal, and gate-scaling calculation exercises?
- Is virtual camera-path registration an intended TPS application, a software implementation feature, or a separate research project?
- Which parts of the production-origin narrative belong in Paper 1, and which should be reserved for educational or book material?

## Conclusion

The recent context does not require undoing the Related Work audit or changing the current specification. It supplies missing operational and validation context that should be synchronized first in research-method and validation documents. The most important boundary is that TPS is a correspondence-and-reference system whose camera recovery is an application; a virtual camera path, a pose solve, and whole-image agreement are larger applications or claims requiring their own scope and evidence.

The recommended synchronization order is:

1. Resolve the D and inclinometer conventions.
2. Define the four mathematical calculation exercises and the single physical recovery protocol with its evidence hierarchy.
3. Cross-reference the conditional A–B → C lineup method.
4. Scope virtual camera-path registration separately.
5. Only then consider minimal Paper 1 or specification updates.
