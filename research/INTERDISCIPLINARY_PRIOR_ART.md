# Interdisciplinary TPS Prior Art

**Status:** Research review. This document does not modify the TPS specification or claim originality.

## Scope and evidence standard

This review asks which established methods help an operator reproduce a previously recorded view using physical references, image comparison, or physical-to-image correspondence. It spans rephotography, photogrammetry, surveying, registration, fiducials, astronomy, microscopy, projective geometry, animation, and VFX.

Evidence is classified as:

- **Verified:** Relevant source content was examined and supports the stated description.
- **Partially supported:** The source supports the general method, but not every comparison or TPS interpretation.
- **Identified:** A source was located but the relevant content was not fully examined.
- **Needs research:** The method or historical claim requires additional source review or experiment.

## Method comparisons

### Repeat photography / rephotography

- **Field:** Landscape research, cultural heritage, and visual anthropology.
- **Authoritative source:** “Heritage and Repeat Photography: Techniques, Management, Applications, and Publications,” *Heritage* 5(4), 2022. DOI and open article: https://doi.org/10.3390/heritage5040220
- **Date or period:** 2022 review of earlier practice.
- **Technical principle:** Locate an earlier camera position and produce a new image for comparison; registration may be performed after capture.
- **Operational objective:** Measure or communicate change between historical and current views.
- **Similarities to TPS:** Previously recorded view, camera-view reproduction, image comparison, registration, and practical field repositioning.
- **Differences from TPS:** Rephotography commonly relies on landmarks, site records, maps, or image registration; it does not establish the TPS three-point physical/image record or TPS calculations.
- **Evidence status:** Verified for the review's description of rephotography objectives and registration challenges. No claim is made about a universal rephotography protocol.

### Photogrammetric space resection

- **Field:** Photogrammetry and surveying.
- **Authoritative source:** Carl Chow, “Photogrammetric Space Resection,” *Transactions of the American Society of Civil Engineers* 115(1), 1950, pp. 235–259, DOI: https://doi.org/10.1061/TACEAT.0006318
- **Date or period:** 1950.
- **Technical principle:** Known object/control points and their image coordinates constrain the exterior orientation of a photograph or camera.
- **Operational objective:** Determine camera position and orientation from control-point observations.
- **Similarities to TPS:** Three physical points, three corresponding image points, relative physical quantities, and camera-view geometry.
- **Differences from TPS:** Space resection is explicitly a camera-reconstruction method. TPS uses correspondence to compare/reproduce a view and does not require solving the camera pose.
- **Evidence status:** Verified from the publisher abstract and bibliographic record. The source is a very close mathematical precedent for the physical-to-image relationship, but not a TPS workflow.

### Basic photogrammetric resection / collinearity

- **Field:** Photogrammetry education and geodesy.
- **Authoritative source:** Open AGH, *Basics of Photogrammetry*, “Basics of Photogrammetry” module: https://epodreczniki.open.agh.edu.pl/handbook/4795/module/4812/reader
- **Date or period:** Current open educational material; publication date not relied upon.
- **Technical principle:** The perspective center, object point, and image point are collinear; exterior orientation uses camera position and orientation parameters.
- **Operational objective:** Convert between image and object space and determine camera orientation.
- **Similarities to TPS:** Physical/image point correspondence and explicit camera/image coordinate relationships.
- **Differences from TPS:** The educational method is oriented toward photogrammetric measurement and camera orientation, not operator-guided view recovery without camera solving.
- **Evidence status:** Verified for collinearity and exterior-orientation concepts.

### Planar homography and projective registration

