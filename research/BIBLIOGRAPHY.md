# TPS Research Bibliography

This bibliography records sources relevant to TPS research. It distinguishes bibliographic identification from review of relevant source content.

Verification status:

- **Identified:** A bibliographic record was located.
- **Examined:** Relevant source content was reviewed.
- **Verified:** A specific claim was checked against the reviewed source content.

## Perspective Projection and Camera Geometry

### OpenCV — *Perspective-n-Point (PnP) pose computation*, version 4.10.0

- **Author or organization:** OpenCV
- **Publication year:** Documentation generated 2024; version 4.10.0
- **Publisher or institution:** Open Source Computer Vision
- **Stable URL:** https://docs.opencv.org/4.10.0/d5/d1f/calib3d_solvePnP.html
- **Access status:** Open
- **Relevant subject:** P3P, PnP, 3D–2D correspondences, reprojection error, camera pose, and multiple solutions
- **Verification status:** Examined; directly relevant. The documentation states that `solveP3P()` uses exactly three correspondences and may return up to four solutions. It is pose-estimation prior art, not TPS.

### OpenCV — *Perspective-n-Point (PnP) pose computation*

- **Author or organization:** OpenCV
- **Publication year:** Documentation version 4.8.0; page accessed during this review
- **Publisher or institution:** Open Source Computer Vision
- **Stable URL:** https://docs.opencv.org/4.8.0/d5/d1f/calib3d_solvePnP.html
- **Access status:** Open
- **Relevant subject:** 3D object points, corresponding 2D image projections, camera intrinsics, distortion, pose, and reprojection error
- **Verification status:** Examined; directly relevant to the correspondence and camera-pose prior art; not a TPS specification

### OpenCV — *Camera Calibration*

- **Author or organization:** OpenCV
- **Publication year:** Documentation version 4.11.0; page accessed during this review
- **Publisher or institution:** Open Source Computer Vision
- **Stable URL:** https://docs.opencv.org/4.11.0/dc/dbb/tutorial_py_calibration.html
- **Access status:** Open
- **Relevant subject:** Object points, image points, calibration patterns, intrinsic and extrinsic parameters, distortion, and image-size-dependent calibration
- **Verification status:** Examined; directly relevant to calibration prior art; not a TPS requirement

### Hartley and Zisserman — *Multiple View Geometry in Computer Vision*

- **Author:** Richard Hartley and Andrew Zisserman
- **Publication year:** 2000; second edition 2004
- **Publisher or institution:** Cambridge University Press; author-hosted Visual Geometry Group, University of Oxford
- **Stable URL:** https://robots.ox.ac.uk/~vgg/hzbook/hzbook1.html
- **Access status:** Open access to bibliographic page and selected chapters; book access varies
- **Relevant subject:** Projective geometry, camera projection, image correspondence, and multiple-view geometry
- **Verification status:** Examined; not used here as sole verification of a specific TPS claim

### MIT — *Foundations of Computer Vision, Chapter 5: Imaging*

- **Author or organization:** Massachusetts Institute of Technology
- **Publication year:** Not stated on the reviewed page
- **Publisher or institution:** MIT
- **Stable URL:** https://visionbook.mit.edu/imaging.html
- **Access status:** Open
- **Relevant subject:** Pinhole and perspective projection, 3D-to-2D mapping, image coordinates, depth, and focal length
- **Verification status:** Examined and verified for the general perspective-projection, depth, and image-coordinate claims cited in the evidence map; not verification of TPS-specific behavior

## Triangle Geometry and Similarity

### OpenStax — *Contemporary Mathematics, Section 10.3: Triangles*

- **Author or organization:** OpenStax
- **Publication year:** 2021 edition page; exact publication year not relied on here
- **Publisher or institution:** OpenStax, Rice University
- **Stable URL:** https://openstax.org/books/contemporary-mathematics/pages/10-3-triangles
- **Access status:** Open
- **Relevant subject:** Noncollinear points forming a triangle and triangle similarity by corresponding proportions
- **Verification status:** Examined and verified for the basic triangle-formation and similarity statements cited in the evidence map; not verification of TPS-specific triangle requirements

