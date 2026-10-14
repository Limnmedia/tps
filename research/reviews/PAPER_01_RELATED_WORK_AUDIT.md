# Paper 1 Related Work Audit

**Document audited:** `research/papers/PAPER_01_REVISED.md`  
**Section audited:** “Related Work”  
**Supporting records:** `research/BIBLIOGRAPHY.md`, `research/EVIDENCE_MAP.md`, `research/PRIOR_ART_REVIEW.md`, `research/INTERDISCIPLINARY_PRIOR_ART.md`, the two TPS lineup-method documents, and `SPECIFICATION.md`  
**Audit status:** Local-repository audit; no new source or originality claim is introduced.

## A. Executive summary

The Related Work section is directionally sound and its central distinction is well supported: photogrammetry and PnP use physical-to-image correspondences for camera or pose estimation, while TPS proposes to preserve such correspondences as an implementation-independent reference for practical view reproduction. The section also correctly identifies image registration, rephotography, fiducial registration, VFX survey/lineup, and stop-motion overlays as related practices with different objectives or scopes.

The local research record supports the following conclusions:

- Perspective projection, physical/image correspondence, P3P/PnP inputs, calibration inputs, image registration, rephotography, fiducial registration, surveyed VFX lineup, and overlay-guided stop-motion alignment are established subject matter or production practices.
- TPS-specific reference contents, the TPS Reference Distance, the Working Focal Length convention, the proposed reference-centered workflow, and its practical performance are not established by those sources. They are respectively proposed requirements, TPS-specific conventions, or unvalidated operational claims.
- The proposed contribution statement is supportable as a characterization of TPS’s intended organization, provided it remains explicitly framed as a proposed contribution and not as demonstrated novelty.
- The closest substantial overlaps are P3P/PnP for three-point physical/image correspondence, 3DEqualizer and surveyed VFX practice for physical survey data plus camera lineup, and Dragonframe/Gasek/AFTRS for registered visual comparison after camera movement. These overlaps weaken any broad claim that TPS invents correspondence, overlays, camera lineup, or view matching as individual techniques.
- The existing citations [1]–[12] correspond to entries in the paper’s reference list and to records in the research bibliography. Most associated claims are within the recorded evidence scope. The principal citation weaknesses are omitted direct citation for camera calibration, reliance on documentation or abstracts for some technically broad claims, and several negative/originality conclusions that should be labeled as limited findings rather than source-proven facts.

The section can proceed with a modest revision rather than a rewrite. It should add or cross-reference camera calibration explicitly, distinguish source-supported findings from the authors’ comparative interpretation, and state that the prior-art search did not establish a complete duplicate without implying that no such method exists.

## B. Prior-art comparison

