# TPS NotebookLM Addendum — Paper 1, Projective Continuity, and Lineup Geometry

This addendum contains newly developed research material after the original NotebookLM package. The repository remains authoritative. Source contents below are reproduced verbatim. The revised paper is authoritative; the alternate draft is included only for comparison. The lineup documents are non-normative research material.

## Index

| Original file path | Document title | Category | Status |
|---|---|---|---|
| research/papers/PAPER_01_REVISED.md | The Three Point System: A Reference-Based Method for Camera-View Reproduction | Academic paper | Authoritative revised draft |
| research/notes/PROJECTIVE_CONTINUITY_RESEARCH_NOTE.md | Projective Continuity Across Physical, Digital, and Cinematic Space | Research note | Proposed conceptual frame |
| research/methods/TPS_CAMERA_LINEUP_GEOMETRY.md | TPS Camera Lineup: Operational Method and Geometric Foundations | Research method | Non-normative working draft |
| research/methods/TPS_LINEUP_MATHEMATICAL_VERIFICATION.md | TPS Lineup — Mathematical Verification Report | Research verification | Non-normative verification report |
| research/methods/TPS_PHYSICAL_LINEUP_PROCEDURE_REVIEW.md | TPS Physical Camera Lineup — Procedure Review | Research procedure review | Non-normative operational review |
| entropy-buffer/PAPER_01_DRAFT_VIEW_CONTINUITY.md | The Three Point System: A Reference-Based Method for Camera-View Reproduction | Comparison draft | Uncommitted alternate draft |

## Manifest

Included documents: 6. The revised paper is the canonical paper for this addendum. The projective-continuity note is a supporting conceptual document. The lineup documents are non-normative research material. The entropy-buffer paper is preserved only as an uncommitted comparison reference.


==================================================
SOURCE: research/papers/PAPER_01_REVISED.md
==================================================
# The Three Point System: A Reference-Based Method for Camera-View Reproduction

**Christopher Weinberg**
**LIMNMEDIA**

## 1. Abstract

The Three Point System (TPS) is an implementation-independent method for recording and reproducing a camera view. Its central principle is: “TPS connects three points in the physical world with where those same three points appear in an image.” A TPS reference identifies three physical points, records their corresponding image locations, preserves the physical relationships among the points, and retains information needed to interpret and register the image coordinates. It may also preserve a measured TPS Reference Distance, a Working Focal Length, and a derived horizontal angle of view.

TPS is deliberately narrower than camera calibration, photogrammetric resection, or visual-effects matchmoving. It does not attempt to solve for a unique camera position, orientation, or complete camera model. Instead, it gives an operator a portable visual reference and a small set of physical measurements with which to seek the closest practical reproduction of a previously recorded three-point view. The method can be implemented with a physical overlay, a monitor, photographic or film media, or software.

The geometric foundations of TPS are established principles of perspective projection and correspondence. Related practices exist in multiple disciplines, including photogrammetry, rephotography, image registration, visual effects, fiducial registration, astronomy, and stop-motion production. This paper defines the reference, describes the recording and recovery operations, and derives the associated camera quantities under stated assumptions. Practical performance remains to be evaluated.

## 2. Introduction

Reproducing a camera view is a common practical problem. A camera may be moved, removed, replaced, or unavailable when a scene must be photographed again. The problem appears in independent filmmaking, visual effects, stop-motion, architectural documentation, rephotography, education, and other settings. Existing solutions range from careful physical measurements and motion-control systems to camera calibration, feature tracking, and full matchmoving pipelines. These approaches can be effective, but they may require specialized equipment, software, or technical expertise.

TPS addresses a more limited question: how can an operator record enough information about a view to seek that view again later using three identifiable physical reference points and their image locations? The intended answer is not a camera-solving algorithm. It is a reference-based method for view matching.

The TPS kernel states the relationship directly: “TPS connects three points in the physical world with where those same three points appear in an image.” The physical points are conventionally labeled A, B, and C. Their corresponding image points are a, b, and c. The identities are preserved as A→a, B→b, and C→c, even when the image coordinates change.

This distinction between identity and location is fundamental. A point can move in an image when the camera moves, rotates, changes focal length, or changes other imaging conditions. The image point remains associated with the same physical point. Conversely, three image locations alone do not reveal a unique three-dimensional camera configuration. Multiple physical and camera configurations can produce the same three-point projection under appropriate conditions.

TPS therefore has two layers. The first is geometric: physical points are projected into image space, and correspondence can be compared. The second is operational: a reference is recorded and later presented in registration with a live view so that a user can adjust the camera. The first layer rests on established mathematics. The practical effectiveness of the second layer requires experiments.

## 3. Related Work

### Photogrammetric resection and PnP

Photogrammetry provides a close mathematical precedent. In space resection, known control points and their image coordinates are used to determine the exterior orientation of a photograph or camera. Chow’s 1950 paper discusses three ground control points and their photograph coordinates as a basis for determining the position and orientation of a photograph [1]. Open educational photogrammetry material similarly describes the collinearity of the perspective center, object point, and image point, together with exterior-orientation parameters [2].

Perspective-n-point methods provide a modern computer-vision counterpart. OpenCV documents P3P as a pose problem using exactly three 3D–2D correspondences, with up to four possible solutions [3]. The same documentation describes PnP as estimating rotation and translation from object points, image projections, camera intrinsics, and distortion parameters. These methods establish that physical/image point correspondence is a standard input to camera pose estimation, and that three correspondences do not necessarily imply a unique pose.

TPS overlaps this geometry but has a different objective. Resection and PnP seek camera or object parameters. TPS does not require the operator to solve for a camera pose. It uses correspondence to compare a recorded view with a live view and to guide adjustment toward a practical match. Thus, TPS should not be described as a simplified PnP solver.

### Repeat photography

Repeat photography, or rephotography, seeks to make a new photograph from an earlier viewpoint, often to document landscape or cultural change. A review in *Heritage* describes locating the original camera position, producing a new image, and addressing the registration of old and new images [4]. This shares TPS’s operational goal more closely than camera resection does: the desired outcome is a comparable view rather than a complete camera model.

The difference is that rephotography commonly uses landmarks, historical records, maps, field judgment, or post-capture image registration. The reviewed literature does not establish the TPS record of three identified physical points, explicit A→a/B→b/C→c correspondence, physical triangle measurements, or TPS calculations. TPS can be understood as a constrained and formalized reference strategy within the larger problem of repeat photography.

### Image registration and homography

Image registration establishes a common coordinate relationship between images. OpenCV’s homography tutorial describes a planar projective transformation between planes [5]. In a full projective transformation, the transformation model has more degrees of freedom than three point pairs can determine. TPS therefore distinguishes registration from geometric correction. A known crop, rotation, scale, or coordinate transformation may be applied to make two records interpretable in the same frame. An arbitrary transformation chosen because it makes three nonmatching projections coincide would remove the difference TPS is meant to measure.

Astroalign is a particularly relevant interdisciplinary precedent. Beroiz, Cabral, and Sanchez describe matching three-point star asterisms to find transformations between astronomical images without relying on world-coordinate-system information [6]. This demonstrates an established three-point image-registration technique. It differs from TPS because its triangles are image features rather than identified physical scene points, and its output is an estimated image transformation rather than an operator-guided physical camera recovery.

Fiducial-marker registration in microscopy provides another related precedent. Mohammadian and colleagues describe visible markers and composed transformations for registering fluorescence and electron-microscopy images with different resolution and contrast [7]. The work supports the general value of stable correspondences, registered frames, and overlay comparison. It does not establish TPS’s camera-view objective or its physical triangle record.

### VFX camera surveying and lineup

Visual-effects matchmoving systems use tracked image features, survey data, camera and lens parameters, and optimization to reconstruct a virtual camera and scene relationship. 3DEqualizer documents manual and automatic camera lineup to surveyed geometry, survey points, distance constraints, focal-length controls, and lens parameters [8]. A related industry interview discusses the use of LIDAR, total-station data, reference frames, and lens-distortion models in production camera tracking [9].

These practices substantially overlap TPS’s use of physical measurements and image correspondences. They differ in scale and purpose. A VFX pipeline generally seeks a virtual camera, tracked scene, lens model, or renderable production solution. TPS seeks a portable reference for a human or application to reproduce a view and does not require the recovery of a unique virtual camera.

### Stop-motion overlays

Stop-motion workflows commonly compare a live camera view with a previous frame. The Australian Film Television & Radio School describes onion-skin transparency as a way to see a prior frame over the live image and align the next drawing [10]. Gasek describes frame-grabber onion skinning and ghosted frames for placement registration after a camera bump [11]. Dragonframe documentation similarly describes onionskin, Live View comparison, line-up layers, and difference display [12].

These are close operational precedents for registered visual comparison. They demonstrate that an overlay can guide an operator without requiring a camera solution. They do not, in the sources examined, define a reference consisting of three identified physical points together with physical triangle measurements, TPS Reference Distance, Working Focal Length, and AOV.

## 4. TPS Method

TPS begins by identifying three distinct, non-collinear physical points. A point is a specified location in three-dimensional Euclidean space; it need not be a separate physical object. A corner, mark, or identifiable feature may represent one. The points are labeled A, B, and C.

The camera observes the points and produces image points a, b, and c. Correspondence is explicit:

```text
A → a
B → b
C → c
```

The reference preserves both the identities and the image locations. The physical triangle and image triangle are related but are not assumed to be geometrically similar. Under perspective projection, physical side-length ratios and angles are not generally preserved in the image.

A TPS reference preserves at least the following information:

1. The three identified physical points A, B, and C.
2. Their image locations a, b, and c.
3. Explicit correspondence.
4. Measured physical triangle relationships, including AB and other relationships relevant to the operation.
5. The TPS Reference Distance, D.
6. The actual captured image width and height in pixels.
7. Active physical sensor dimensions when known and applicable to the captured imaging area.
8. Image coordinate-frame information sufficient to interpret and register the recorded points.
9. The Working Focal Length, its inputs, and the calculated horizontal AOV.

The image coordinate frame must state image dimensions, coordinate origin, axis directions, coordinate units, point positions, and relevant crop, rotation, or mirroring information when needed. No particular file format or software convention is required. The purpose is interpretability across implementations.

The TPS Reference Distance is measured from the camera sensor plane to the designated physical reference plane. It is not automatically equivalent to a lens focus-ring marking, a manufacturer-reported focus distance, or an ideal optical projection-center distance. The sensor-plane convention is practical and approximate.

## 5. Mathematical Foundations

Under an ideal perspective camera, a physical point with camera coordinates `(X,Y,Z)` projects to image-plane coordinates

```text
x = f X / Z
y = f Y / Z
```

where `f` is the model focal length. This mapping explains why image position depends on camera position, orientation, intrinsic parameters, and point depth. It also explains why the physical triangle need not resemble the image triangle.

If A, B, and C have different depths, each point is scaled by a different denominator. A single scale factor therefore does not generally relate all physical side lengths to all image side lengths. Similarity can occur in special cases, such as a triangle on a plane parallel to the image plane under an ideal model, or under an orthographic approximation. Similarity is not a universal TPS requirement.

Correspondence is a different concept from similarity. TPS preserves which image point belongs to which physical point. It does not claim that A, B, and C and a, b, and c have equal distances or angles. Three physical points can also produce a collinear or coincident image configuration under certain viewing geometries. Such a projection exists, although it may be unusable for a particular operation.

Registration also has a limited role. Two records may use different resolutions, crops, rotations, or coordinate conventions. A declared transformation can place them in a common frame. That transformation must be known or independently justified. It must not be selected solely to force a mismatch into agreement.

## 6. Working Focal Length and AOV

TPS records a Working Focal Length when establishing a reference. The approved calculations are:

```text
f_px = |xB - xA| * D / AB

AOV_h = 2 * atan(AB * W_image / (2 * D * |xB - xA|))

f_mm = f_px * W_sensor / W_image
```

Here, `xA` and `xB` are roll-corrected horizontal image coordinates; `AB` is the measured physical distance between A and B; `D` is the TPS Reference Distance; `W_image` is the actual captured image width in pixels; and `W_sensor` is the active physical sensor width in millimeters.

The ideal pinhole relationship is `image separation = focal length × physical separation / Z`, where `Z` is the segment’s depth measured along the camera optical axis from the projection center. TPS substitutes the measured sensor-plane-to-reference-plane distance `D` for `Z` as a practical approximation. This substitution is most defensible when A and B lie approximately in the designated reference plane, that plane is approximately perpendicular to the optical axis, and the difference between sensor plane and projection center is small relative to the working distance. The second equation follows from the ideal pinhole model: the half-width of the image corresponds to half the horizontal field angle. Substituting `f_px = |xB-xA|D/AB` gives the equivalent form `AOV_h = 2 atan(W_image/(2 f_px))`. The third converts pixel focal length to millimeters using the active sensor width and captured image width.

