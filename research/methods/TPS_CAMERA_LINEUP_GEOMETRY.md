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

`x_A,x_B` are the horizontal image coordinates used in the calculation; `W_image` is **captured image width**, not necessarily native sensor pixel width; `W_sensor` is active physical sensor width for that captured mode. The millimeter conversion is omitted when active sensor width is unknown. `D` is the practical sensor-plane reference measurement. Recorded camera tilt and roll are recovery measurements, not inputs to these equations. These equations assume approximately equal A/B optical depth and horizontal AB alignment, plus the approximation `D≈Z` from projection center to the reference. They do **not** apply unconditionally to arbitrary A/B orientation or triangle geometry. `f_px` is a *Working* Focal Length, not necessarily the laboratory focal length.

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