| Method or practice | Problem it solves | Information typically required | Shared principles with TPS | Objective that differs from TPS | Local evidence status |
|---|---|---|---|---|---|
| Photogrammetry and space resection | Estimates the position and orientation of a photograph or camera from known control points. | Known object/control-point coordinates, image coordinates, camera model or orientation assumptions, and observations. | Perspective projection, collinearity, physical points, image points, and explicit correspondence. | Solves exterior orientation; TPS records a reference and does not require a unique pose solution. | Chow [1] and Open AGH [2] are recorded as examined/relevant in the bibliography and evidence map. |
| Perspective-n-Point (P3P/PnP) | Estimates camera rotation and translation from 3D–2D correspondences. | 3D object points, 2D image projections, intrinsics, and often distortion; P3P can use exactly three correspondences and return multiple solutions. | A/B/C ↔ a/b/c correspondence, reprojection comparison, and recognition that three points do not necessarily determine one pose. | Computes camera pose; TPS uses correspondence as a practical reference and expressly does not require camera reconstruction. | OpenCV [3] is directly cited and marked verified in the local evidence map. |
| Camera calibration | Estimates intrinsic parameters and, depending on the procedure, extrinsic parameters and distortion from calibration patterns or multiple views. | Calibration target geometry, detected image points, image dimensions, multiple views or poses, and a camera model. | Physical/image point measurement, image coordinates, camera parameters, and reprojection error. | Establishes a camera model; TPS preserves a recorded view and may record Working Focal Length without becoming a calibration procedure. | The bibliography contains an examined OpenCV calibration record, but the Related Work section does not cite it directly. |
| Matchmoving and VFX camera tracking | Tracks image features through footage and estimates camera motion, lens behavior, and/or a virtual camera and scene relationship. | Image sequences, tracked features, survey data, lens and camera information, and optimization or reconstruction tools. | Physical measurements, image correspondences, camera/lens parameters, and iterative alignment. | Usually seeks a solved virtual camera, tracked scene, lens model, or renderable production asset; TPS seeks a portable practical view reference. | Radke [bibliography], 3DEqualizer [8], and FXguide [9] are documented locally. Paper 1 directly cites [8] and [9]. |
| Image registration and homography | Places images or measurements into a common coordinate frame or estimates a transformation between images or planes. | Image features or control points, coordinate frames, transformation model, and sometimes a planar-scene assumption. | Registered frames, image correspondences, overlays, and comparison in image space. | TPS treats registration as a declared/interpretable comparison frame; it does not use an arbitrary fitted transformation to force nonmatching camera projections into agreement. | OpenCV homography [5], Brown, and the TPS registration derivation support the general distinction. The warning against forced agreement is a TPS interpretation requiring protocol validation. |
| Repeat photography and rephotography | Recreates or compares a historical or earlier viewpoint to document change or produce a comparable view. | Earlier image, landmarks or physical records, camera-location clues, maps, field judgment, and/or post-capture registration. | View reproduction, prior-view comparison, registration, and practical rather than necessarily model-complete recovery. | Does not, in the reviewed source, define TPS’s explicit three-point physical/image record, triangle measurements, or TPS calculations. | The *Heritage* review [4] is recorded as examined and verified for general rephotography and registration claims. |
| Fiducial markers and reference targets | Establish stable, detectable correspondences or transformations across images, modalities, or instruments. | Visible markers or targets, known identities/locations, imaging frames, and transformation or registration procedures. | Stable correspondence, physical or image reference points, registered comparison, and overlay use. | Microscopy fiducials and calibration targets generally serve multimodal registration or calibration, not recovery of a physical camera view through TPS’s reference record. | Mohammadian et al. [7] is marked examined and verified for its stated registration scope. |
| Practical camera lineup procedures | Aligns a camera or virtual camera to surveyed lines, points, geometry, or a reference image. | Survey points/geometry, image evidence, camera/lens controls, distance constraints, and operator or software feedback. | A/B initial alignment, C as additional information, coupled controls, and iterative visual comparison. | Existing VFX lineup generally solves or supports a virtual camera and production scene; TPS proposes a smaller, implementation-independent physical-camera reference workflow. | 3DEqualizer [8], FXguide [9], and the internal lineup-method documents establish substantial conceptual overlap; the A–B → C order remains a proposed heuristic. |
| Stop-motion overlays and onion skin | Compares a live/current frame with a previous frame to align drawings, placement, or a bumped camera. | Previous frame or reference image, live view, overlay/difference display, and operator judgment. | Registered visual comparison and iterative adjustment without requiring a camera solve. | Usually frame-to-frame placement or camera-bump recovery, not a documented three-point physical reference containing TPS measurements. | AFTRS [10], Gasek [11], and Dragonframe [12] are locally documented; Paper 1 cites all three. |

### Similar reference-based camera recovery prior art

The strongest prior-art concern is not one source that reproduces every TPS field, but the convergence of existing practices:

1. P3P/PnP already formalize three-dimensional point to image-point correspondence and expose pose ambiguity.
2. Survey-based VFX lineup already combines physical survey information, image observations, and iterative camera/lens adjustment.
3. Rephotography already treats returning to a prior view as a practical objective.
4. Stop-motion systems already use registered overlays to guide a user after a camera bump or between recorded and live images.
5. Fiducial and astronomical registration already use stable point identities and transformations for image comparison.

The local search did not identify an examined source that documents the complete TPS combination of an implementation-independent three-point physical/image reference, the TPS Reference Distance convention, the Working Focal Length/AOV record, and live-view recovery without a camera-solving objective. This is a limited search result, not evidence that no substantially similar method exists. The prior-art review itself identifies historical optical viewfinders, calibration targets, cinematography manuals, patents, and production-engineering literature as remaining search areas.

