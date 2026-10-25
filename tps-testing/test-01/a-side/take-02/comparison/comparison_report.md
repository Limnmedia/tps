# Test-01 Take-02 Comparison

## Inputs

- A-side: `../tps_001_02_X1_0001.jpg`
- B-side: `../tps_001_02_X1_0002.jpg`
- Both source images: 6000 x 4000 pixels

## Generated artifacts

- `comparison.png` presents the auto-levelled grayscale A-side, B-side, and
  difference image side by side.
- `difference-gray.png` is the full-resolution grayscale difference image.
- `a-side-gray.png` and `b-side-gray.png` are the auto-levelled grayscale
  intermediates used to generate the comparison.

The comparison was generated with ImageMagick from the two take-02 JPEGs.
Grayscale conversion and independent auto-level normalization make scene
structure easier to inspect despite lighting and exposure differences. No
camera solve, marker-constrained registration, lens calibration, or calibrated
pixel-residual measurement was performed.

## Interpretation

The comparison is provided as visual evidence for the reported overlay-guided
recovery. It does not establish quantitative TPS accuracy. Differences may
include lighting, exposure, shadows, surface texture, and operator alignment.
The exact operator movement sequence and individual adjustments were not
recorded.

## Provenance and privacy

The images were captured by Christopher Weinberg, who approved public
redistribution. The public evidence set excludes the raw CR3 files because
they contain camera serial-number metadata.