## Camera Optics and Focal Length

### Edmund Optics — *Understanding Focal Length and Field of View*

- **Author or organization:** Edmund Optics
- **Publication year:** Not stated on the reviewed page
- **Publisher or institution:** Edmund Optics technical resource
- **Stable URL:** https://www.edmundoptics.com/knowledge-center/application-notes/imaging/understanding-focal-length-and-field-of-view
- **Access status:** Open
- **Relevant subject:** Focal length, field of view, working distance, sensor size, and practical optical limitations
- **Verification status:** Examined and verified for the general focal-length and field-of-view relationship; not verification of the TPS Working Focal Length, which remains TPS-specific

## Image Coordinate Registration

### Brown — *A Survey of Image Registration Techniques*

- **Author:** Lisa Gottesfeld Brown
- **Publication year:** 1992
- **Publisher or institution:** ACM Computing Surveys, 24(4), 325–376; Columbia University affiliation listed in the record
- **DOI:** https://doi.org/10.1145/146370.146374
- **Access status:** Unknown / access to the full article was not confirmed
- **Relevant subject:** Registration of images acquired at different times, viewpoints, and sensors
- **Verification status:** Identified from the bibliographic record; full relevant content was not accessible and no claim is verified from it

## Visual Effects and Camera Matching

### Radke — *Computer Vision for Visual Effects*

- **Author:** Richard J. Radke
- **Publication year:** 2012
- **Publisher or institution:** Cambridge University Press
- **Stable URL:** https://www.cambridge.org/core/product/identifier/CBO9781139019682A034/type/BOOK_PART
- **Access status:** Open chapter record and summary; full book access varies
- **Relevant subject:** Feature matching, correspondence, tracking, and matchmoving for visual effects
- **Verification status:** Examined at the publisher chapter record; directly relevant for scope comparison, but not a verified source for a three-point TPS method

## Stop-Motion and Overlay Practice

### Dragonframe — *Using Dragonframe 2025*

- **Author or organization:** DZED Systems / Dragonframe
- **Publication year:** 2025 manual
- **Publisher or institution:** Dragonframe
- **Stable URL:** https://www.dragonframe.com/download/Using%20Dragonframe%202025.pdf
- **Access status:** Restricted by large-PDF retrieval during this review; indexed manual text was accessible
- **Relevant subject:** Onionskin transparency, Live View comparison, difference mode, and frame echo
- **Verification status:** Examined in indexed manual excerpts; directly relevant to overlay practice. Full manual review was not completed, so no broader claim is made.

### Dragonframe — *Camera Support*

- **Author or organization:** DZED Systems / Dragonframe
- **Publication year:** Current support page accessed during this review
- **Publisher or institution:** Dragonframe
- **Stable URL:** https://www.dragonframe.com/camera-support/
- **Access status:** Open
- **Relevant subject:** Low-resolution video assist, high-quality capture, tandem image sequences, and camera-specific live-view dimensions
- **Verification status:** Examined; directly relevant to coordinate-frame and resolution distinctions. It does not define TPS.

## Computer Vision Textbooks

### Szeliski — *Computer Vision: Algorithms and Applications*, Second Edition

- **Author:** Richard Szeliski
- **Publication year:** 2022
- **Publisher or institution:** Springer; author-hosted book site
- **Stable URL:** https://szeliski.org/Book/
- **Access status:** Open bibliographic page; electronic text available through the author's download process
- **Relevant subject:** Computer vision, camera geometry, image matching, and registration
- **Verification status:** Examined at the official book page; specific relevant chapters were not examined in this pass and are not used as verified evidence.

## VFX Camera Lineup and Survey

### Science-D-Visions — *3DEqualizer Technical Specification*

