# TPS Prior-Art Review

**Scope:** External literature review supporting Paper 1 of the Three Point System.

**Status:** Research document. It does not modify or add to the TPS specification.

## 1. Research Scope

This review examines established methods involving physical points, image correspondences, camera alignment, view reproduction, image registration, overlays, visual effects, and stop-motion. It does not claim that TPS is novel. The comparison is limited to publicly identifiable methods and sources whose relevant content was examined.

The central question is whether TPS contributes a distinct practical organization of known techniques: recording three identified physical points and their image locations, then using a registered reference to guide a later closest-practical view match without requiring camera solving.

## 2. Search Method

Sources were sought in projective geometry, computer vision, photogrammetry, visual effects, image registration, and stop-motion production. Priority was given to official university, standards, publisher, and software-documentation sources, with open access where available.

Each source is classified as:

- **Identified:** A bibliographic record was located.
- **Examined:** Relevant source content was accessible and reviewed.
- **Directly relevant:** The examined content addresses a TPS concept or a closely related method.
- **Inaccessible:** A record was located, but the relevant full content was not confirmed.

## 3. Established Mathematical Foundations

### Perspective projection and physical/image correspondence

MIT's *Foundations of Computer Vision*, §5.3.1, describes perspective image formation from 3D points to 2D image coordinates. OpenCV's official Perspective-n-Point documentation describes object points, corresponding image projections, camera intrinsics, and reprojection error.

These sources directly support the general relationship between physical points and image points. They do not establish the TPS reference, its three-point operating choice, or the Working Focal Length convention.

### Pose estimation and calibration

OpenCV's `solvePnP` documentation states that pose estimation uses 3D object points and corresponding 2D image projections, together with camera intrinsics and distortion coefficients, to estimate rotation and translation by minimizing reprojection error. OpenCV's calibration tutorial describes obtaining object points and image points from calibration patterns and estimating intrinsic and extrinsic parameters across multiple views.

This is the closest established computational analogue to TPS's point correspondence. It differs fundamentally in objective: PnP and calibration solve for camera or object parameters, while TPS records and compares a three-point view and does not require unique pose recovery.

## 4. Existing Camera-Matching Techniques

Radke's *Computer Vision for Visual Effects*, Chapter 4, explains matching and tracking image features across different perspectives and times; its Chapter 6 is dedicated to matchmoving. The publisher's chapter description identifies feature matching as a basis for relating images and tracking camera motion.

This is directly relevant to the broader camera-view-reproduction problem. Matchmoving generally uses many image features, temporal sequences, and 3D reconstruction or camera-path estimation. TPS is narrower: three identified correspondences, a recorded reference, and manual or practical view matching without requiring a solved camera path.

Perspective-n-point methods are also substantially overlapping prior art when the physical 3D coordinates and camera intrinsics are known. They should not be described as TPS implementations, because their goal is parameter estimation rather than implementation-independent reference matching.

## 5. Image Registration and Overlays

Brown's 1992 survey is a foundational bibliographic source for image registration across different times, viewpoints, and sensors, but the full relevant article was not accessible during this review. It is therefore identified, not examined or verified here.

The TPS research derivation on image registration is consistent with the established distinction between declaring a coordinate transformation and fitting a transformation merely to force three points into agreement. The latter would erase the measured difference TPS intends to compare. This is a TPS interpretation requiring further protocol and experiment, not a claim that TPS invented image registration.

## 6. Stop-Motion and VFX Applications

The Australian Film Television and Radio School stop-motion material, pp. 14–15 of the reviewed PDF, describes an onion-skin effect in which translucent frames are projected over one another so that a user can align successive drawings. This directly supports the use of transparent overlays for practical visual alignment, but it concerns frame-to-frame animation rather than recovery of a camera view from three physical point correspondences.

Gasek's *Frame-by-Frame Stop Motion*, Chapter 6, pp. 104–105 in the examined chapter PDF, describes camera stability, frame-grabber onion skinning, coaxing a bumped camera back into place, and ghosted frames for placement registration. This is a close practical precedent for overlay-guided recovery after camera movement. It does not define TPS's three-point reference contents or its Working Focal Length.

The literature therefore supports overlays and camera stability as established production practices. It does not show that TPS's exact three-point reference procedure is an established named method.

## 7. Historical Precedents

