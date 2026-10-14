# TPS Camera Report

**Report state:** PUBLISHABLE

## Reference

- Reference ID: `tps-9f587b561c307313`
- Name: tps_001_02_X1_0001

This report records the TPS reference package. It does not claim that physical Stage Line-Up has occurred.

## Camera / Sensor

| Parameter | Value | Provenance |
|---|---|---|
| Camera make | — | — |
| Active sensor width | 22.300000 | found:manufacturer_sensor_catalog:https://www.canon-europe.com/cameras/eos-r100/specifications/ |
| Active sensor height | 14.900000 | found:manufacturer_sensor_catalog:https://www.canon-europe.com/cameras/eos-r100/specifications/ |
| Active area state | assumedFullSensor | found:manufacturer_sensor_catalog:https://www.canon-europe.com/cameras/eos-r100/specifications/ |
- Full sensor: 22.3 mm × 14.9 mm
- Normalized raster: 6000 × 4000 px

## Lens / Optics

| Parameter | Value | Provenance |
|---|---|---|
| Source / on-set focal length | — | — |
| TPS calculated working focal length | 39.680971 | calculated:limnlens |
| 36-mm-width normalized horizontal working focal length | — | — |
| TPS calculated EFL | — | — |
| TPS Focus Distance | 304.400000 | entered:tps_workflow |
- Metadata SubjectDistance: — mm (supporting metadata only)

## Sacred Triangle

Image points are in normalized image pixel space. Physical side lengths are entered authority; physical angles are calculated from those sides.

| Parameter | Value | Provenance |
|---|---|---|
| Base Pair | 74 | entered:tps_workflow |
| Left Side | 87.500000 | entered:tps_workflow |
| Right Side | 79 | entered:tps_workflow |
| Left Interior Angle | 57.849646 | calculated:tps_geometry |
| Right Interior Angle | 69.677122 | calculated:tps_geometry |
| Top Interior Angle | 52.473232 | calculated:tps_geometry |

## Camera Orientation

| Tilt | 4.600000 | entered:tps_workflow |
| Roll / Dutch | 0.700000 | entered:tps_workflow |

## Projection / Scale

| Reference mm per pixel | 0.028508 | calculated:reference_plane_scale |
| Reference pixels per mm | 35.077813 | calculated:reference_plane_scale |
| Effective sensor mm per pixel X | 0.003717 | calculated:limnlens |
| Effective sensor mm per pixel Y | 0.003725 | calculated:limnlens |

## Source Metadata

- Metadata focal length: — mm
- Metadata equivalent focal length: — mm
- Metadata SubjectDistance: — mm
- Capture timestamp: —

## Assumptions and Warnings

- Focus convention: sensorPlaneToReferencePlane
- Active area state: assumedFullSensor
- Calculation method: physicalSensor
- Calculation version: tps-horizontal-focal-v1
- Base Pair image diagnostics: dx=2595.4684463279254 px, dy=-38.78060955613137 px, length=2595.7581535192066 px, angle=-0.8560304118351723 deg
- Normalized-solve limitations:
- Physical Stage Line-Up remains external to LIMNTPS.

## TPS / Package Provenance

- Format: `tps-reference-v0.1`
- Focal solve: `tps-horizontal-focal-v1`
- Authoritative revision: 2165

## VES Fields and TPS Extensions