These calculations require assumptions. A and B should be at approximately equal depth, and the physical A–B segment should be aligned as closely as practical with camera-horizontal. Roll correction accounts for image rotation; it does not correct physical A–B misalignment. Lens distortion, unequal depth, reference-plane tilt, crop ambiguity, resampling, finite-focus effects, and the sensor-plane distance convention can introduce error.

`f_px` and `AOV_h` do not require physical sensor dimensions. `f_mm` does. If active sensor dimensions are unavailable, the reference remains usable with the pixel calculation and AOV retained while the millimeter calculation is omitted. The AOV is derived from TPS geometry; it does not independently determine a missing sensor width. The Working Focal Length is a TPS measurement convention and is not necessarily identical to a manufacturer’s nominal focal length or a laboratory effective focal length.

These equations are dimensionally consistent under the stated ideal geometry. Their application to real cameras is approximate. TPS uses established geometric principles and alignment techniques; its accuracy, repeatability, reproducibility, and performance under varying production conditions require systematic characterization.

## 7. Recording and Recovering a View

### Establishing the reference

Consider a stop-motion set that must be photographed again after the camera has been removed. Before the original setup is disturbed, the operator chooses three identifiable points on the set, A, B, and C, that can be identified again. The points need not be dedicated markers: suitable corners or set features may serve, provided their identities are unambiguous and they retain their intended geometric relationships for the recovery operation. The operator identifies their image locations a, b, and c in a captured reference image and records the physical triangle measurements. A and B should be selected with the Working Focal Length assumptions in mind; the general correspondence method does not require the whole triangle to be parallel to the image plane.

The reference also preserves the image's actual pixel dimensions, coordinate origin and axis conventions, and any information needed to interpret crop, rotation, or mirroring. The operator measures the TPS Reference Distance D from the sensor plane to the designated physical reference plane and records the measurement convention. Active physical sensor dimensions are included when known, and only when they correspond to the active imaging area represented by the capture. When establishing the TPS reference, the Working Focal Length and horizontal AOV are calculated and retained with their inputs. If active sensor dimensions are unavailable, `f_px` and `AOV_h` are retained and `f_mm` is omitted. These values describe the original reference; they are not a substitute for the three correspondences.

### Recovering the view

When the set is revisited, the operator identifies the same physical points. The recorded image points are displayed in a coordinate frame registered to the current live camera image. A transparent reference can be placed over a television monitor showing the live view; a registered celluloid or film reference can be aligned with an optical or projected view; or a digital overlay, such as a transparent PNG, can be composited over a live feed. The overlay is one representation of the reference, not the complete TPS record.

The operator adjusts the physical camera while observing the positions of A, B, and C relative to a, b, and c. Camera position, orientation, focal length, crop, and other imaging parameters that affect the projection or image coordinate frame may each affect the observed positions. The reference helps the operator recognize the remaining differences, but TPS does not prescribe an adjustment order or claim that a particular mismatch uniquely identifies its cause. The objective is the closest practical reproduction of the recorded three-point projection, judged in the context of the shot.

The physical measurements provide a durable description of the reference triangle and a way to check or re-establish the recorded triangle measurements if the set is disturbed. D and the derived camera quantities provide additional context for re-establishing the setup, particularly when the original lens settings are unavailable. None of these measurements alone determines the recovery camera's pose. If the set points themselves have moved, the original correspondence no longer describes the same physical geometry until that change has been resolved.

A replacement camera may have different sensor dimensions, image resolution, lens behavior, or controls. In that case the live image and recorded point positions must still be compared in an appropriately registered frame; matching raw pixel coordinates from unlike images is not meaningful without a justified mapping. TPS does not require identical camera equipment, but it does not guarantee that two different optical systems can reproduce the same projection over the entire scene.

## 8. Assumptions and Limitations

TPS assumes that point identities remain consistent within a correspondence set. The physical points must remain visible and maintain the intended geometric relationships for the operation. If a different triangle is used, its correspondence and geometric relationship to the reference must be established separately. Triangle similarity is one possible relationship, not a universal requirement.

Three-point matching is limited. A match of a, b, and c does not prove that the original camera position, orientation, focal length, or complete configuration has been recovered. It does not guarantee that other scene points project to the same locations or that the complete image matches. OpenCV’s P3P documentation provides a direct mathematical reminder: exactly three 3D–2D correspondences can yield up to four pose solutions [3].

The reference can also be geometrically degenerate. If projected points are coincident or collinear, the three-point record may not contain enough information for a particular operation. Point correspondence must not be inferred from proximity alone. A point that moves across the image remains associated with its original physical identity.

The Working Focal Length calculation has additional limitations. D is measured from the sensor plane rather than an ideal projection center. A and B may have unequal depth. The reference plane may be tilted. Lens distortion and focus breathing may affect the relation between image separation and focal length. The active sensor width may be unknown or may not correspond to the captured image area. These limitations mean that the recorded value is best treated as a reproducible TPS quantity under stated conditions, not as a universal optical truth.

Finally, practical matching involves measurement uncertainty and operator judgment. A visual match can be useful without being mathematically exact. Exact coordinate equality and practical agreement within a user- or operation-specific tolerance must remain distinct.

## 9. Discussion

TPS sits between two established traditions. One tradition solves geometry: photogrammetric resection, P3P/PnP, camera calibration, homography, and matchmoving estimate transformations, camera parameters, or scene structure. The other tradition guides practical alignment: repeat photography, stop-motion onion skin, reference overlays, and fiducial registration help an operator compare one view with another.

TPS uses information from both traditions but adopts neither objective completely. It borrows the precision of explicit point identity, physical measurement, and declared image coordinates. It borrows the accessibility of a registered visual comparison. It does not require a 3D reconstruction, a solved camera, a calibration pattern, a proprietary software package, or a particular recording medium.

This combination may be useful for independent animators, students, small productions, educators, and production environments where the desired result is a repeatable view rather than a complete camera asset. Its possible contribution is organizational and operational: define a small reference containing physical and image information, preserve it independently of technology, and use it to guide recovery.

### Research Origins and Production Context

TPS is an independently formalized method developed through LIMNMEDIA. The author reports approximately two decades of professional stop-motion and VFX experience, including work associated with *Coraline*, *ParaNorman*, *The Boxtrolls*, *Kubo and the Two Strings*, *Missing Link*, *The Tiny Chef Show* (Seasons 2 and 3), and *In the Know*. This experience informs the practical problem and the proposed workflow. It does not imply that TPS was an official studio project, a production deliverable, or an endorsed methodology of any studio or production.

The later formalization of TPS through LIMNMEDIA is distinct from those production experiences. The component techniques are established; this paper presents their proposed organization as a portable reference workflow. Comparative performance, repeatability, reproducibility, and the extent of any distinctive contribution remain open questions requiring systematic characterization. No intellectual-property ownership claim is made here on the basis of professional experience alone.

### View Continuity and Cinematic Space

TPS distinguishes reproduction of a camera view from reconstruction of a unique physical camera state. Camera position, orientation, reference measurements, and optical parameters remain important because they provide practical means of approaching a recorded view. They are instrumental to recovery, rather than the final criterion by which recovery is judged. The common reference is the projected image, whose formation from physical geometry is described by perspective-projection models [13].

Physical measurements constrain the recovery process; explicit A→a, B→b, and C→c correspondence establishes reference image positions; and registered comparison provides feedback for camera adjustment. This makes visual refinement a meaningful part of the method rather than an alternative to measurement. Nevertheless, agreement at three points does not establish agreement elsewhere in the image.

In cinematic production, visual coherence can also support the perception of a single represented or diegetic world. Film studies uses *diegesis* for a film's story or narrative world [14]. Film-production choices establish a coherent and credible diegesis through elements such as sets, props, lighting, and staging [15]. Practical compositing guidance likewise treats compatible perspective, scale, framing, lighting, and related image conditions as important when combining independently produced elements [16]. These sources provide context for TPS's view-oriented objective, but do not demonstrate that TPS alone can achieve whole-image coherence or diegetic continuity. Those outcomes depend on additional scene and imaging conditions and require systematic characterization.

## 10. Future Validation

A first practical demonstration can test the complete TPS workflow without establishing a universal performance threshold. Record a reference image and the three identified physical points, their measured triangle, image coordinates, coordinate frame, D, and available camera quantities. Remove or move the camera, then attempt recovery using a registered reference overlay. Preserve the recovered image and compare the three reference-point positions, together with several visible scene features outside the triangle. Report the observed differences, setup conditions, and any operator adjustments without treating three-point agreement as proof of full-image agreement.

Later work could compare repeatability across operators or camera systems and separately evaluate Working Focal Length against independently measured optical parameters. Those studies are extensions, not prerequisites for presenting the reference method. No experimental result is asserted here.

## 11. Conclusion

TPS is a reference-based method for camera-view reproduction. It connects three identified physical points with the locations where those points appear in an image. A TPS reference preserves correspondence, image coordinates, physical triangle measurements, coordinate-frame information, a measured TPS Reference Distance, and related Working Focal Length and AOV information when available.

The method is independent of software, hardware, operating system, file format, and recording medium. Recovery compares a registered reference with a live view and adjusts toward the closest practical match; three-point agreement does not establish a unique camera configuration or complete scene alignment.

The mathematical foundations and many operational components have clear precedents. Photogrammetric resection and P3P establish related physical/image geometry. Rephotography establishes the goal of returning to a prior view. Fiducial registration, astronomy, homography, VFX surveying, and stop-motion overlays establish related methods of correspondence, registration, and practical alignment. The possible contribution of TPS is the constrained, portable combination of these ideas for view matching without camera solving. That possibility remains to be tested and compared, not asserted as established originality.

## 12. References

[1] Carl Chow, “Photogrammetric Space Resection,” *Transactions of the American Society of Civil Engineers* 115(1), 1950, pp. 235–259. DOI: https://doi.org/10.1061/TACEAT.0006318.

[2] Open AGH, *Basics of Photogrammetry*, “Basics of Photogrammetry” module. https://epodreczniki.open.agh.edu.pl/handbook/4795/module/4812/reader.

[3] OpenCV, “Perspective-n-Point (PnP) pose computation,” version 4.10.0 documentation. https://docs.opencv.org/4.10.0/d5/d1f/calib3d_solvePnP.html.

[4] “Heritage and Repeat Photography: Techniques, Management, Applications, and Publications,” *Heritage* 5(4), 2022. https://doi.org/10.3390/heritage5040220.

[5] OpenCV, “Basic concepts of the homography explained with code.” https://docs.opencv.org/4.5.1/d9/dab/tutorial_homography.html.

[6] M. Beroiz, J. B. Cabral, and B. Sanchez, “Astroalign: A Python module for astronomical image registration,” *Astronomy and Computing* 32, 2020, article 100384. DOI: https://doi.org/10.1016/j.ascom.2020.100384.

[7] Sajjad Mohammadian et al., “High accuracy, fiducial marker-based image registration of correlative microscopy images,” *Scientific Reports* 9, 3211, 2019. DOI: https://doi.org/10.1038/s41598-019-40098-4.

[8] Science-D-Visions, *3DEqualizer Technical Specification*. https://www.3dequalizer.com/?item=tech_spec&site=start.

[9] Mike Seymour, “3DEqualizer – German precision where VFX needs it,” *fxguide*, 2014. https://www.fxguide.com/quicktakes/3dequalizer-german-precision-where-vfx-needs-it/.

[10] Australian Film Television & Radio School, *Stop Motion*, pp. 14–15. https://medialab.aftrs.edu.au/wp-content/uploads/2021/07/AFTRS16_StopMotion.2021.pdf.

[11] Tom Gasek, “Objects, People, and Places,” in *Frame-by-Frame Stop Motion: The Guide to Non-Puppet Photographic Animation*, Chapter 6, pp. 104–105. Publisher chapter PDF: https://www.bloomsburyvisualarts.com/app/downloadpdf?docIdS=b-9781315155166.

[12] DZED Systems, *Using Dragonframe 2025*. https://www.dragonframe.com/download/Using%20Dragonframe%202025.pdf.

[13] MIT, *Foundations of Computer Vision*, §5.3.1, “Image Formation by Perspective Projection.” https://visionbook.mit.edu/imaging.html.

[14] Columbia University, *Film Language Glossary*, “Diegesis.” https://filmglossary.ccnmtl.columbia.edu/term/diegesis/.

[15] Oklahoma State University Open Textbooks, *Introduction to Film & TV*, “Mise en scène.” https://open.library.okstate.edu/introfilmtv/part/mise-en-scene/.

[16] Adobe, “What makes amazing creative compositing.” https://www.adobe.com/learn/photoshop/web/photography-effects.