- **Field:** Computer vision and projective geometry.
- **Authoritative source:** OpenCV, “Basic concepts of the homography explained with code”: https://docs.opencv.org/4.5.1/d9/dab/tutorial_homography.html
- **Date or period:** OpenCV 3.0+ tutorial; access date not used as a publication claim.
- **Technical principle:** A planar projective transformation maps points between planes up to scale; corresponding points can estimate the transformation.
- **Operational objective:** Align or warp planar image content and support pose reasoning.
- **Similarities to TPS:** Image-coordinate registration and planar reference geometry.
- **Differences from TPS:** A full homography generally requires at least four point correspondences and transforms image data. TPS does not fit an arbitrary transformation to force three points to agree and does not define a planar warp as its operation.
- **Evidence status:** Verified for the stated homography principle. The distinction from TPS is an interpretation consistent with the repository's registration derivation.

### Astronomical triangle matching and registration

- **Field:** Astronomy and astronomical image processing.
- **Authoritative source:** M. Beroiz, J. B. Cabral, and B. Sanchez, “Astroalign: A Python module for astronomical image registration,” *Astronomy and Computing* 32, 2020, article 100384, DOI: https://doi.org/10.1016/j.ascom.2020.100384
- **Date or period:** 2020.
- **Technical principle:** Match three-point star asterisms to estimate a linear transformation between images without requiring world-coordinate-system information.
- **Operational objective:** Register stellar images for stacking, difference imaging, and mosaics.
- **Similarities to TPS:** Explicit three-point configurations, correspondence, image registration, and comparison without a full camera model.
- **Differences from TPS:** Astroalign uses triangles as image features and estimates a transformation automatically; TPS identifies physical points and uses the recorded image locations to guide view recovery. Astroalign does not preserve TPS physical triangle measurements, D, Working Focal Length, or AOV.
- **Evidence status:** Verified from the article abstract and bibliographic record. This is one of the closest non-film precedents for three-point image registration, but it is not a physical-camera recovery method.

### Fiducial-marker registration in microscopy

- **Field:** Correlative microscopy and industrial-style multimodal registration.
- **Authoritative source:** Sajjad Mohammadian et al., “High accuracy, fiducial marker-based image registration of correlative microscopy images,” *Scientific Reports* 9, 3211, 2019, DOI: https://doi.org/10.1038/s41598-019-40098-4
- **Date or period:** 2019.
- **Technical principle:** Fiducial markers visible across modalities establish transformations between images with different resolution and contrast; multiple transformations can be composed.
- **Operational objective:** Register fluorescence and electron microscopy images accurately.
- **Similarities to TPS:** Physical or visible reference markers, correspondence, registered image frames, overlay comparison, and portable coordinate relationships.
- **Differences from TPS:** The method is multimodal microscopy registration and seeks accurate transformation estimation, not camera-view reproduction by an operator. It also uses marker systems and image transformations beyond TPS's minimal conceptual scope.
- **Evidence status:** Verified from the open article abstract and full text.

### Astronomy image registration with reference sources

- **Field:** Astrometry.
- **Authoritative source:** F. Masci et al., “Image registration and astrometric calibration for the Spitzer Space Telescope,” *Publications of the Astronomical Society of the Pacific* 116, 2004; open PDF: https://web.ipac.caltech.edu/staff/fmasci/home/sirtfwork/paper7R.pdf
- **Date or period:** 2004.
- **Technical principle:** Match common point sources, estimate offsets or transformations, and place images in a common reference frame.
- **Operational objective:** Combine images and measure motions or positions consistently.
- **Similarities to TPS:** Reference points, common coordinate frames, image registration, and uncertainty-aware comparison.
- **Differences from TPS:** The objective is astrometric measurement and image combination, not physical-camera repositioning or view recovery.
- **Evidence status:** Identified and source record located; the PDF was not fully examined in this pass. Specific claims remain unverified.

### Optical surveying and instrument resection