Traditional animation's translucent-paper onion skin and modern stop-motion frame-grabber overlays are historical and contemporary precedents for comparing a current view with a recorded visual reference. The reviewed sources establish the practice at a general level.

The present review did not verify a historical camera-view method using exactly three physical points, explicit A→a/B→b/C→c correspondence, and a sensor-plane reference distance. That absence is not evidence of originality; it identifies a search gap.

## 8. Comparison with TPS

| Existing method | Overlap with TPS | Important difference |
|---|---|---|
| Perspective projection | Physical points map to image points. | General mathematical model, not a recovery workflow. |
| Camera calibration | Uses known physical points and image measurements. | Estimates intrinsics/extrinsics, usually from patterns and multiple views. |
| PnP / pose estimation | Uses corresponding 3D and 2D points. | Solves pose and requires camera-model inputs; TPS does not solve cameras. |
| Image registration | Places image measurements in a common frame. | General registration may estimate transformations; TPS forbids using registration to force a match. |
| Matchmoving | Reproduces or explains camera motion from image evidence. | Typically uses many features, sequences, and camera reconstruction. |
| Onion-skin overlays | Compares a live/current frame with a recorded frame. | Usually frame-to-frame or placement alignment, not a three-point physical/image reference. |

The strongest overlap is conceptual and operational: known correspondences, a registered visual reference, and iterative adjustment to recover a desired view. The strongest difference is scope: TPS intentionally packages a minimal three-point method while excluding camera reconstruction as its objective.

## 9. Potential TPS Contribution

The following may constitute a practical contribution, but are hypotheses rather than established novelty claims:

1. A simple, explicit three-point correspondence record intended for physical, photographic, overlay, or software use.
2. An implementation-independent recovery workflow centered on comparing three registered image locations.
3. A deliberate separation between view matching and camera reconstruction.
4. Preservation of physical triangle measurements and a TPS-specific Working Focal Length record alongside the image correspondence.

The first three items combine established concepts in a constrained workflow. The fourth is TPS-specific in its formulation but remains mathematically approximate and experimentally unvalidated. A formal novelty claim requires a broader patent and academic search, especially in cinematography, optical viewfinders, matchmoving, photogrammetry, and production engineering.

## 10. Research Gaps

- Search for prior methods using exactly three physical reference points and a live registered overlay for camera-view recovery.
- Search historical optical viewfinders, alignment frames, and cinematography manuals for physical registration techniques.
- Compare TPS with planar fiducials, calibration targets, and minimal pose-estimation methods without treating them as equivalent.
- Experimentally measure recovery repeatability under camera movement, replacement cameras, crop changes, and lens changes.
- Test the Working Focal Length convention against real lenses and the sensor-plane distance approximation.
- Establish how three-point matching behaves when the replacement physical triangle is relocated, scaled, or replaced.
- Do not treat lack of evidence in this review as evidence of TPS originality.

## 11. References

The complete bibliographic records and access statuses are maintained in [BIBLIOGRAPHY.md](BIBLIOGRAPHY.md). The most directly relevant examined sources are:

1. OpenCV, “Perspective-n-Point (PnP) pose computation,” 4.8.0 documentation.
2. OpenCV, “Camera Calibration,” 4.11.0 documentation.
3. Richard J. Radke, *Computer Vision for Visual Effects*, Chapters 4 and 6, Cambridge University Press, 2012; publisher chapter record examined.
4. Australian Film Television & Radio School, *Stop Motion*, pp. 14–15, open educational PDF.
5. Tom Gasek, “Objects, People, and Places,” in *Frame-by-Frame Stop Motion*, Chapter 6, pp. 104–105; chapter PDF examined, publisher access restricted.
6. Richard Hartley and Andrew Zisserman, *Multiple View Geometry in Computer Vision*.
7. MIT, *Foundations of Computer Vision*, §5.3.1.

## Independent Research Addendum

This addendum records the targeted external pass requested after the initial review. It is evidence about prior art and established practice, not a change to TPS requirements.

### OpenCV — Perspective-n-Point Pose Computation

The examined OpenCV 4.10 documentation states that pose computation uses 3D–2D point correspondences, camera intrinsics, and distortion parameters to estimate rotation and translation by minimizing reprojection error. Its P3P section states that `solveP3P()` uses exactly three 3D–2D correspondences and can return up to four solutions. The documentation also distinguishes P3P/AP3P input behavior in `solvePnP()` and notes that generic PnP can expose multiple solutions.