## C. Citation audit

### Citation-to-bibliography consistency

| Paper citation | Associated claim in Related Work | Bibliography/reference consistency | Relevance and support | Audit result |
|---|---|---|---|---|
| [1] Chow, “Photogrammetric Space Resection” | Three ground control points and image coordinates support photograph/camera position and orientation determination. | Complete enough in Paper 1; matches the Chow entry in `research/BIBLIOGRAPHY.md`. | Directly relevant to resection and the contrast with TPS. The local review examined the abstract/record rather than asserting complete full-text verification. | Retain; qualify full-text scope if needed. |
| [2] Open AGH, *Basics of Photogrammetry* | Collinearity of perspective center, object point, and image point; exterior orientation. | Matches the Open AGH entry in the bibliography. | Directly relevant to general photogrammetric principles. | Retain. |
| [3] OpenCV PnP 4.10 | P3P uses exactly three 3D–2D correspondences and may have up to four solutions; PnP estimates pose. | Matches the versioned OpenCV 4.10 entry. | Directly supports the stated P3P/PnP contrast and pose ambiguity. | Retain. |
| [4] *Heritage and Repeat Photography* | Rephotography locates an earlier camera position, produces a new image, and addresses registration. | Matches the bibliography title/DOI entry. | Supports the general rephotography objective; does not support a claim that TPS’s exact record is absent from all literature. | Retain with limited-search wording. |
| [5] OpenCV homography tutorial | Homography is a planar projective transformation; registration differs from TPS comparison. | Matches the bibliography entry and URL. | Supports the general homography/planar-transformation claim. It does not by itself establish the degree-of-freedom statement or the normative TPS prohibition on forced registration. | Retain; narrow or add a direct projective-geometry source for the degrees-of-freedom sentence. |
| [6] Astroalign | Three-point star asterisms can be matched to estimate an image transformation without WCS information. | Matches the bibliography entry, DOI, and author names. | Directly relevant to three-point image registration and clearly distinct from physical scene points. | Retain. |
| [7] Mohammadian et al. | Visible fiducials and composed transformations register multimodal microscopy images. | Matches the bibliography entry, DOI, and title. | Directly supports fiducial correspondence, registration, and overlay comparison within that microscopy scope. | Retain; avoid generalizing beyond the source. |
| [8] 3DEqualizer Technical Specification | Manual/automatic lineup to surveyed geometry, survey points, distance constraints, focal-length and lens controls. | Matches the bibliography entry and URL. | Strongly relevant prior art for survey-based camera lineup and parameter adjustment. It supports overlap, not the claim that TPS is categorically different in every operational respect. | Retain; acknowledge substantial overlap explicitly. |
| [9] FXguide interview | LIDAR, total-station data, reference frames, lens distortion, and production camera tracking. | Matches the bibliography entry and URL. | Relevant industry context, but an interview is weaker than a primary technical specification for precise workflow claims. | Retain for context; avoid relying on it for technical definitions. |
| [10] AFTRS *Stop Motion* | Onion-skin transparency helps align successive drawings/frames. | Matches the bibliography entry and URL. | Supports overlay-guided visual alignment; it does not support the TPS physical-point record. | Retain. |
| [11] Gasek, Chapter 6 | Frame-grabber onion skinning, ghosted frames, and recovery after a camera bump. | Matches the bibliography entry and publisher PDF link. | Strong practical precedent for overlay-guided recovery after camera movement. Access is restricted, so page-level claims should remain limited to the examined chapter excerpt. | Retain with access qualification. |
| [12] Dragonframe 2025 | Onionskin, Live View comparison, line-up layers, and difference display. | Matches the bibliography entry and URL. | Supports existing software practice for live/reference comparison. The local record notes limited direct PDF retrieval. | Retain with “indexed/manual material indicates” wording if precision is required. |

### Citation gaps and unsupported or overbroad assertions