==================================================
SOURCE: research/notes/PROJECTIVE_CONTINUITY_RESEARCH_NOTE.md
==================================================
# Projective Continuity Across Physical, Digital, and Cinematic Space

**Research note — working draft**  
**Christopher Weinberg · LIMNMEDIA · October 2026**

## Scope

This note explores the relationship between physical geometry, photographic projection, visual coherence, and cinematic continuity. It is a conceptual interpretation and set of research hypotheses, not a claim that TPS has been experimentally validated or that “projective continuity” is an established named theory with the definition proposed here.

## Central proposition

A camera relationship can remain useful across different physical or digital spaces when the projective relationships needed for the intended view are preserved or recovered. Physical coordinates help constrain the recovery, but agreement in the image is the operational target.

## Reasoning

**1. Physical and represented space differ.** Perspective projection maps three-dimensional points to two-dimensional image positions [1]. An image does not uniquely encode every physical condition of its production.

**2. A cinematic image can depict a coherent world assembled from distinct production spaces.** Film theory calls the represented narrative world the *diegesis* [2]. Film-production choices can establish a credible, internally coherent diegetic world even though it is distinct from physical reality [3].

**3. Coherence is an image-level achievement, not proof of common physical coordinates.** Compositing practice emphasizes matching perspective, scale, framing, lighting, and shadows across separately produced elements [4]. This supports the narrower observation that visually compatible elements may read as one image; it does not prove they have identical underlying geometry.

**4. View recovery need not equal unique camera reconstruction.** TPS records A→a, B→b, C→c and physical reference measurements. These constrain an operator-guided attempt to reproduce a projection, without solving for a unique camera state. Multiple camera configurations can share three-point image correspondences, and those correspondences alone do not ensure whole-image agreement [5].

**5. Visual refinement is part of the recovery logic.** Measurement narrows the search; image correspondence supplies targets; registered comparison exposes differences; camera adjustment reduces visible mismatch. Features outside the reference triangle remain necessary checks.

**6. Cross-space portability is a testable possibility.** A reference might guide transitions such as physical set → digital scene → physical reconstruction, or original camera → replacement camera. Such transfers need not share one world-coordinate system, but they do require interpretable correspondence and sufficiently compatible scene geometry and imaging conditions.

## Conceptual chain

Physical geometry → projection → correspondence → visual coherence → diegetic continuity → possible cross-space portability.

These are **not logical equivalences**. In particular, point correspondence does not entail whole-image coherence, and visual coherence does not necessarily entail narrative or diegetic continuity. The chain describes progressively broader goals and possible consequences.

## Relationship to TPS

TPS directly specifies physical/image correspondence and an operator-guided comparison method. “Projective continuity” is a proposed descriptive frame for its view-recovery objective. “Diegetic continuity” describes a possible cinematic consequence of a convincing result, not a measurable output of the TPS kernel.

## Research questions

1. How closely can TPS recover a view after camera removal or replacement?
2. How well do non-reference scene features align after the three reference points agree?
3. Can a reconstructed or scaled reference triangle support comparable projection?
4. Can TPS references guide physical-to-digital and digital-to-physical camera alignment?
5. How do lens distortion, scene depth, camera differences, and operator judgment limit transfer?

## Boundaries

No unique camera pose, complete scene match, scale independence, or universal optical equivalence is claimed. Proposed cross-medium portability requires controlled experiments. The cinematic terminology contextualizes the problem; it does not establish TPS's effectiveness or novelty.

## Sources

[1] MIT, *Foundations of Computer Vision*, “Image Formation by Perspective Projection.” https://visionbook.mit.edu/imaging.html

[2] Columbia University, *Film Language Glossary*, “Diegesis.” https://filmglossary.ccnmtl.columbia.edu/term/diegesis/

[3] Oklahoma State University Open Textbooks, *Introduction to Film & TV*, “Mise en scène.” https://open.library.okstate.edu/introfilmtv/part/mise-en-scene/

[4] Adobe, “What makes amazing creative compositing.” https://www.adobe.com/learn/photoshop/web/photography-effects

[5] Christopher Weinberg, *The Three Point System: A Reference-Based Method for Camera-View Reproduction*, Paper 1 working draft, §§2, 7–10.

==================================================
SOURCE: research/methods/TPS_CAMERA_LINEUP_GEOMETRY.md
==================================================
# TPS Camera Lineup: Operational Method and Geometric Foundations

**Working technical draft · October 2026 · Christopher Weinberg / LIMNMEDIA**  
**Status:** Research-method draft for author review; not a normative amendment to TPS Specification v0.1.

## Abstract

The Three Point System (TPS) records correspondence between three identified physical points (A, B, C) and their image projections (a, b, c), together with physical measurements and camera-reference quantities. This document develops the *operator-guided lineup* method for reproducing a previously photographed view: establish shared UP; measure and lock camera tilt; establish the lens/focus condition and Working Focal Length; use TPS Reference Distance as an initial geometric guide; register the A–B Base Pair with pan, height, and horizontal translation; use the third point C and its parallax response to refine depth translation (zT); and finally minimize whole-view disagreement while preserving the tilt constraint. The sequence is a documented practical method, not a unique camera-pose solver. Established perspective geometry, an image-motion Jacobian, and local conditioning analysis explain its behavior and limits. Where precise adjustment rules have not yet been established experimentally, this draft marks them as working heuristics.

## 1. Purpose, scope, and provenance

**Kernel:** “TPS connects three points in the physical world with where those same three points appear in an image.” TPS preserves identities A→a, B→b, C→c; the physical triangle is not generally similar to the projected triangle. The desired result is *view recovery*, not necessarily recovery of the original six-degree-of-freedom pose or exact lens model. The reference is independent of cameras, stages, coordinates, applications, and media.

This operational method was distilled from Christopher Weinberg's professional camera, motion-control, and VFX practice and subsequently formalized as TPS through LIMNMEDIA. It is not represented as an official method, deliverable, or endorsement of any former employer or production. The mathematical components are established; their particular organization and performance under production conditions require characterization.

**Evidence/status labels used here:** **Established** = follows from standard geometric or differential models under stated assumptions; **Method** = specified operator practice; **Hypothesis** = useful predicted behavior to test; **Open** = not yet settled by the available method description.

## 2. What must be recorded

### 2.1 Physical reference

- Three stable, unmistakably identifiable physical locations A, B, C; natural set features are acceptable. Preserve their identities, not just triangle shape.
- Physical lengths AB, BC, CA (and measurement units), plus how the triangle was surveyed or recreated. Side lengths specify triangle shape up to rigid transformation/reflection, **not** its position in a world coordinate system.
- A designated A–B Base Pair. For Working Focal Length calculations, select A/B at approximately equal optical depth and with AB approximately camera-horizontal; this is a **calculation assumption**, not a general TPS correspondence requirement.
- A useful C, preferably non-collinear in the *image* and at a depth distinct enough from A/B to produce diagnostic parallax when possible. Depth separation is advantageous for particular translation diagnostics, but is not mandatory for TPS correspondence.
- TPS Reference Distance D and its practical measurement target associated with A–B. Depending on the physical arrangement, the operator may measure from a sensor-plane mark to A, B, the A–B midpoint, or an estimated midpoint. Record the selected endpoints, tool, direction, and any approximation. A laser distance meter held alongside the camera near the sensor-plane mark is one practical method; survey-grade equipment is not required.

### 2.2 Image and camera reference

- A-side reference image, **actual captured pixel dimensions**, point coordinates a/b/c, coordinate origin, axes, rotation/mirroring/crop, and any justified image-to-live display registration.
- Tilt relative to physical gravity/UP (or a declared UP direction in CG); roll when available. Measure with an inclinometer square to the camera's relevant reference surfaces, taking camera roll into account. Document sign conventions and device accuracy.
- Focus setting or focus distance (operationally important because lens breathing changes the projection); lens identification and focal setting when known. Record the **Working Focal Length** and its assumptions rather than silently substituting nominal lens markings.
- Active sensor dimensions when known and valid for the *captured image mode*; they are not required to preserve image-space focal length or AOV.
- Optional notes: lens distortion, nodal/non-parallax behavior, motion-control offsets, physical access restrictions, frame in a camera move, set changes, and reference quality.

### 2.3 Camera variables and notation

Let `T_x,T_y,T_z` denote camera translation along declared axes; `R_x,R_y,R_z` denote camera rotations. **zT means Z translation**, not zoom. The operational directions *height*, *horizontal X*, and *depth Z* must be mapped to stage axes explicitly; no common origin between A-side, B-side, or CG is required. UP is a shared *direction* (gravity in the physical world, declared vertical in CG), not a shared coordinate origin. Distinguish physical stage axes from camera-local axes throughout.

## 3. Complete physical lineup procedure

The procedure below is the working author-described sequence. Some steps can interact; “lock” means a controlled constraint during convergence, not that all other degrees of freedom have mathematically vanished.

### Phase A — Record the A-side

**A1. Choose the geometry.** Identify A/B as the Base Pair and C as an independent third point. Prefer stable features that can be physically relocated or recreated, with clear visibility and a useful image triangle. Record point identity photographically as well as numerically. Avoid points that will be occluded or animated between setups.

**A2. Capture the reference.** Preserve the original A-side frame and its exact image-coordinate convention. Mark a/b/c at the actual physical feature locations; do not move the image marks to make a visually pleasing triangle.

**A3. Measure.** Measure AB, BC, CA and D as accurately as practical. Select the D target—A, B, the A–B midpoint, or an estimated midpoint—according to the physical arrangement. A laser distance meter may be held alongside the camera near the sensor-plane mark, using the focal-plane mark when available. Record the endpoints, direction, tool, and uncertainty. Do not treat D as automatically equal to optical-center depth, perpendicular depth, or camera-forward-axis distance. Record tilt and roll with a square/inclinometer. Record focus distance/setting and lens state. Where sensor width is unknown, preserve image-space quantities rather than guessing millimeters.

**A4. Derive and preserve the optical reference.** Under the assumptions in §5, compute `f_px`, `AOV_h`, and, if active sensor width is known, `f_mm`. Preserve inputs and assumptions with results. Do not assume these quantities reconstruct a full lens model.

### Phase B — Prepare the B-side

**B1. Recreate or identify A/B/C.** Verify point identities and physical side lengths. If the geometry has changed, document it and decide whether the original correspondence remains valid. A similar triangle at another scale is a *different experimental condition*, not automatically an identical physical reference.

**B2. Register the image frames.** Display the saved A-side points and image over the live B-side view using an explicitly known frame mapping (same sensor mode, declared crop/rotation, or independently justified mapping). Do not warp the live image to force the three points into agreement: that would conceal camera error.

**B3. Establish UP and set tilt.** Determine the same vertical reference in both setups. Set the camera's measured tilt and **keep tilt locked through ordinary lineup**. Preserve or explicitly resolve roll, rather than letting roll errors masquerade as A–B translation. If the camera is rolled, measure tilt in a manner that accounts for the rolled camera reference frame. **Method:** tilt precedes Base Pair scale and alignment.

**B4. Restore optical condition.** Set the intended lens/focal state and the recorded focus distance or focus condition before fine registration. Focus breathing may mimic a change in focal length or camera depth. The *known/working focal length* and the *focus setting* are related but not interchangeable: record both if available. Where the exact lens is unavailable, use Working Focal Length/AOV as a starting guide and expect residual lens differences.

**B5. Establish initial conditions.** Restore the recorded tilt, Working Focal Length, focus/lens condition, and D as closely as practical. Use D as an initial physical guide, without treating it as a solved camera pose. The measurement is from the **sensor plane** to a practical A–B-associated target; ideal pinhole projection is from an optical center, so the difference and measurement uncertainty may influence the recovered projection.

### Phase C — Register the Base Pair

**C1. Observe the A–B mismatch.** Compare live a′/b′ to saved a/b in the same image frame. Examine pair midpoint, pair separation, pair angle, and the two individual residual vectors. These observables are more informative than a single scalar “match” score.

**C2. Adjust by visual feedback.** With tilt held fixed and optical condition stabilized, observe the overlay, make a small adjustment to whichever camera control appears appropriate, and observe the resulting displacement. Pan and horizontal X translation can produce similar horizontal image displacement; tilt and camera height can produce similar vertical displacement; Z translation can change projected scale; tilt, height, and Z can interact; and roll can affect apparent triangle angle. These are qualitative relationships, not universal equivalences. There is **no mandatory camera-axis order and no one-control-to-one-image-effect mapping**; recheck both endpoints after each adjustment.

**C3. Diagnose rather than compensate blindly.** A pair that matches in midpoint but not separation suggests a scale/geometry/intrinsics issue; a pair that matches in separation but not midpoint suggests displacement/rotation. These are *diagnostic tendencies*, not unique causes. A pan about a pivot displaced from the entrance pupil also introduces translation and parallax. If A/B repeatedly diverge after C adjustments, revisit focus, D, point identity, roll, and the Base Pair assumptions.