This directly establishes that three corresponding physical/image points are part of an existing camera-pose problem and that three correspondences do not necessarily identify a unique camera pose. It does not establish TPS: P3P assumes a pose-estimation objective and camera-model inputs, while TPS records and compares image locations and expressly does not require camera reconstruction.

### Dragonframe — *Using Dragonframe 2025*

The accessible indexed text from the examined Dragonframe 2025 manual describes onionskin transparency, dissolving a previous frame over Live View, difference mode, and frame-echo controls. Direct retrieval of the large PDF was limited by the source endpoint, so this source is treated as examined for the indexed manual sections but not as a complete manual review.

The material establishes an existing stop-motion practice of comparing a live view with a recorded frame using transparency or difference display. It does not establish physical point identities, measured triangle geometry, TPS Reference Distance, Working Focal Length, AOV, or a camera-independent TPS reference record.

### Dragonframe — Camera Support

The examined camera-support page states that Dragonframe creates a low-resolution live video-assist sequence and a high-quality capture sequence, keeps them in tandem, and may use live view for animation while capturing full-resolution stills. It also lists camera-specific live-view dimensions, including examples where live view is 960 × 640 or 1920 × 1280.

This is directly relevant to TPS coordinate-frame registration: a live comparison image and a final capture may not share dimensions or representation. It supports the need to distinguish the actual captured image frame from a video-assist frame. It does not define TPS registration or the TPS minimum reference contents.

### Szeliski — *Computer Vision: Algorithms and Applications*, Second Edition

The author's examined book page identifies the 2022 second edition, its computer-vision course basis, and the official electronic edition. The specific downloadable chapter text was not available in the reviewed page, so no chapter-specific mathematical claim is marked verified from this source.

The source is relevant as an authoritative textbook reference for camera geometry, image formation, registration, and matching, but this pass does not claim to have examined those specific chapters. It does not establish TPS or a three-point recovery workflow.

### Science-D-Visions — 3DEqualizer Technical Specification

The examined technical specification lists Lineup Controls for manual camera alignment to surveyed line geometry, dragging lineup-only points, extracting survey data from vertices, lines, and faces, and matching a camera in the current frame to tracked survey points. It also lists automatic camera-consistency operations involving rotation, translation, focal length, and camera position, as well as survey point types, distance constraints, camera constraints, adjustable lens parameters, and focal-length calculation from perspective grid shots.

These are clear precedents for:

- physical survey data associated with image-tracked points;
- physical-to-image correspondence;
- manual camera alignment;
- automatic camera alignment and consistency operations;
- use of distance constraints and lens/camera parameters.

The operational objective differs from TPS. 3DEqualizer is a software system for matchmoving, survey alignment, camera solving, lens modeling, and production tracking. TPS is an implementation-independent method for recording and recovering a three-point image view without requiring a solved virtual camera, a 3D scene reconstruction, or a particular software system.

The reviewed specification does not document a workflow that is substantially identical to the complete TPS operational model, including the TPS Reference Distance convention, the approved Working Focal Length and AOV record, and physical overlay or live-view recovery independent of camera-solving software. It does, however, substantially overlap the underlying correspondence and camera-lineup concepts. This reduces the basis for broad originality claims.

### FXguide — 3DEqualizer interview

The examined interview describes the value of precise survey data, including LIDAR, total-station data, and reference frames; use of survey to reduce tracking effort and address low-parallax shots; and the need to optimize lens distortion, focal length, scale, and other camera parameters. It also describes camera-tracking workflows and the distinction between monoscopic scale ambiguity and more constrained stereoscopic work.

This supports the conclusion that surveyed physical geometry and image tracking are established VFX practice. It does not establish TPS's manual, implementation-independent, three-point reference-and-recovery objective.

### Addendum conclusion

The closest technical precedents are P3P/PnP for three-point physical/image correspondence and pose ambiguity, 3DEqualizer for survey-based camera lineup and parameter adjustment, and Dragonframe for overlay-guided live/reference comparison. TPS's possible contribution is the combination and restriction of these ideas into a small, implementation-independent view-recovery method with preserved physical measurements and TPS-specific recorded calculations. That combination remains a research hypothesis, not a demonstrated novel contribution.

