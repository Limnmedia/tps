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