- **Camera calibration is uncited in Related Work.** The paper names camera calibration in the Introduction and later contrasts TPS with it, but the bibliography already contains an examined OpenCV Camera Calibration record that is not assigned a paper reference number. Add that source to the paper’s references and cite it in a short calibration paragraph, or remove the stronger calibration comparison.
- **The homography degrees-of-freedom sentence is broader than [5] alone.** “A full projective transformation has more degrees of freedom than three point pairs can determine” is plausible and consistent with the local derivation, but the cited OpenCV tutorial is primarily an implementation/tutorial source. Cite a projective-geometry source already present in the bibliography or state it as a mathematical observation derived in the paper.
- **Negative literature claims need scope limits.** Statements such as “the reviewed literature does not establish” are acceptable when they mean “the sources examined in this review do not establish.” They should not read as proof that no prior method exists.
- **“Output is an estimated image transformation” and similar descriptions should remain source-bounded.** They are accurate for Astroalign and fiducial registration as characterized locally, but should not be generalized to all image-registration methods.
- **The phrase “operator-guided physical camera recovery” is comparative interpretation.** The cited sources establish overlays, image registration, or camera lineup separately; they do not collectively prove TPS’s proposed organization. Mark this as the authors’ synthesis.
- **Stop-motion sources support operational analogy, not TPS equivalence.** The current section mostly observes this distinction correctly; it should preserve the explicit limitation that the reviewed sources do not define TPS’s full record.
- **No paper citation currently covers the local lineup-method analysis.** `TPS_CAMERA_LINEUP_GEOMETRY.md` and `TPS_LINEUP_MATHEMATICAL_VERIFICATION.md` support the internal classification of A–B → C as a plausible, conditional heuristic, not a published prior-art source. They should not be presented as external validation.

## D. Established, proposed, and unvalidated claims

### Established

- Under an ideal perspective model, physical points map to image locations and image position depends on depth and camera parameters.
- Photogrammetric resection and P3P/PnP use physical/object points and corresponding image points for camera or pose estimation.
- Camera calibration uses measured object/image points and camera-model assumptions to estimate intrinsic and/or extrinsic parameters.
- Image registration and homography provide established ways to relate images or planes in a common coordinate system.
- Rephotography addresses return to or comparison with an earlier viewpoint.
- Fiducials, survey points, and reference targets support stable correspondence and registration in their respective applications.
- VFX camera lineup uses survey/image information and camera/lens adjustment; stop-motion tools use overlays or onion skin for practical visual alignment.
- Matching three points does not, by itself, establish the broader claim that an entire scene or image has been reproduced. This limitation is supported by the TPS geometry and the P3P ambiguity context, but the exact performance of any TPS procedure remains unvalidated.

### Proposed

- TPS’s implementation-independent reference record and its minimum information fields.
- The deliberate separation of a correspondence/reference system from camera recovery as an application.
- The use of the A–B relationship as a useful initial alignment reference and C as additional geometric information.
- The A–B → C order as a practical operator heuristic without a fixed mandatory adjustment sequence.
- The TPS Reference Distance convention and the Working Focal Length/AOV record as TPS-specific conventions.
- The proposed organization of correspondence, physical measurement, registered comparison, and iterative view alignment into one portable reference method.

These are proposals or design choices even where they use established components. Their inclusion in TPS is not made established merely by citing the component techniques.

### Unvalidated

- Accuracy, repeatability, and reproducibility of the complete TPS recovery workflow.
- Whether the A–B-first, C-refinement procedure improves convergence time, operator consistency, or final residuals relative to alternatives.
- Whether the TPS Reference Distance and Working Focal Length convention is sufficiently stable across real cameras, lenses, crops, sensor formats, focus states, and depth configurations.
- Whether three-point agreement provides useful predictive information about off-triangle image points under specified scene conditions.
- Interoperability in practice across independent tools, file formats, live-view systems, and replacement cameras.
- Any claim that TPS is original, non-obvious, or materially superior to existing lineup, registration, calibration, or matchmoving workflows.

## E. Potential originality concerns

The available research does not support an unqualified novelty claim. The individual elements of TPS are well represented in prior art:

- P3P/PnP: three-dimensional to two-dimensional correspondence and multiple pose solutions.
- Calibration: measured object/image points and camera-parameter estimation.
- VFX lineup: survey geometry, image evidence, camera/lens controls, and iterative alignment.
- Rephotography: practical return to an earlier camera viewpoint.
- Fiducial/astronomical registration: stable point identities, transformations, and reference frames.
- Stop-motion overlays: live/reference visual comparison after camera movement.