| Field | Value | Provenance | Layer |
|---|---|---|---|
| CRIF Version | 1.1 | system:ves_crif_export | VES standard |
| SlatesUUID | tps-9f587b561c307313 |  | VES standard |
| Slate | tps_001_02_X1_0001 |  | VES standard |
| Camera Letter | — |  | VES standard |
| Shoot Timestamp | — |  | VES standard |
| Camera Body | — |  | VES standard |
| Tk Take | — |  | VES standard |
| Tk Focal Length | — |  | VES standard |
| Tk Focal Length End | — |  | VES standard |
| Tk Lens Focus | — |  | VES standard |
| Tk Lens Focus End | — |  | VES standard |
| Tk Lens ID | — |  | VES standard |
| Tk Lens Serial Num | — |  | VES standard |
| Tk Stop | — |  | VES standard |
| Tk Camera Tilt | 4.600000 | entered:tps_workflow | VES standard |
| Tk Camera Tilt End | — |  | VES standard |
| Tk Camera Dutch | 0.700000 | entered:tps_workflow | VES standard |
| Tk Camera Dutch End | — |  | VES standard |
| Tk Notes | TPS reference; physical Stage Line-Up is external. | system:tps_report_export | VES standard |
| Tk TPS Calculated Focal Length | 39.680971 | calculated:limnlens | TPS extension |
| Tk TPS Normalized Horizontal Working Focal Length | — |  | TPS extension |
| Tk TPS Calculation Method | physicalSensor |  | TPS extension |
| Tk TPS Calculation Version | tps-horizontal-focal-v1 |  | TPS extension |
| Tk TPS Raster Width Px | 6000 |  | TPS extension |
| Tk TPS Raster Height Px | 4000 |  | TPS extension |
| Tk TPS Base Pair Dx Px | 2595.468446 |  | TPS extension |
| Tk TPS Base Pair Dy Px | -38.780610 |  | TPS extension |
| Tk TPS Base Pair Pixel Length | 2595.758154 |  | TPS extension |
| Tk TPS Base Pair Image Angle Deg | -0.856030 |  | TPS extension |
| Tk TPS Normalized Solve Warnings | — |  | TPS extension |
| Tk TPS Calculated EFL | — |  | TPS extension |
| Tk TPS Base Left X | 1411.017746 | entered:point_placement | TPS extension |
| Tk TPS Base Left Y | 3511.054207 | entered:point_placement | TPS extension |
| Tk TPS Base Right X | 4006.486192 | entered:point_placement | TPS extension |
| Tk TPS Base Right Y | 3472.273597 | entered:point_placement | TPS extension |
| Tk TPS Top X | 2924.207151 | entered:point_placement | TPS extension |
| Tk TPS Top Y | 3238.670551 | entered:point_placement | TPS extension |
| Tk TPS Base Pair Length | 74 | entered:tps_workflow | TPS extension |
| Tk TPS Left Side Length | 87.500000 | entered:tps_workflow | TPS extension |
| Tk TPS Right Side Length | 79 | entered:tps_workflow | TPS extension |
| Tk TPS Left Interior Angle | 57.849646 | calculated:tps_geometry | TPS extension |
| Tk TPS Right Interior Angle | 69.677122 | calculated:tps_geometry | TPS extension |
| Tk TPS Top Interior Angle | 52.473232 | calculated:tps_geometry | TPS extension |
| Tk TPS Active Sensor Width | 22.300000 | found:manufacturer_sensor_catalog:https://www.canon-europe.com/cameras/eos-r100/specifications/ | TPS extension |
| Tk TPS Active Sensor Height | 14.900000 | found:manufacturer_sensor_catalog:https://www.canon-europe.com/cameras/eos-r100/specifications/ | TPS extension |
| Tk TPS Active Area State | assumedFullSensor | found:manufacturer_sensor_catalog:https://www.canon-europe.com/cameras/eos-r100/specifications/ | TPS extension |
| Tk TPS Effective Sensor Mm Per Pixel X | 0.003717 | calculated:limnlens | TPS extension |
| Tk TPS Effective Sensor Mm Per Pixel Y | 0.003725 | calculated:limnlens | TPS extension |
| Tk TPS Reference Mm Per Pixel | 0.028508 | calculated:reference_plane_scale | TPS extension |
| Tk TPS Reference Pixels Per Mm | 35.077813 | calculated:reference_plane_scale | TPS extension |
| Tk TPS Base Pair Sensor Length | 9.646491 | calculated:limnlens | TPS extension |
| Tk TPS Focus Distance | 304.400000 | entered:tps_workflow | TPS extension |
| Tk TPS Focus Distance Geometry | sensorPlaneToReferencePlane | system:tps_optical_assumptions | TPS extension |
| Tk TPS Focal Solve Version | tps-horizontal-focal-v1 | system:tps_optical_assumptions | TPS extension |
| Tk TPS Source Focal Provenance | — |  | TPS extension |
| Tk TPS Calculated Focal Provenance | calculated:limnlens | calculated:limnlens | TPS extension |
