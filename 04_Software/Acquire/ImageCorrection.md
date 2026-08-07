# Image Correction

> iDetector Acquire Module - Image Correction

---

# 1. Purpose

The **Image Correction** function controls the correction algorithms applied to acquired images.

It allows engineers to enable or disable different correction items before image acquisition, ensuring that the displayed and saved images meet the expected image quality requirements.

The correction functions are configured in the **Correct Menu** of the Acquire page.

---

# 2. Scope

This document describes all correction options available in the **Correct Menu**.

According to the iDetector User Manual, the correction menu contains three categories:

- Offset
- Gain
- Defect

Each category provides software correction and/or hardware correction options depending on the detector model. :contentReference[oaicite:1]{index=1}

---

# 3. Correction Overview

| Category | Available Options |
|----------|-------------------|
| Offset | SWPreOffset, HWPreOffset, SWPostOffset, HWPostOffset* |
| Gain | SWGain, HWGain |
| Defect | SWDefect, HWDefect* |

> *Availability depends on detector model. HWPostOffset is currently supported only by Mars series detectors. HWDefect is currently supported by Mars series and Mercu detectors. :contentReference[oaicite:2]{index=2}

---

# 4. Offset Correction

Offset correction compensates for detector offset signals before or after image acquisition.

Available options:

| Option | Description |
|--------|-------------|
| SWPreOffset | Enable software PreOffset correction |
| HWPreOffset | Enable hardware PreOffset correction |
| SWPostOffset | Enable software PostOffset correction |
| HWPostOffset | Enable hardware PostOffset correction (Mars series only) |

These options correspond to the Correct Menu definitions in the iDetector User Manual. :contentReference[oaicite:3]{index=3}

---

# 5. Gain Correction

Gain correction compensates for detector response non-uniformity.

Available options:

| Option | Description |
|--------|-------------|
| SWGain | Enable software Gain correction |
| HWGain | Enable hardware Gain correction |

These options correspond to the Correct Menu definitions in the iDetector User Manual. :contentReference[oaicite:4]{index=4}

---

# 6. Defect Correction

Defect correction compensates for defective detector pixels.

Available options:

| Option | Description |
|--------|-------------|
| SWDefect | Enable software Defect correction |
| HWDefect | Enable hardware Defect correction (Mars series and Mercu detectors) |

These options correspond to the Correct Menu definitions in the iDetector User Manual. :contentReference[oaicite:5]{index=5}

---

# 7. Typical Workflow

```text
Connect Detector

↓

Acquire Page

↓

Configure Correct Menu

↓

Select Offset / Gain / Defect Options

↓

Start Acquisition

↓

Image Processing

↓

Image Display
```

---

# 8. Engineering Recommendations

Before image acquisition:

- Verify the detector has completed the required calibration.
- Select the appropriate correction items for the detector model.
- Do not arbitrarily disable correction options during routine engineering work unless troubleshooting requires it.
- Record the correction configuration when collecting abnormal images.

---

# 9. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Offset artifact | Offset correction disabled or calibration abnormal |
| Bright/Dark non-uniformity | Gain correction disabled or Gain calibration abnormal |
| Bad pixels visible | Defect correction disabled or Defect template abnormal |
| Different image quality | Different correction combinations selected |

For detailed troubleshooting, refer to:

- 05_Calibration
- 07_FailureKnowledge
- 09_DecisionTree

---

# 10. Related Documents

## Acquire Module

- README.md
- Acquisition.md
- SequenceAcquisition.md
- ImageDisplay.md
- ImageList.md
- ImageSave.md
- FAQ.md

## Knowledge Base

- ../../05_Calibration
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Image Correction documentation based on iDetector User Manual |