### Phase D — Resolve C and refine

**D1. Introduce C after A/B are useful.** Measure c′−c and compare its direction/magnitude with residuals at a/b. C is an additional geometric constraint and diagnostic reference, particularly when it differs in depth from the Base Pair. A C residual may prompt investigation of roll, height, tilt, Z translation, scale, Working Focal Length, A-side measurements, nominal lens or EXIF values, or other discrepancies. It does not uniquely diagnose any one cause.

**D2. Refine using all three points.** Adjust whichever camera parameter appears appropriate, including a cautious test of declared rig Z translation (`zT`) when its predicted image effect is relevant. A small roll adjustment may improve the recovered image even when recorded roll was zero, because it may compensate for another discrepancy; it does not prove the original roll was nonzero. The operator must return to A/B after each move. No residual uniquely diagnoses a particular adjustment.

**D3. Iterate with tilt preserved.** Cycle A/B → C → A/B. Make progressively smaller adjustments as appropriate, while recognizing that improving C may disturb A/B. If convergence stalls, check optical/focus state, camera pivot, lens distortion, scene geometry, frame registration, and whether the chosen triangle is poorly conditioned. Releasing tilt is a documented exception requiring a reason, not an unrecorded convenience.

**D4. Evaluate the whole image.** Inspect scene features outside A/B/C and, for moving shots, additional frames along the motion path. Three matched points can coexist with wrong background parallax, scale, lens distortion, or nodal behavior. Record both point residuals and whole-image observations. A good TPS result is an operationally useful view match, not proof of unique camera reconstruction.

**D5. Preserve the recovery record.** Capture B-side image(s), final measured settings, residuals, adjustments, and any deliberate departures from the nominal reference. Distinguish a recovered shot from a reference whose image was digitally warped after capture.

## 4. Why this sequence can help: geometry and constraints

**Established:** A pinhole camera projects 3D points by perspective division; image motion responds differently to translation and rotation, and to the depth of each point. **Method:** the operator establishes useful initial conditions, uses the Base Pair to establish a visible reference, then uses C to diagnose remaining misregistration through iterative visual feedback. **Hypothesis:** this approach may reduce operator confusion or incorrect compensating adjustments compared with unconstrained trial and error. No mandatory sequence or superiority claim is established.

### 4.1 UP and tilt are not a solved camera pose

Shared UP removes an arbitrary choice of vertical direction between spaces. Locking measured tilt reduces the adjustable parameter space and can make operator control more predictable. It does not fix pan, roll, translation, optical center, or focal state, nor does it establish common world coordinates. In CG, tilt is relative to declared world UP; in physical space, it is measured relative to gravity. Instrument mounting and camera roll must be accounted for.

### 4.2 The Base Pair provides interpretable image observables

For two image points `a=(u_A,v_A)` and `b=(u_B,v_B)`, define midpoint `m=(a+b)/2`, displacement `d=b−a`, length `s=||d||`, and image angle `φ=atan2(d_v,d_u)`. Two points supply four scalar image measurements. Under ideal fronto-parallel equal-depth geometry, projected separation mainly reflects the ratio of focal length to depth; this is why the pair is a useful scale cue. But a change in focal length can mimic a change in depth for the pair, and a change in camera rotation can shift its midpoint. Base Pair agreement alone is not a complete camera solution.

### 4.3 The third point provides additional information

C adds two image-coordinate residuals, making six measured scalar residuals for three points. For a *known rigid 3D triangle, calibrated ideal camera, and nondegenerate configuration*, three correspondences may constrain a finite set of poses (P3P), **not necessarily one**. TPS does not require such a solve. With unknown lens parameters, imperfect measurements, movable points, or pivot offsets, ambiguities increase. A depth-separated C can be useful because its parallax under selected translations differs from that of A/B, but this is an optional diagnostic advantage, not a TPS requirement. C can also reveal possible roll, tilt, height, scale, focal-length, measurement, or metadata discrepancies without uniquely identifying their cause.

### 4.4 Why translation and rotation should not be confused

For an ideal pinhole camera and small camera-local **lateral translation** `δT_x`, keeping orientation and intrinsics fixed, the image displacement of point i is approximately `δu_i = −(f_x/Z_i) δT_x`. Thus

`δu_C − δu_A ≈ −f_x δT_x (1/Z_C − 1/Z_A)`.

The differential vanishes when the two depths are equal, making this particular cue unavailable. **But this expression is for lateral translation, not for zT.** For camera-local **axial translation** `δT_z`, with other parameters fixed:

`δu_i ≈ (f_x X_i/Z_i²) δT_z = (u_i−c_x) δT_z/Z_i`,  
`δv_i ≈ (f_y Y_i/Z_i²) δT_z = (v_i−c_y) δT_z/Z_i`.

Axial movement produces expansion/contraction about the principal point with depth-dependent magnitude. It can help distinguish C's behavior from A/B, but a single residual at C is not proof that zT is the sole required adjustment. The sign of displacement depends on the translation convention.

## 5. Projection model and TPS Working Focal Length

### 5.1 Ideal perspective projection

For a point `P_w`, camera center `C_w`, and world-to-camera rotation `R`, set `P_c = R(P_w−C_w) = (X,Y,Z)`, with `Z>0`. In undistorted pixel coordinates:

`u = f_x X/Z + c_x`  
`v = f_y Y/Z + c_y`.

Real lenses introduce distortion, focus breathing, pupil movement, and other departures. The ideal model is an analytical baseline, not a claim that every practical camera is a pinhole.

### 5.2 Existing approved TPS equations (do not redefine)

`f_px = |x_B−x_A| D / AB`  
`AOV_h = 2 atan(AB W_image / (2 D |x_B−x_A|))`  
`f_mm = f_px W_sensor / W_image`.

`x_A,x_B` are roll-corrected horizontal pixel coordinates; `W_image` is **captured image width**, not necessarily native sensor pixel width; `W_sensor` is active physical sensor width for that captured mode. The millimeter conversion is omitted when active sensor width is unknown. `D` is the practical sensor-plane reference measurement. These equations assume approximately equal A/B optical depth and horizontal AB alignment, plus the approximation `D≈Z` from projection center to the reference. They do **not** apply unconditionally to arbitrary A/B orientation or triangle geometry. `f_px` is a *Working* Focal Length, not necessarily the laboratory focal length.

### 5.3 Tilt/reference-distance triangle: important convention check

A prior practical description treats the tilt line as a triangle's hypotenuse and proposes component relationships. With `Z` defined as horizontal camera-forward distance and `H` as vertical distance, if `θ` is measured from horizontal, the components are `ΔZ = D cos θ` and `ΔH = D sin θ`. If `θ` is measured from vertical, they are `ΔZ = D sin θ` and `ΔH = D cos θ`. In either case, `D` must be the slanted hypotenuse between the two selected endpoints and the horizontal/vertical axes must be defined in the same plane. If D is a sensor-plane-to-*plane* distance measured along the optical axis, neither construction can be adopted automatically. The measured camera *tilt*, tape-line inclination, and optical-axis inclination are not necessarily identical. **Open for author verification:** instrument zero convention; the exact D tape line; sign conventions; whether the earlier ΔZ/ΔH labels refer to stage depth and height. Do not silently embed either triangle in normative TPS calculations.

## 6. Differential image motion: the Jacobian

### 6.1 Camera motion as image motion

Let normalized image coordinates be `x=X/Z`, `y=Y/Z`; use square-pixel pinhole intrinsics for this derivation (`u=f_x x+c_x`, `v=f_y y+c_y`). Define a *camera velocity* twist `(v_x,v_y,v_z,ω_x,ω_y,ω_z)` expressed in camera coordinates. For a static scene, camera-coordinate point motion is `Ṗ_c = −v − ω×P_c`. Differentiating gives the standard **interaction matrix** (image Jacobian):

```
[x_dot]   [ -1/Z   0    x/Z     x*y    -(1+x²)    y ] [v_x]
[y_dot] = [  0   -1/Z   y/Z   (1+y²)    -x*y     -x ] [v_y]
                                                       [v_z]
                                                       [ω_x]
                                                       [ω_y]
                                                       [ω_z]
```

Read the displayed matrix as a **2×6** matrix multiplying the **6×1** twist vector; the line breaks on the right are illustrative. Pixel-coordinate derivatives are `u_dot=f_x x_dot`, `v_dot=f_y y_dot` for fixed intrinsics. This convention assumes no changing focal length, crop, distortion, or moving reference points.

For three points, stack their 2×6 blocks into `J∈R^(6×6)` and their image residuals into `e∈R^6`. For sufficiently small camera motions,

`Δp ≈ J Δq`,

where `Δq` is a local twist increment in compatible units. For a physical crane with pan/tilt pivots away from the optical center, map **actual joint motion** to the camera twist using a rig kinematic Jacobian `G`: `Δp ≈ J G Δs`. This distinction is essential: turning a pan axis does not generally equal a pure rotation about the camera's entrance pupil.

### 6.2 The local adjustment problem

With reference coordinates `p_ref` and live coordinates `p_live(q)`, define `e(q)=p_live(q)−p_ref`. A small least-squares correction may be written

`Δq* = −(Jᵀ W J + λ I)⁻¹ Jᵀ W e`,

with positive weights `W` and regularization `λ≥0` when the inverse exists; a pseudoinverse/SVD formulation is preferable for rank-deficient cases. This is an **analysis and optional software-assistance model**, not a replacement for the human lineup. Constrain tilt by removing its column or enforcing `Δtilt=0`; optionally hold focal/focus state fixed. Solve in declared physical units with sensible scaling/regularization because meters and radians differ.

### 6.3 Why iterative feedback may be easier to operate

With useful initial conditions established, the operator uses overlay feedback rather than a rigid axis sequence. A/B midpoint, separation, and orientation are visible summaries of the residual. C tests whether a seemingly successful Base Pair alignment also holds at another image position/depth. This is conceptually related to **block-coordinate descent**, but the actual procedure selects adjustments from observed image response and has not been shown to converge monotonically or optimally. A/B alignment can be disrupted by later adjustments, requiring iteration. Never claim the Jacobian mathematically proves the method is globally optimal or superior to simultaneous adjustment.

### 6.4 Rank, singular values, and sensitivity

The singular values of a suitably normalized Jacobian indicate how distinguishable small camera motions are from the available image measurements. A very small singular value means some motion combination produces little detectable image change; noise can then cause large uncertainty. Rank and conditioning depend on the actual 3D point geometry, depths, focal length, view, and constrained degrees of freedom. Three points yield six residual components but do not guarantee a well-conditioned or globally unique solution. In particular, collinear image points, nearly coincident points, weak depth variation, and measurement noise may undermine practical recovery. A simulation should examine these cases rather than declare a universal “best triangle.”

## 7. Focus, focal length, pivots, and false matches

**Focus breathing.** Changing focus can alter angle of view and effective magnification. A change in image scale caused by breathing can be mistaken for zT or a focal-setting change. The practical method therefore establishes focus state before fine lineup and records changes. A future lens focal-length-versus-focus lookup table (LFLUT) may help characterize this dependence; it is not required for the core TPS reference.

**Zoom versus translation.** A zoom/focal change can reproduce the apparent size of a nearly fronto-parallel Base Pair while producing different parallax elsewhere. Therefore a matching A/B pair after changing focal length is not sufficient evidence of correct camera depth.

**Rotation pivot.** Pan/tilt/roll around a mechanical axis away from the optical projection center introduce coupled translation. The operator should document pivot geometry or evaluate its visible effects. An entrance pupil/non-parallax calibration may reduce this coupling but cannot be assumed exact for every lens/focus setting.

**Lens distortion and sensor modes.** Distortion may allow three points to agree while peripheral features disagree. Compare equivalent image frames and actual capture modes; a raw pixel match between differently cropped or rotated images is not meaningful without declared registration.

**Moving cameras.** One reference frame may be insufficient for a whole motion-control path. Sample multiple frames and examine continuity of A/B/C and other set features along the path; camera path, lens state, and pivot offsets can vary across frames.

## 8. Worked example: geometry and differential diagnosis

The following is an **illustrative mathematical example, not measured TPS performance**.

Take an ideal 1920-pixel-wide image, `f_x=1200 px`, principal point `c_x=960 px`, A/B at `Z=2.0 m`, separated horizontally by `AB=0.40 m`, centered about the optical axis. The projected A/B separation is

`Δu_AB = f_x AB/Z = 1200×0.40/2.0 = 240 px`.

If a measured sensor-plane distance `D=2.0 m` is substituted for Z under the TPS approximation, `f_px=240×2.0/0.40=1200 px`, and `AOV_h=2 atan(1920/(2×1200))≈77.3°`. This does not establish that the actual lens has a 1200-pixel pinhole focal length; it illustrates the assumptions.

