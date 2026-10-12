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