The potentially distinctive aspect is the constrained organization: a small, implementation-independent reference intended for practical camera-view reproduction, carrying physical triangle relationships and TPS-specific measurement conventions while declining to solve for a unique camera. That characterization is reasonable as a proposed contribution, but it is not a demonstrated originality result. A stronger originality assessment would require a broader search of patents, cinematography and optical-viewfinder manuals, camera-lineup procedures, calibration-target workflows, stop-motion production literature, and proprietary or historical production documentation.

The 3DEqualizer comparison is especially important. Its documented survey points, lineup controls, distance constraints, focal-length controls, and camera-consistency operations substantially overlap TPS’s physical/image correspondence and alignment concepts. The difference in implementation independence and objective may be meaningful, but it does not by itself establish novelty. Likewise, Dragonframe and related stop-motion practices weaken any broad claim that live/reference overlay-guided recovery is new.

## F. Recommended Related Work revisions

1. Add a short “Camera calibration” paragraph using the existing OpenCV calibration bibliography entry. State its inputs and parameter-estimation objective, then contrast it with TPS’s reference-preservation objective.
2. In the opening of Related Work, state that TPS combines established elements but proposes a different scope and organization; avoid implying that any individual component is new.
3. Replace broad negative formulations with bounded language such as “The sources examined here do not establish…” and “This review did not identify…”.
4. Cite or qualify the homography degrees-of-freedom statement. If no additional reference is added, present it as a mathematical consequence of the model rather than as a claim supported solely by the OpenCV tutorial.
5. Expand the VFX lineup paragraph to acknowledge 3DEqualizer as substantial overlapping prior art, not only as a different-scale practice.
6. Add one sentence distinguishing the local TPS lineup-method documents from external prior art: they verify or analyze a proposed TPS heuristic; they do not establish historical precedence or independent validation.
7. Keep the existing caveats around Dragonframe, Gasek, and restricted/incomplete access. The bibliography’s verification statuses should govern the paper’s wording.
8. Preserve the statement that the proposed contribution is organizational and operational, but pair it with the explicit limitation that comparative performance and originality remain open questions.

## G. Unresolved research questions

- Does a prior publication, patent, cinematography manual, optical viewfinder procedure, or production document already specify three physical reference points, their image correspondences, and a live registered camera-recovery workflow?
- Is the TPS Reference Distance convention materially different from existing camera-survey, focus-distance, calibration-target, or lineup measurements, and does that difference improve reproducibility?
- What camera, lens, sensor, crop, distortion, focus, and depth conditions determine whether a three-point match predicts useful off-triangle agreement?
- Under what configurations does C add measurable information beyond A–B, and when is it poorly conditioned or redundant?
- Does the proposed iterative workflow outperform unguided overlay alignment, conventional camera lineup, or a solved PnP/matchmoving workflow for a defined practical task?
- What is the appropriate baseline and acceptance metric: point residuals, off-triangle landmark residuals, whole-image registration, time to convergence, operator variability, or production usability?
- Can independent implementations exchange a TPS reference without ambiguity in units, image dimensions, crop, coordinate origin, sensor area, and measurement conventions?
- Which claims about Working Focal Length and AOV should remain descriptive TPS quantities rather than be interpreted as calibrated optical parameters?
- What broader search is needed before making any claim about originality, non-obviousness, or priority?

## Bottom line

The Related Work section is suitable as a cautious foundation, but it should not present TPS as novel on the basis of terminology or implementation independence. The proposed contribution statement is supported as a description of TPS’s intended organization:

> TPS organizes physical-to-image correspondence, geometric measurement, and iterative visual comparison into a portable reference method for practical camera-view reproduction without requiring a complete camera-pose solution.

The statement is strongest when “organizes” and “proposed contribution” remain explicit, and when “practical camera-view reproduction” is treated as an objective requiring validation rather than as an established performance result. The existing research supports the ingredients and the distinction of objectives; it does not yet establish that the complete organization is original, superior, or experimentally effective.