Let C be at `Z_C=3.0 m`. For a small camera-local lateral movement `δT_x=0.010 m` (10 mm), with orientation fixed:

`δu_A≈−1200×0.010/2=−6 px`  
`δu_C≈−1200×0.010/3=−4 px`.

The difference, `δu_C−δu_A≈+2 px`, is a measurable parallax signature **if point marking and capture are sufficiently precise**. This is a lateral-translation demonstration; it does not justify choosing zT from the same equation.

For axial translation `δT_z=0.010 m`, a point at `u−c_x=120 px`, `Z=2 m`, shifts approximately `+0.6 px` under the declared convention; a point at the same pixel offset but `Z=3 m` shifts `+0.4 px`. Real measurements may be overwhelmed by image noise, lens effects, or mechanical play. The appropriate next step is to compute predictions for the actual A/B/C coordinates and the physical rig axes.

## 9. Failure modes and operator troubleshooting

| Observation | Possible explanations | Test before adjusting |
|---|---|---|
| A/B both displaced similarly | Translation, pan, frame registration | Verify overlay registration and fixed tilt |
| A/B midpoint matches, separation does not | Depth, focal state, focus breathing, AB geometry | Check focus/lens, D, AB, crop |
| A/B align but C does not | Parallax, changed triangle, pivot, distortion, wrong pose branch | Check C identity/depth and try controlled zT with A/B recheck |
| A/B and C align but background does not | Different camera pose/lens, distortion, nonrigid set | Inspect independent features and depth layers |
| Alignment shifts after focus adjustment | Focus breathing/pupil shift | Restore reference focus state |
| Pan shifts the image unexpectedly | Mechanical pivot offset, camera-axis coupling | Characterize rig kinematics |
| Repeatedly unstable adjustments | Poor triangle conditioning, noisy point locations, flex/backlash | Improve reference geometry and measurement |

These are diagnostic possibilities, **not one-to-one fault signatures**.

## 10. Physical, motion-control, and digital implementations

**Manual camera:** use physical tilt measurement, marked points, registered overlay, incremental pan/height/X/zT adjustments, and a written residual log. The method should remain executable without a specialized application.

**Motion-control crane:** record physical axis conventions, offsets, and pivot locations. Use the rig's joint-to-camera Jacobian `G` when predicting image motion. Account for backlash, axis calibration, and coupled translations during pan/tilt. The same projected triangle can be used as the visual acceptance reference; it does not imply the original motor counts have been recovered.

**Blender/Maya:** define world UP and image/camera conventions, use physical triangle coordinates if available, set camera tilt and lens state, and compare projected points in the render frame. Software may numerically minimize image residuals; that is an optional implementation. TPS itself does not require a common origin, automatic PnP solve, or a specific DCC. Proposed plugins must be described as planned until implemented and tested.

**LIMNTPS / TPS-Qt:** distinguish the reference record and export, operator guidance, and any future automatic optimization. Do not infer that a current application performs a mathematical pose solve or full Jacobian-based lineup without confirming its implemented behavior.

## 11. Experimental program and falsifiable predictions

**Experiment 1 — Recover a moved camera.** Capture A-side reference; record triangle, tilt, focus, D, image coordinates. Move/remove camera, then use the stated ordered lineup. Measure point reprojection error (pixels or normalized image width), off-triangle landmark error, time to convergence, number of adjustments, and operator variability. Repeat across trials and operators. Compare with a baseline such as unguided overlay-only lineup.

**Experiment 2 — Recreate the set triangle.** Remove and rebuild the reference geometry. Measure side-length/point-location reconstruction error separately from camera recovery error. Do not attribute set errors to camera pose alone.

**Experiment 3 — Scale transfer.** Rebuild triangle and scene at known scale ratios. Specify which distances, focal conditions, and depth relationships are scaled. Evaluate whether corresponding image projections and off-triangle landmarks agree; record departures due to optics and miniature construction.

**Experiment 4 — Physical-to-digital.** Scan/survey A-side set, reconstruct A/B/C in Blender, and recover a virtual camera through the same staged correspondence workflow. Compare render and original in registered image space, accounting for material/lighting differences and lens model. Distinguish geometric registration from visual/diegetic coherence.

**Specific hypotheses:** (H1) locked-tilt staged lineup reduces adjustment time relative to free six-axis search; (H2) useful C depth separation improves sensitivity to certain translation errors; (H3) restoring focus state reduces false depth compensation; (H4) point residuals alone are an incomplete predictor of whole-image match. Report counterexamples and failure cases.

## 12. Reporting metrics and uncertainty

Let `r_i = p_live,i−p_ref,i` in registered pixel coordinates. Report per-point `||r_i||`, RMS point error `sqrt((||r_A||²+||r_B||²+||r_C||²)/3)`, and maximum error. Normalize by image width or diagonal when comparing sensor modes. Evaluate *additional* landmarks outside the TPS triangle, preferably at multiple depths. Report point-marking uncertainty, ruler/inclinometer uncertainty, lens/focus state, frame mapping, camera control increments, backlash, and set reconstruction tolerance. Distinguish repeatability (same operator/setup), reproducibility (different operator/equipment), and accuracy against a declared reference. Define acceptable tolerances per shot; do not invent a universal TPS threshold.

## 13. Relationship to Paper 1 and the specification

Paper 1 currently describes reference creation and overlay-guided recovery but says TPS **does not prescribe an adjustment order**. This document proposes an explicit *operational lineup procedure*. Until the author approves the exact steps and the specification's normative scope is decided, retain that distinction: **the TPS kernel/reference is implementation-independent; the ordered camera lineup is a documented method for using it, not automatically a universal requirement of the specification**. After review, Paper 1 can include a concise procedure and cite this detailed method without replacing its equations or overstating experimental results.

## 14. Items requiring author review before normative use

1. Confirm the exact tilt instrument reference and angle convention, especially when the camera is rolled.
2. Confirm whether D is the straight sensor-mark-to-A/B-midpoint tape distance, an optical-axis distance, or another measurement in the geometric triangle construction.
3. Confirm the exact use of pan, height, horizontal X, and zT; whether any are locked during the C step, and which mechanical stage axes those names denote.
4. Confirm whether **focus distance** must precede Working Focal Length or whether the practical workflow treats them as a single lens-state setup step.
5. Confirm when roll is locked or actively adjusted and how it is measured.
6. Confirm whether C is ordinarily above/below the Base Pair in the frame, physically depth-separated, or both; these are distinct geometric properties.
7. Confirm the treatment of lens calibration, nodal/entrance-pupil shifts, multi-pass scale changes, and moving-camera frame selection in the *core* procedure versus advanced extensions.

These are precision questions, not reasons to withhold the draft. No missing answer has been silently elevated into a mathematical requirement.

## 15. Mathematical and technical precedents (for citation development)

- Perspective camera projection and camera calibration: standard photogrammetry and computer-vision treatments; see the existing TPS Paper 1 references for collinearity and PnP/P3P.
- P3P multiple-solution ambiguity: OpenCV `solveP3P` documentation, already cited in Paper 1.
- Image Jacobian / interaction matrix: classical image-based visual servoing (IBVS) literature; verify a specific authoritative citation before publication (e.g., Chaumette and Hutchinson, *Visual Servo Control, Part I: Basic Approaches*, IEEE Robotics & Automation Magazine, 2006).
- Camera motion versus lens/optical state: lens calibration and VFX matchmoving literature already discussed in Paper 1.
- TPS reference conventions and approved Working Focal Length equations: TPS Specification v0.1 and `research/papers/PAPER_01_REVISED.md` (local authoritative project sources).

---

**Editorial principle:** The mathematics explains *how camera adjustments affect image correspondence*. It does not prove that a particular operator sequence is globally optimal, that three correspondences uniquely recover a camera, or that whole-image/diegetic continuity follows from a three-point match.

==================================================
SOURCE: research/methods/TPS_LINEUP_MATHEMATICAL_VERIFICATION.md
==================================================
# TPS Lineup — Mathematical Verification Report

**Status:** Research verification draft; not a normative amendment to TPS Specification v0.1.

## 1. Scope and conclusion

This report independently checks the perspective-motion equations, sign conventions, numerical example, tilt/reference-distance construction, and staged A–B → C lineup reasoning in `TPS_CAMERA_LINEUP_GEOMETRY.md`.

The principal result is positive: the image Jacobian in the lineup draft is correct for its stated convention. The convention is:

- Camera coordinates are right-handed: `X` is image-right, `Y` is image-up, and `Z` is forward from the camera into the scene.
- A static world point has camera coordinates `P=(X,Y,Z)` with `Z>0`.
- `v=(v_x,v_y,v_z)` is camera-center velocity expressed in camera coordinates.
- `ω=(ω_x,ω_y,ω_z)` is camera angular velocity expressed in camera coordinates.
- Positive camera motion changes point coordinates by `P_dot = -v - ω × P`.
- Perspective projection is `x=X/Z`, `y=Y/Z`, `u=f_x x+c_x`, and `v_image=f_y y+c_y`.

The draft contained one trigonometric wording error in its tilt/reference-distance discussion. It stated the `D sin θ`/`D cos θ` assignment in a way that reversed the stated horizontal/vertical angle interpretation. That paragraph has been corrected in the research draft. The correction does not change TPS canonical mathematics or the approved meaning of `D`.

The A–B → C sequence is mathematically plausible as a staged operator heuristic, but it does not follow as a universally optimal or uniquely determined algorithm. A depth-separated C can improve sensitivity to some translation modes, while an equal-depth or poorly placed C may not. The sequence remains a proposed method requiring experiments.

## 2. Independent Jacobian derivation

Let:

```text
P = (X, Y, Z)
x = X/Z
y = Y/Z
```

For camera translation and rotation under the declared convention:

```text
X_dot = -v_x - ω_y Z + ω_z Y
Y_dot = -v_y - ω_z X + ω_x Z
Z_dot = -v_z - ω_x Y + ω_y X
```

Using the quotient rule:

```text
x_dot = (X_dot Z - X Z_dot) / Z²
y_dot = (Y_dot Z - Y Z_dot) / Z²
```

Substituting `X=xZ` and `Y=yZ` gives:

```text
x_dot = -v_x/Z + x v_z/Z
         + x y ω_x - (1+x²) ω_y + y ω_z

y_dot = -v_y/Z + y v_z/Z
         + (1+y²) ω_x - x y ω_y - x ω_z
```

Therefore:

```text
[x_dot]   [ -1/Z   0    x/Z     x*y    -(1+x²)    y ] [v_x]
[y_dot] = [  0   -1/Z   y/Z   (1+y²)    -x*y     -x ] [v_y]
                                                       [v_z]
                                                       [ω_x]
                                                       [ω_y]
                                                       [ω_z]
```

The matrix in the lineup draft is therefore internally consistent with its stated camera-motion convention. Pixel derivatives are:

```text
u_dot = f_x x_dot
v_image_dot = f_y y_dot
```

for fixed intrinsics and no distortion, crop, or rolling-shutter terms.

The signs are convention-dependent. If `v` denotes point velocity rather than camera-center velocity, or if positive camera axes are defined differently, translation signs change. A publication-quality version must retain the convention next to the matrix.

## 3. Motion interpretation

### 3.1 Lateral translation

For positive camera-center translation `v_x`, with orientation fixed:

```text
u_dot_i = -f_x v_x/Z_i
```

All points move in the negative image-horizontal direction for positive `v_x` under this convention. The differential between points A and C is:

```text
u_dot_C - u_dot_A = -f_x v_x (1/Z_C - 1/Z_A)
```

If `Z_C = Z_A`, this differential is zero. Thus depth separation is useful for diagnosing this particular lateral-translation cue. It is not a universal requirement for TPS correspondence.

### 3.2 Axial translation

For positive camera-center translation `v_z`:

```text
u_dot_i = f_x x_i v_z/Z_i
v_image_dot_i = f_y y_i v_z/Z_i
```

The image expands about the principal point for points with positive normalized coordinates and contracts toward it for negative coordinates, under the declared convention. A point on the principal point has no first-order axial image displacement. Therefore axial translation cannot be diagnosed reliably from a point configuration concentrated at or near the principal point.

This verifies the draft's statement that `zT` can produce depth-dependent expansion/contraction. It does not prove that `zT` is the correct or sole adjustment for every residual at C.

### 3.3 Rotation

For positive camera angular velocities:

```text
ω_x: x_dot = x y ω_x,       y_dot = (1+y²) ω_x
ω_y: x_dot = -(1+x²) ω_y,  y_dot = -x y ω_y
ω_z: x_dot = y ω_z,         y_dot = -x ω_z
```