- **Field:** Land surveying and geodetic instrument setup.
- **Authoritative source:** The reviewed photogrammetric resection literature and surveying references treat resection as determining an unknown station from known control points and observed directions or image relationships.
- **Date or period:** Historical and continuing surveying practice.
- **Technical principle:** Known control points constrain an observer or instrument station.
- **Operational objective:** Establish instrument location and orientation relative to control.
- **Similarities to TPS:** Three-point reference geometry and repeatable aiming/alignment.
- **Differences from TPS:** Survey resection solves the observer's position/orientation. It is therefore a close physical precedent but not evidence that TPS's non-solving objective is novel.
- **Evidence status:** Partially supported by the examined resection sources; a dedicated instrument-manual review remains needed.

### Traditional animation and registration pins

- **Field:** Hand-drawn and cel animation, film registration.
- **Authoritative source:** Registration-pin historical record located in the reviewed search; authoritative archival manual not examined in this pass.
- **Date or period:** Historical film and animation practice.
- **Technical principle:** Physical pins or peg bars hold successive image media in a repeatable spatial relationship.
- **Operational objective:** Preserve frame-to-frame registration during drawing, exposure, copying, or compositing.
- **Similarities to TPS:** Physical registration, overlays, and repeatable image-frame alignment.
- **Differences from TPS:** Registration pins stabilize media rather than reproduce a camera view from three physical scene points.
- **Evidence status:** Identified; needs authoritative historical-manual verification.

## Cross-domain answers

### A. Methods sharing TPS's operational objective

Repeat photography and some stop-motion or optical-overlay practices most closely share the operator objective of returning to a previously recorded view through visual comparison. Photogrammetric resection shares the geometric information but changes the objective to camera reconstruction.

### B. Shared measurements

Photogrammetry and VFX surveying preserve physical control-point coordinates, image coordinates, camera orientation, focal length, and sometimes lens or distance data. These overlap TPS's physical triangle measurements, correspondence, image frame, TPS Reference Distance, and Working Focal Length inputs. The sources do not establish TPS's exact combination or its sensor-plane convention.

### C. Reconstruction requirements

Space resection, P3P/PnP, VFX matchmoving, and surveying resection generally reconstruct or estimate camera/instrument pose. Repeat photography and overlay-guided animation can operate through visual alignment without explicitly solving pose. TPS belongs operationally closer to the latter while using measurements associated with the former.

### D. Portable reference data

Photogrammetric control-point records, fiducial-marker coordinate systems, astronomical reference frames, and VFX survey packages all demonstrate the value of preserving identifiers, coordinates, units, and frame conventions. This supports the general importance of portable reference data but does not prescribe a TPS file format.

### E. Potentially equivalent methods

No examined source documents a method that is clearly equivalent to the complete TPS workflow: three identified physical points; three corresponding image locations; a registered reference; preserved physical triangle measurements; TPS Reference Distance; Working Focal Length and AOV; and operator-guided recovery without camera reconstruction. Astroalign is equivalent to a three-point image-registration subproblem, and photogrammetric space resection is equivalent to the physical/image geometry but has the opposite operational objective. These are substantial precedents, not complete duplicates.

### F. Mathematical limitations to acknowledge

- Three physical/image correspondences can support camera-pose calculations, but pose may be non-unique under perspective models.
- Three image points do not generally determine a full planar projective transformation; arbitrary registration can create false agreement.
- Perspective projection does not generally preserve physical triangle shape.
- Unequal point depths, reference-plane tilt, lens distortion, crop, scaling, and differing image frames affect comparison.
- Fiducial or feature correspondence must preserve identity; proximity is not sufficient.
- Rephotography and visual overlays demonstrate practical alignment, not proof of recovered camera pose.

## Research conclusion

The interdisciplinary record shows that TPS is assembled from well-established elements: rephotography, physical control points, projective geometry, fiducial registration, overlays, and camera surveying. The potentially distinct contribution is their deliberately minimal combination for practical camera-view reproduction without requiring camera reconstruction, together with a portable reference record. That contribution remains a hypothesis requiring broader prior-art search, especially historical manuals and patents, and experimental comparison against existing workflows.