- **Author or organization:** Science-D-Visions
- **Publication year:** Not stated on the reviewed page
- **Publisher or institution:** Science-D-Visions
- **Stable URL:** https://www.3dequalizer.com/?item=tech_spec&site=start
- **Access status:** Open
- **Relevant subject:** Lineup Controls, survey points, distance and plane constraints, camera/lens parameters, manual and automatic camera consistency, and focal-length calculation
- **Verification status:** Examined; directly relevant to TPS prior art. It documents a broader software camera-lineup and matchmoving system, not the TPS specification.

### Mike Seymour — “3DEqualizer – German precision where VFX needs it”

- **Author:** Mike Seymour; interview with Rolf Schneider
- **Publication year:** 2014
- **Publisher or institution:** fxguide
- **Stable URL:** https://www.fxguide.com/quicktakes/3dequalizer-german-precision-where-vfx-needs-it/
- **Access status:** Open
- **Relevant subject:** Survey data, camera tracking, low-parallax shots, lens distortion, scale, and production camera matching
- **Verification status:** Examined; directly relevant for comparison with VFX survey and camera-tracking practice. It does not establish TPS.

### Australian Film Television & Radio School — *Stop Motion*

- **Author or organization:** Australian Film Television & Radio School
- **Publication year:** 2021 document version shown in the URL; exact publication date not relied on here
- **Publisher or institution:** AFTRS Media Lab
- **Stable URL:** https://medialab.aftrs.edu.au/wp-content/uploads/2021/07/AFTRS16_StopMotion.2021.pdf
- **Access status:** Open
- **Relevant subject:** Onion-skin overlays and aligning successive stop-motion frames
- **Verification status:** Examined, pp. 14–15; directly relevant to overlay practice, not camera-view recovery by three physical points

### Gasek — “Objects, People, and Places”

- **Author:** Tom Gasek
- **Publication year:** 2015
- **Publisher or institution:** Bloomsbury Visual Arts, in *Frame-by-Frame Stop Motion: The Guide to Non-Puppet Photographic Animation*
- **Stable URL:** https://www.bloomsburyvisualarts.com/app/downloadpdf?docIdS=b-9781315155166
- **Access status:** Restricted / chapter PDF accessible through publisher delivery during review
- **Relevant subject:** Camera stability, frame-grabber onion skinning, camera-bump recovery, and placement registration
- **Verification status:** Examined, Chapter 6, pp. 104–105; directly relevant to practical overlay-guided recovery, not a three-point TPS method

## Measurement Uncertainty and Repeatability

### Taylor and Kuyatt — *Guidelines for Evaluating and Expressing the Uncertainty of NIST Measurement Results*, NIST Technical Note 1297

- **Authors:** Barry N. Taylor and Chris E. Kuyatt
- **Publication year:** 1994
- **Publisher or institution:** National Institute of Standards and Technology
- **Stable URL:** https://www.nist.gov/pml/nist-technical-note-1297
- **Access status:** Open
- **Relevant subject:** Measurement uncertainty, repeatability, reproducibility, uncertainty components, and reporting
- **Verification status:** Examined and verified for the repeatability and reproducibility terminology cited in the evidence map

### JCGM — *Evaluation of Measurement Data — Guide to the Expression of Uncertainty in Measurement (JCGM 100:2008)*

- **Author or organization:** Joint Committee for Guides in Metrology
- **Publication year:** 2008
- **Publisher or institution:** JCGM / BIPM and member organizations
- **DOI:** https://doi.org/10.59161/JCGM100-2008E
- **Stable URL:** https://www.bipm.org/documents/20126/2071204/JCGM_100_2008_E.pdf
- **Access status:** Open for online access; copyright restrictions apply
- **Relevant subject:** Evaluation and expression of measurement uncertainty
- **Verification status:** Examined at the official bibliographic and access page; no TPS-specific claim is marked verified from this source in this draft