These are image-space effects for rotations about camera-local axes. A physical pan, tilt, or roll control may not be a pure camera-local rotation because its mechanical pivot can be displaced from the projection center. The rig's joint-to-camera kinematics must then be included. Consequently, “pan,” “tilt,” and “roll” cannot be assigned universal image effects without a declared rig frame and pivot geometry.

## 4. Numerical example recalculation

The draft uses:

```text
W_image = 1920 px
f_x = 1200 px
c_x = 960 px
Z_A = Z_B = 2.0 m
AB = 0.40 m
```

For a centered horizontal base pair:

```text
u_A = 960 - (1200 × 0.20 / 2.0) = 840 px
u_B = 960 + (1200 × 0.20 / 2.0) = 1080 px
Δu_AB = 1080 - 840 = 240 px
```

Using `D=2.0 m` as the TPS approximation:

```text
f_px = 240 × 2.0 / 0.40 = 1200 px
AOV_h = 2 atan(1920 / (2 × 1200))
      ≈ 77.32°
```

These calculations are correct and dimensionally consistent under the stated ideal assumptions.

For a lateral camera-center translation `v_x=0.010 m`:

```text
Δu_A = -1200 × 0.010 / 2.0 = -6 px
Δu_C = -1200 × 0.010 / 3.0 = -4 px
Δu_C - Δu_A = +2 px
```

More precisely, these are the first-order image displacements associated with the stated 10 mm motion. The result is a 2 px differential under the ideal model.

For axial camera-center translation `v_z=0.010 m`, a point with `u-c_x=120 px` has `x=120/1200=0.1`:

```text
Δu_A ≈ 1200 × 0.1 × 0.010 / 2.0 = +0.6 px
Δu_C ≈ 1200 × 0.1 × 0.010 / 3.0 = +0.4 px
```

The sign is positive because the report defines positive camera-center motion along +Z and uses `P_dot=-v` for static scene points. A different translation convention reverses the sign.

The example is mathematically correct as an idealized first-order calculation. It is not an accuracy claim. Lens distortion, marking uncertainty, pixel sampling, focus changes, mechanical play, and the difference between D and projection-center depth may exceed the predicted displacement.

## 5. Jacobian rank and conditioning

For three points, stack the three 2×6 point Jacobians to form a 6×6 image-motion Jacobian. Six scalar image residuals do not guarantee rank six.

Important cases include:

- Coincident or nearly coincident image points.
- Collinear or nearly collinear projected points.
- Points with weak spatial spread in the image.
- Points at similar depths when relying on lateral-translation parallax.
- Points near the principal point when relying on axial-translation expansion.
- Unknown focal length, principal point, distortion, or crop included as free variables.
- Mechanical pivots that couple nominal rig axes.
- Physical point movement, misidentification, occlusion, or marking noise.
- A constrained procedure in which tilt or other variables are locked.

Conditioning depends on the actual 3D coordinates, camera orientation, intrinsics, and units used to scale translations and rotations. Singular values of a sensibly normalized Jacobian are appropriate diagnostics. No universal “best triangle” follows from the six-observation count alone.

## 6. Verification of the staged A–B → C procedure

The proposed sequence has a defensible operational rationale:

1. Locking tilt and stabilizing optical state reduces the number of actively changing variables.
2. A/B supplies four visible residual components and useful midpoint, separation, and orientation summaries.
3. C supplies two additional residual components and can reveal depth-dependent disagreement.
4. Iterating A/B after C is necessary because controls are coupled.

The mathematical justification is conditional, not absolute. A/B does not isolate pan, height, or horizontal translation. A/B alignment can be reproduced by compensating changes in depth, focal state, rotation, or pivot position. C can help distinguish some alternatives, but it does not uniquely identify `zT` or any other control.

The staged method may have a practical advantage over simultaneous unconstrained adjustment by reducing the operator's active search space and making residuals easier to interpret. This is a hypothesis about usability and convergence, not a theorem. To establish an advantage, compare the staged procedure with a defined simultaneous or unguided baseline using time to convergence, adjustment count, final point residuals, off-triangle landmark residuals, operator variability, and failure rate.

The staged procedure can be expressed as progressively constrained adjustment, but “progressively constrained” must not be confused with mathematically optimal. Locking tilt removes or restricts a degree of freedom; stabilizing optics removes a changing nuisance variable; A/B-first and C-second select an observation order. None proves global convergence or superiority.

## 7. Tilt/reference-distance verification

The corrected draft now uses the following convention:

- If `θ` is measured from horizontal, vertical component `ΔH=D sin θ` and horizontal-forward component `ΔZ=D cos θ`.
- If `θ` is measured from vertical, `ΔH=D cos θ` and `ΔZ=D sin θ`.
- These formulas require `D` to be the slanted segment between the same endpoints in the same vertical plane.

The canonical TPS definition measures D from a sensor-plane mark to a designated physical reference plane. The clarified operator convention targets the estimated A–B midpoint. That measurement does not automatically establish a slanted hypotenuse or a camera-forward-axis distance. The right-triangle construction therefore remains conditional and must not be inserted into the canonical Working Focal Length equations without an additional geometric definition.

## 8. Corrections and recommendations

Applied to `TPS_CAMERA_LINEUP_GEOMETRY.md`:

- Corrected the angle-reference wording for the `sin`/`cos` component relationships.
- Preserved the explicit warning that the triangle requires matching endpoints, axes, and a slanted D measurement.

Recommended for later review, not applied to the canonical specification:

- Retain the Jacobian with its camera-center velocity convention adjacent to the equation.
- Keep `zT` as a rig-frame workflow notation and empirical heuristic.
- Treat depth-separated C as advantageous for selected diagnostics, not mandatory.
- Keep tilt locking, A/B-first ordering, focus-state stabilization, and troubleshooting as research-method or recommended-practice material.
- Add an authoritative image-based visual-servoing reference before publication if the Jacobian is retained as a literature-backed claim.

## 9. Verification status

| Item | Result | Status |
|---|---|---|
| Six-DOF image Jacobian | Matches independent derivation under declared convention | Verified mathematically |
| Translation signs | Correct for camera-center velocity convention | Verified conditionally |
| Rotation terms | Correct for stated camera-frame angular velocity convention | Verified conditionally |
| Numerical example | Recalculates to 240 px, 1200 px, approximately 77.32°, −6/−4 px, and +0.6/+0.4 px | Verified mathematically |
| Tilt/reference triangle wording | Original angle qualification required correction | Corrected in draft |
| A–B → C sequence | Plausible staged heuristic; no optimality proof | Needs experiment |
| `zT` as primary C adjustment | Workflow-specific observation only | Needs experiment |
| Full-rank local alignment | Configuration-dependent | Needs rank/conditioning analysis |
| Whole-image agreement | Not implied by three-point agreement | Requires experiment |

No canonical TPS document, application code, or approved Working Focal Length equation was modified.

==================================================
SOURCE: research/methods/TPS_PHYSICAL_LINEUP_PROCEDURE_REVIEW.md
==================================================
# TPS Physical Camera Lineup — Procedure Review

**Christopher Weinberg / LIMNMEDIA · October 2026**  
**Status:** Non-normative operational review; author confirmation required.  
**Sources reviewed:** `TPS_CAMERA_LINEUP_GEOMETRY.md` and `TPS_LINEUP_MATHEMATICAL_VERIFICATION.md`.

## Purpose and scope

TPS camera lineup is an iterative process of matching three recorded image correspondences by adjusting coupled camera parameters, using the residual errors to diagnose and refine the setup.

The physical triangle need not be similar to the image triangle. A-side means the reference recording; B-side means the attempted recovery. These are workflow conventions, not universal TPS requirements. The method is camera-view registration, not unique pose recovery.

## Measurement and initial conditions

### 1. Establish the reference

Identify stable, distinguishable physical points A, B, and C. Preserve their identities, locations, and measured relationships. Record the A-side image, actual dimensions, coordinate frame, and correspondence:

```text
A → a
B → b
C → c
```

A and B form the Base Pair for the approved Working Focal Length approximation when they are at approximately equal optical depth and aligned as closely as practical with camera-horizontal. This is a calculation assumption, not a general TPS correspondence requirement. C may be depth-separated to improve selected diagnostics, but depth separation is optional.

### 2. Measure the physical reference

Measure AB, BC, CA, and TPS Reference Distance D as accurately as practical. D is measured from a mark on the camera sensor plane to a practical reference location associated with A–B. Depending on the physical arrangement, the operator may target A, B, the midpoint of A–B, or an estimated midpoint when no precise midpoint mark is available.

A laser distance meter is one practical tool. It may be held alongside the camera near the sensor-plane mark, using the camera focal-plane mark when available. Survey-grade equipment is not required. Record the selected endpoints, measurement direction, tool, and any meaningful uncertainty.

D is a practical measurement convention. It is not automatically optical-center distance, perpendicular depth, or camera-forward-axis distance. In the ideal projection equations, a camera-depth quantity appears instead. The difference and uncertainty can influence the recovered projection.

### 3. Establish initial camera conditions

Restore the recorded tilt, Working Focal Length, focus/lens state, roll condition, and D relationship as closely as practical. These are initial estimates, not guarantees of optical equivalence.

Measure tilt and roll using the declared inclinometer procedure, including the instrument's orientation relative to the camera. Shared UP establishes a direction, not a common origin or complete camera pose. Do not treat the initial measurements as a solved camera configuration.

## Iterative A–B–C procedure

### Stage A — Establish initial conditions

**Operator observes:** Camera inclination, roll, lens/focus state, Working Focal Length, image frame, and approximate reference distance.

**Possible adjustment:** Restore the recorded configuration as closely as practical. Use D and the optical quantities as starting guides.

**Mathematics predicts:** Under ideal perspective projection, image position depends on camera pose, point depth, and imaging parameters. The approved Working Focal Length equations provide approximate reference quantities under their stated assumptions.

**Ambiguity:** D is not automatically projection-center depth. Nominal lens focal length or EXIF metadata may not represent the projection produced under the original focus, crop, active sensor, or distortion conditions.

**Information gained:** A baseline from which image residuals can be interpreted. Measurement uncertainty and optical mismatch remain possible.

### Stage B — Establish A–B alignment

**Operator observes:** Live a′ and b′ compared with recorded a and b in a consistently registered image frame. Examine individual residual vectors, pair midpoint, separation, and angular orientation.

**Possible adjustment:** Make a small change to whichever camera control appears appropriate, then observe the resulting displacement. Do not follow a mandatory Pan → Height → X sequence. Pan and horizontal translation may produce similar horizontal displacement; tilt and height may produce similar vertical displacement; and rig pivots can couple nominal controls.

**Mathematics predicts:** A and B provide four scalar image observations. The local image response can be approximated by `Δp ≈ JGΔs`, where `J` maps camera motion to image motion and `G` maps rig controls to camera motion. The verified Jacobian predicts qualitative displacement under declared conventions.

**Ambiguity:** No individual residual uniquely identifies pan, height, horizontal translation, focal change, depth, roll, or another cause. A/B agreement alone is not a complete camera solution.

**Information gained:** The operator learns how the actual rig's controls affect the registered image and whether the Base Pair can be brought toward its recorded projection without unexplained scale or registration error.

### Stage C — Introduce C

**Operator observes:** After A and B are usefully close, compare C with its recorded image point and evaluate the complete projected triangle. Continue to monitor A and B.

**Possible adjustment:** Consider roll, height, tilt, Z translation, scale, Working Focal Length, A-side measurements, nominal lens or EXIF values, and other setup differences. A small roll adjustment may improve alignment even when recorded roll was zero.

**Mathematics predicts:** C contributes two additional image observations. A depth-separated C may respond differently to selected translations, such as camera-local lateral translation. Camera-local axial translation changes image scale relative to the principal point and depends on depth.

**Ambiguity:** C does not uniquely diagnose any listed error. An improvement from roll does not prove the original camera had nonzero roll; it may compensate for another discrepancy. Rig `zT` is not automatically camera-local Z.

**Information gained:** C helps distinguish whether an apparently successful A–B alignment remains compatible with a third image observation and exposes discrepancies that the Base Pair cannot reveal by itself.

### Stage D — Refine

**Operator observes:** The effect of each small adjustment across all three residuals.

**Possible adjustment:** Adjust whichever parameter appears appropriate. A cautious test of declared rig Z translation (`zT`) may be useful when its predicted image effect is relevant. Return to A and B after each change.

**Mathematics predicts:** Camera controls are coupled. Improving C may disturb A–B. The local Jacobian describes sensitivity near the current configuration but does not prove global convergence, optimality, or a unique correction.

**Ambiguity:** A staged feedback process resembles constrained or block-coordinate optimization, but it is not proven to be faster, better conditioned, or superior to simultaneous adjustment.

**Information gained:** The operator accumulates a practical response model for the actual camera, rig, optics, and reference geometry.

### Stage E — Evaluate the recovered view

**Operator observes:** Whether all three correspondences agree within a practical, project-specific tolerance, followed by independent scene features outside the triangle.

**Possible adjustment:** Continue iterating or document remaining discrepancies. A recovery may be accepted for a particular shot without claiming universal TPS accuracy.

**Mathematics predicts:** Three-point agreement does not imply agreement at other depths, image regions, or frames. Lens distortion, wrong pose branches, set deformation, and changing optical conditions may remain visible.

**Ambiguity:** TPS does not provide a universal numerical tolerance or guarantee whole-image alignment.

**Information gained:** The result separates three-point projection agreement from broader practical view quality.

## Qualitative control relationships

| Controls or observation | Possible visual relationship | Limitation |
|---|---|---|
| Pan and horizontal X translation | Similar horizontal image displacement | Pivot and rig geometry determine the actual effect |
| Tilt and camera height | Similar vertical image displacement | Effects are coupled and configuration-dependent |
| Z translation and image scale | Camera depth can change projected scale | Focal/focus changes can mimic scale changes |
| Tilt, height, and Z translation | Can interact through camera geometry | No universal equivalence follows |
| Roll and other adjustments | Can affect apparent triangle angle | A compensating roll does not prove original roll |
| C residual after A–B alignment | Additional information about the current projection | Does not uniquely identify an error or control |

These relationships are qualitative. They guide observation and testing; they do not define one-to-one control mappings.

## Working Focal Length error interpretation

TPS distinguishes the Working Focal Length from manufacturer-reported focal length and EXIF metadata. A reported value may not represent the projection under the original conditions. Focus breathing, active sensor dimensions, crop or output mode, lens distortion, and measurement uncertainty can all contribute to a mismatch.

During lineup, an incorrect Working Focal Length or an incorrect input may appear as A–B separation error, a scale mismatch, or a disagreement that changes with depth. The operator may adjust a camera parameter to compensate, but that correction does not prove the parameter was the source of the error. The operator should also investigate focus state, sensor/crop registration, D, AB measurement, point identity, and nominal metadata before treating a visual improvement as a verified parameter correction.

The approved equations remain unchanged. They are approximate real-camera reference calculations, not substitutions for visual feedback or nominal metadata.

## Research status and boundaries

- Perspective projection and the image Jacobian are established mathematical models under declared assumptions.
- The TPS reference definitions and approved Working Focal Length equations remain canonical elsewhere.
- The iterative A–B–C lineup is proposed operator methodology.
- The diagnostic use of C is a research interpretation, not a unique error classifier.
- A depth-separated C is optional and is not a TPS requirement.
- Tilt locking, adjustment selection, practical tolerances, and whole-image evaluation are operational choices requiring characterization.
- The method is not proven to converge, optimal, or superior to simultaneous adjustment.

## Remaining author decisions

1. Exact D target and measurement direction for each physical arrangement.
2. Inclinometer zero, sign, and camera-surface conventions for tilt and roll.
3. Mapping between rig axes and camera-local axes.
4. Conditions under which roll is held, adjusted, or revisited.
5. Project-specific practical acceptance tolerances.
6. Experimental comparison between iterative visual feedback and simultaneous adjustment.

## Recommended research test

Use a fixed, surveyed A/B/C triangle and instrumented camera rig. Compare iterative visual feedback with a defined simultaneous or unguided baseline. Measure time to convergence, control changes, A/B/C residuals, off-triangle landmark residuals, operator variation, and failure cases. Repeat with C at varied depths, focus states, D measurement targets, pivot conditions, and optical configurations. Estimate `JG` from observed rig motions and compare predicted image motion with measured motion.

No result is claimed until these experiments are performed.

==================================================
SOURCE: entropy-buffer/PAPER_01_DRAFT_VIEW_CONTINUITY.md
==================================================
# The Three Point System: A Reference-Based Method for Camera-View Reproduction

**Christopher Weinberg**  
**LIMNMEDIA**

## 1. Abstract

The Three Point System (TPS) is an implementation-independent method for recording and reproducing a camera view. Its central principle is: “TPS connects three points in the physical world with where those same three points appear in an image.” A TPS reference identifies three physical points, records their corresponding image locations, preserves the physical relationships among the points, and retains information needed to interpret and register the image coordinates. It may also preserve a measured TPS Reference Distance, a Working Focal Length, and a derived horizontal angle of view.

TPS is deliberately narrower than camera calibration, photogrammetric resection, or visual-effects matchmoving. It does not attempt to solve for a unique camera position, orientation, or complete camera model. Instead, it gives an operator a portable visual reference and a small set of physical measurements with which to seek the closest practical reproduction of a previously recorded three-point view. The method can be implemented with a physical overlay, a monitor, photographic or film media, or software.

The geometric foundations of TPS are established principles of perspective projection and correspondence. The proposed operational combination is TPS-specific but is not claimed here as original: related practices exist in photogrammetry, rephotography, image registration, visual effects, fiducial registration, astronomy, and stop-motion production. The present paper is a first technical draft. It presents the method, equations, assumptions, related work, and a future validation plan without claiming experimental validation.

## 2. Introduction

Reproducing a camera view is a common practical problem. A camera may be moved, removed, replaced, or unavailable when a scene must be photographed again. The problem appears in independent filmmaking, visual effects, stop-motion, architectural documentation, rephotography, education, and other settings. Existing solutions range from careful physical measurements and motion-control systems to camera calibration, feature tracking, and full matchmoving pipelines. These approaches can be effective, but they may require specialized equipment, software, or technical expertise.

TPS addresses a more limited question: how can an operator record enough information about a view to seek that view again later using three identifiable physical reference points and their image locations? The intended answer is not a camera-solving algorithm. It is a reference-based method for view matching.

The TPS kernel states the relationship directly: “TPS connects three points in the physical world with where those same three points appear in an image.” The physical points are conventionally labeled A, B, and C. Their corresponding image points are a, b, and c. The identities are preserved as A→a, B→b, and C→c, even when the image coordinates change.

This distinction between identity and location is fundamental. A point can move in an image when the camera moves, rotates, changes focal length, or changes other imaging conditions. The image point remains associated with the same physical point. Conversely, three image locations alone do not reveal a unique three-dimensional camera configuration. Multiple physical and camera configurations can produce the same three-point projection under appropriate conditions.

TPS therefore has two layers. The first is geometric: physical points are projected into image space, and correspondence can be compared. The second is operational: a reference is recorded and later presented in registration with a live view so that a user can adjust the camera. The first layer rests on established mathematics. The practical effectiveness of the second layer requires experiments.

## 3. Related Work

### Photogrammetric resection and PnP

Photogrammetry provides a close mathematical precedent. In space resection, known control points and their image coordinates are used to determine the exterior orientation of a photograph or camera. Chow’s 1950 paper discusses three ground control points and their photograph coordinates as a basis for determining the position and orientation of a photograph [1]. Open educational photogrammetry material similarly describes the collinearity of the perspective center, object point, and image point, together with exterior-orientation parameters [2].

Perspective-n-point methods provide a modern computer-vision counterpart. OpenCV documents P3P as a pose problem using exactly three 3D–2D correspondences, with up to four possible solutions [3]. The same documentation describes PnP as estimating rotation and translation from object points, image projections, camera intrinsics, and distortion parameters. These methods establish that physical/image point correspondence is a standard input to camera pose estimation, and that three correspondences do not necessarily imply a unique pose.

TPS overlaps this geometry but has a different objective. Resection and PnP seek camera or object parameters. TPS does not require the operator to solve for a camera pose. It uses correspondence to compare a recorded view with a live view and to guide adjustment toward a practical match. Thus, TPS should not be described as a simplified PnP solver.

### Repeat photography

Repeat photography, or rephotography, seeks to make a new photograph from an earlier viewpoint, often to document landscape or cultural change. A review in *Heritage* describes locating the original camera position, producing a new image, and addressing the registration of old and new images [4]. This shares TPS’s operational goal more closely than camera resection does: the desired outcome is a comparable view rather than a complete camera model.

The difference is that rephotography commonly uses landmarks, historical records, maps, field judgment, or post-capture image registration. The reviewed literature does not establish the TPS record of three identified physical points, explicit A→a/B→b/C→c correspondence, physical triangle measurements, or TPS calculations. TPS can be understood as a constrained and formalized reference strategy within the larger problem of repeat photography.

### Image registration and homography

Image registration establishes a common coordinate relationship between images. OpenCV’s homography tutorial describes a planar projective transformation between planes [5]. In a full projective transformation, the transformation model has more degrees of freedom than three point pairs can determine. TPS therefore distinguishes registration from geometric correction. A known crop, rotation, scale, or coordinate transformation may be applied to make two records interpretable in the same frame. An arbitrary transformation chosen because it makes three nonmatching projections coincide would remove the difference TPS is meant to measure.

Astroalign is a particularly relevant interdisciplinary precedent. Beroiz, Cabral, and Sanchez describe matching three-point star asterisms to find transformations between astronomical images without relying on world-coordinate-system information [6]. This demonstrates an established three-point image-registration technique. It differs from TPS because its triangles are image features rather than identified physical scene points, and its output is an estimated image transformation rather than an operator-guided physical camera recovery.

Fiducial-marker registration in microscopy provides another related precedent. Mohammadian and colleagues describe visible markers and composed transformations for registering fluorescence and electron-microscopy images with different resolution and contrast [7]. The work supports the general value of stable correspondences, registered frames, and overlay comparison. It does not establish TPS’s camera-view objective or its physical triangle record.

### VFX camera surveying and lineup

Visual-effects matchmoving systems use tracked image features, survey data, camera and lens parameters, and optimization to reconstruct a virtual camera and scene relationship. 3DEqualizer documents manual and automatic camera lineup to surveyed geometry, survey points, distance constraints, focal-length controls, and lens parameters [8]. A related industry interview discusses the use of LIDAR, total-station data, reference frames, and lens-distortion models in production camera tracking [9].

These practices substantially overlap TPS’s use of physical measurements and image correspondences. They differ in scale and purpose. A VFX pipeline generally seeks a virtual camera, tracked scene, lens model, or renderable production solution. TPS seeks a portable reference for a human or application to reproduce a view and does not require the recovery of a unique virtual camera.

### Stop-motion overlays

Stop-motion workflows commonly compare a live camera view with a previous frame. The Australian Film Television & Radio School describes onion-skin transparency as a way to see a prior frame over the live image and align the next drawing [10]. Gasek describes frame-grabber onion skinning and ghosted frames for placement registration after a camera bump [11]. Dragonframe documentation similarly describes onionskin, Live View comparison, line-up layers, and difference display [12].

These are close operational precedents for registered visual comparison. They demonstrate that an overlay can guide an operator without requiring a camera solution. They do not, in the sources examined, define a reference consisting of three identified physical points together with physical triangle measurements, TPS Reference Distance, Working Focal Length, and AOV.

## 4. TPS Method

TPS begins by identifying three distinct, non-collinear physical points. A point is a specified location in three-dimensional Euclidean space; it need not be a separate physical object. A corner, mark, or identifiable feature may represent one. The points are labeled A, B, and C.

The camera observes the points and produces image points a, b, and c. Correspondence is explicit:

```text
A → a
B → b
C → c
```

The reference preserves both the identities and the image locations. The physical triangle and image triangle are related but are not assumed to be geometrically similar. Under perspective projection, physical side-length ratios and angles are not generally preserved in the image.

A TPS reference preserves at least the following information:

1. The three identified physical points A, B, and C.
2. Their image locations a, b, and c.
3. Explicit correspondence.
4. Measured physical triangle relationships, including AB and other relationships relevant to the operation.
5. The TPS Reference Distance, D.
6. The actual captured image width and height in pixels.
7. Active physical sensor dimensions when known and applicable to the captured imaging area.
8. Image coordinate-frame information sufficient to interpret and register the recorded points.
9. The Working Focal Length, its inputs, and the calculated horizontal AOV.

The image coordinate frame must state image dimensions, coordinate origin, axis directions, coordinate units, point positions, and relevant crop, rotation, or mirroring information when needed. No particular file format or software convention is required. The purpose is interpretability across implementations.

The TPS Reference Distance is measured from the camera sensor plane to the designated physical reference plane. It is not automatically equivalent to a lens focus-ring marking, a manufacturer-reported focus distance, or an ideal optical projection-center distance. The sensor-plane convention is practical and approximate.

## 5. Mathematical Foundations

Under an ideal perspective camera, a physical point with camera coordinates `(X,Y,Z)` projects to image-plane coordinates

```text
x = f X / Z
y = f Y / Z
```

where `f` is the model focal length. This mapping explains why image position depends on camera position, orientation, intrinsic parameters, and point depth. It also explains why the physical triangle need not resemble the image triangle.

If A, B, and C have different depths, each point is scaled by a different denominator. A single scale factor therefore does not generally relate all physical side lengths to all image side lengths. Similarity can occur in special cases, such as a triangle on a plane parallel to the image plane under an ideal model, or under an orthographic approximation. Similarity is not a universal TPS requirement.

Correspondence is a different concept from similarity. TPS preserves which image point belongs to which physical point. It does not claim that A, B, and C and a, b, and c have equal distances or angles. Three physical points can also produce a collinear or coincident image configuration under certain viewing geometries. Such a projection exists, although it may be unusable for a particular operation.

Registration also has a limited role. Two records may use different resolutions, crops, rotations, or coordinate conventions. A declared transformation can place them in a common frame. That transformation must be known or independently justified. It must not be selected solely to force a mismatch into agreement.

## 6. Working Focal Length and AOV

TPS records a Working Focal Length when establishing a reference. The approved calculations are:

```text
f_px = |xB - xA| * D / AB

AOV_h = 2 * atan(AB * W_image / (2 * D * |xB - xA|))

f_mm = f_px * W_sensor / W_image
```

Here, `xA` and `xB` are roll-corrected horizontal image coordinates; `AB` is the measured physical distance between A and B; `D` is the TPS Reference Distance; `W_image` is the actual captured image width in pixels; and `W_sensor` is the active physical sensor width in millimeters.

The first relationship is obtained from the ideal equal-depth, horizontal-segment relation `image separation = focal length × physical separation / depth`, with focal length expressed in pixel units. The second follows from the same geometry: the half-width of the image corresponds to half the horizontal field angle at the reference depth. Substituting `f_px = |xB-xA|D/AB` gives the equivalent form `AOV_h = 2 atan(W_image/(2 f_px))`. The third converts pixel focal length to millimeters using the active sensor width and captured image width.

These calculations require assumptions. A and B should be at approximately equal depth, and the physical A–B segment should be aligned as closely as practical with camera-horizontal. Roll correction accounts for image rotation; it does not correct physical A–B misalignment. Lens distortion, unequal depth, reference-plane tilt, crop ambiguity, resampling, finite-focus effects, and the sensor-plane distance convention can introduce error.

`f_px` and `AOV_h` do not require physical sensor dimensions. `f_mm` does. If active sensor dimensions are unavailable, the reference remains usable with the pixel calculation and AOV retained while the millimeter calculation is omitted. The AOV is derived from TPS geometry; it does not independently determine a missing sensor width. The Working Focal Length is a TPS measurement convention and is not necessarily identical to a manufacturer’s nominal focal length or a laboratory effective focal length.

The equations are mathematically consistent with the existing ideal derivation and are dimensionally consistent. They are not claimed to be universally exact optical identities, and their real-camera performance has not been experimentally validated.

## 7. Recording and Recovering a View

The recording operation establishes the reference. The operator identifies A, B, and C; identifies a, b, and c; records the coordinate frame and captured dimensions; measures the physical triangle; measures D; and preserves the calculation inputs and derived values. Physical sensor dimensions are recorded when known and must correspond to the active imaging area represented by the capture. The actual captured image dimensions, rather than a camera’s native sensor pixel resolution, are authoritative for that record.

Recovery compares the reference with the corresponding points in a live camera view. The reference points must be presented in registration with the live viewing frame. The operator adjusts the camera to obtain the closest practical match. TPS does not prescribe a universal numerical tolerance or require a pass/fail decision. It provides a reference against which practical adjustment can be judged.

The comparison representation may be physical or digital. A transparent reference can be placed over a television monitor showing the live view. A registered celluloid or film reference can be aligned with an optical or projected view. A digital overlay, such as a transparent PNG, can be composited over a live feed. These examples illustrate implementation independence; none is mandatory. The overlay is a representation of the reference, not the complete reference itself.

The recovery camera need not be identical to the original camera. A replacement camera may have different sensor dimensions, image resolution, lens behavior, or controls. Those differences make coordinate registration and practical matching more important, but they do not convert TPS into a calibration or pose-solving method.

## 8. Assumptions and Limitations

TPS assumes that point identities remain consistent within a correspondence set. The physical points must remain visible and maintain the intended geometric relationships for the operation. If a different triangle is used, its correspondence and geometric relationship to the reference must be established separately. Triangle similarity is one possible relationship, not a universal requirement.

Three-point matching is limited. A match of a, b, and c does not prove that the original camera position, orientation, focal length, or complete configuration has been recovered. It does not guarantee that other scene points project to the same locations or that the complete image matches. OpenCV’s P3P documentation provides a direct mathematical reminder: exactly three 3D–2D correspondences can yield up to four pose solutions [3].

The reference can also be geometrically degenerate. If projected points are coincident or collinear, the three-point record may not contain enough information for a particular operation. Point correspondence must not be inferred from proximity alone. A point that moves across the image remains associated with its original physical identity.

The Working Focal Length calculation has additional limitations. D is measured from the sensor plane rather than an ideal projection center. A and B may have unequal depth. The reference plane may be tilted. Lens distortion and focus breathing may affect the relation between image separation and focal length. The active sensor width may be unknown or may not correspond to the captured image area. These limitations mean that the recorded value is best treated as a reproducible TPS quantity under stated conditions, not as a universal optical truth.

Finally, practical matching involves measurement uncertainty and operator judgment. A visual match can be useful without being mathematically exact. Exact coordinate equality and practical agreement within a user- or operation-specific tolerance must remain distinct.

## 9. Discussion

TPS sits between two established traditions. One tradition solves geometry: photogrammetric resection, P3P/PnP, camera calibration, homography, and matchmoving estimate transformations, camera parameters, or scene structure. The other tradition guides practical alignment: repeat photography, stop-motion onion skin, reference overlays, and fiducial registration help an operator compare one view with another.

TPS uses information from both traditions but adopts neither objective completely. It borrows the precision of explicit point identity, physical measurement, and declared image coordinates. It borrows the accessibility of a registered visual comparison. It does not require a 3D reconstruction, a solved camera, a calibration pattern, a proprietary software package, or a particular recording medium.

This combination may be useful for independent animators, students, small productions, educators, and production environments where the desired result is a repeatable view rather than a complete camera asset. Its possible contribution is organizational and operational: define a small reference containing physical and image information, preserve it independently of technology, and use it to guide recovery.

That claim must remain restrained. The component ideas are established. Three-point camera geometry is established. Image registration is established. Physical survey data are established. Overlay comparison is established. Whether TPS’s particular combination provides a meaningful advantage over existing methods is an empirical question. Whether it is novel in the academic or patent sense requires a broader search than this first paper draft.

### View Continuity and Cinematic Space

TPS distinguishes reproduction of a camera view from reconstruction of a unique physical camera state. Camera position, orientation, reference measurements, and optical parameters remain important because they provide practical means of approaching a recorded view. They are instrumental to recovery, rather than the final criterion by which recovery is judged. The common reference is the projected image, whose formation from physical geometry is described by perspective-projection models [13].

Physical measurements constrain the recovery process; explicit A→a, B→b, and C→c correspondence establishes reference image positions; and registered comparison provides feedback for camera adjustment. This makes visual refinement a meaningful part of the method rather than an alternative to measurement. Nevertheless, agreement at three points does not establish agreement elsewhere in the image.

In cinematic production, visual coherence can also support the perception of a single represented or diegetic world. Film studies distinguishes that represented world from physical reality [14, 15], while practical compositing guidance emphasizes compatible perspective, scale, framing, and lighting when combining independently produced elements [16]. This provides context for TPS's view-oriented objective, but does not demonstrate that TPS alone can achieve whole-image coherence or diegetic continuity. Those outcomes depend on additional scene and imaging conditions and require validation.

## 10. Future Validation

The primary validation opportunity is a controlled recovery experiment. First, record a reference view containing three visible, non-collinear points. Record A, B, and C, their correspondence to a, b, and c, the image frame, the physical triangle measurements, D, and the available calculation inputs. Then move, remove, or replace the camera. Present the reference points in registration with the live view and adjust the camera toward the recorded projection.

The experiment should record the observed image locations during recovery and compare them with the reference locations. It should also examine scene points outside A, B, and C. The purpose is not to assume that three-point agreement reproduces the whole scene, but to measure how far the practical match extends beyond the defining points.

Further experiments should vary one condition at a time: camera translation, camera rotation, focal length, crop, image resolution, replacement camera, triangle relocation, triangle scale, A–B orientation, unequal point depth, reference-plane tilt, and overlay method. Repeatability should be studied by repeating the same operation under stated conditions. Reproducibility should be studied across operators, cameras, and recording methods.

The Working Focal Length convention requires separate validation against representative real lenses and distances. The experiment should compare the recorded TPS value with independently documented lens and camera measurements without assuming that the manufacturer’s nominal focal length is the correct reference. No numerical acceptance threshold is proposed here. The present paper claims no experimental result.

## 11. Conclusion

TPS is a reference-based method for camera-view reproduction. It connects three identified physical points with the locations where those points appear in an image. A TPS reference preserves correspondence, image coordinates, physical triangle measurements, coordinate-frame information, a measured TPS Reference Distance, and related Working Focal Length and AOV information when available.

The method is intentionally independent of software, hardware, operating system, file format, and recording medium. Recovery is performed by comparing a registered reference with a live view and adjusting toward the closest practical match. TPS does not claim unique camera reconstruction, complete scene alignment, or universal optical exactness.

The mathematical foundations and many operational components have clear precedents. Photogrammetric resection and P3P establish related physical/image geometry. Rephotography establishes the goal of returning to a prior view. Fiducial registration, astronomy, homography, VFX surveying, and stop-motion overlays establish related methods of correspondence, registration, and practical alignment. The possible contribution of TPS is the constrained, portable combination of these ideas for view matching without camera solving. That possibility remains to be tested and compared, not asserted as established originality.

## 12. References

[1] Carl Chow, “Photogrammetric Space Resection,” *Transactions of the American Society of Civil Engineers* 115(1), 1950, pp. 235–259. DOI: https://doi.org/10.1061/TACEAT.0006318.

[2] Open AGH, *Basics of Photogrammetry*, “Basics of Photogrammetry” module. https://epodreczniki.open.agh.edu.pl/handbook/4795/module/4812/reader.

[3] OpenCV, “Perspective-n-Point (PnP) pose computation,” version 4.10.0 documentation. https://docs.opencv.org/4.10.0/d5/d1f/calib3d_solvePnP.html.

[4] “Heritage and Repeat Photography: Techniques, Management, Applications, and Publications,” *Heritage* 5(4), 2022. https://doi.org/10.3390/heritage5040220.

[5] OpenCV, “Basic concepts of the homography explained with code.” https://docs.opencv.org/4.5.1/d9/dab/tutorial_homography.html.

[6] M. Beroiz, J. B. Cabral, and B. Sanchez, “Astroalign: A Python module for astronomical image registration,” *Astronomy and Computing* 32, 2020, article 100384. DOI: https://doi.org/10.1016/j.ascom.2020.100384.

[7] Sajjad Mohammadian et al., “High accuracy, fiducial marker-based image registration of correlative microscopy images,” *Scientific Reports* 9, 3211, 2019. DOI: https://doi.org/10.1038/s41598-019-40098-4.

[8] Science-D-Visions, *3DEqualizer Technical Specification*. https://www.3dequalizer.com/?item=tech_spec&site=start.

[9] Mike Seymour, “3DEqualizer – German precision where VFX needs it,” *fxguide*, 2014. https://www.fxguide.com/quicktakes/3dequalizer-german-precision-where-vfx-needs-it/.

[10] Australian Film Television & Radio School, *Stop Motion*, pp. 14–15. https://medialab.aftrs.edu.au/wp-content/uploads/2021/07/AFTRS16_StopMotion.2021.pdf.

[11] Tom Gasek, “Objects, People, and Places,” in *Frame-by-Frame Stop Motion: The Guide to Non-Puppet Photographic Animation*, Chapter 6, pp. 104–105. Publisher chapter PDF: https://www.bloomsburyvisualarts.com/app/downloadpdf?docIdS=b-9781315155166.

[12] DZED Systems, *Using Dragonframe 2025*. https://www.dragonframe.com/download/Using%20Dragonframe%202025.pdf.

[13] MIT, *Foundations of Computer Vision*, §5.3.1, “Image Formation by Perspective Projection.” https://visionbook.mit.edu/imaging.html.


[14] Columbia University, *Film Language Glossary*, “Diegesis.” https://filmglossary.ccnmtl.columbia.edu/term/diegesis/.

[15] Oklahoma State University Open Textbooks, *Introduction to Film & TV*, “Mise en scène.” https://open.library.okstate.edu/introfilmtv/part/mise-en-scene/.

[16] Adobe, “What makes amazing creative compositing.” https://www.adobe.com/learn/photoshop/web/photography-effects.
