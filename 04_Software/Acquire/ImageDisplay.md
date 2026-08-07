# Image Display

> iDetector Acquire Module - Image Display

---

# 1. Purpose

The **Image Display** function is responsible for displaying, viewing, and interactively adjusting acquired images within the iDetector software.

It provides engineers with tools for image visualization, window adjustment, image orientation, region inspection, and image property viewing during detector testing, engineering verification, calibration validation, and customer demonstrations.

The Image Display area is part of the **Acquire** page.

---

# 2. Scope

This document describes the image display functions provided in the Acquire interface.

Typical display functions include:

- Window Width / Window Level (WW/WL)
- ROI (Region of Interest)
- Mirror
- Zoom
- Image Properties

The actual functions depend on the iDetector software version.

---

# 3. Function Overview

| Function | Description |
|----------|-------------|
| WW/WL | Adjust image brightness and contrast |
| ROI | Display Region of Interest |
| Mirror | Flip displayed image |
| Zoom | Enlarge or reduce image display |
| Image Properties | Display image metadata |

---

# 4. Window Width / Window Level (WW/WL)

## Purpose

WW/WL is used to adjust image grayscale display without modifying the original image data.

Window Width controls image contrast.

Window Level controls image brightness.

Adjusting WW/WL only affects image visualization.

---

## Engineering Applications

Typical applications include:

- Image evaluation
- Exposure verification
- Detector testing
- Image quality comparison
- Customer demonstration

---

## Expected Result

- Image brightness changes.
- Image contrast changes.
- Original image data remains unchanged.

---

# 5. ROI (Region of Interest)

## Purpose

ROI allows engineers to inspect a selected region of the displayed image.

ROI is commonly used during:

- Detector evaluation
- Defect inspection
- Calibration verification
- Image quality analysis

---

## Engineering Applications

Typical applications include:

- Local image inspection
- Detector defect verification
- Artifact analysis
- Image comparison

---

# 6. Mirror

## Purpose

Mirror changes the display orientation of the image.

Typical operations include:

- Horizontal Mirror
- Vertical Mirror

Mirror affects only image display.

The acquired image data remains unchanged.

---

## Engineering Applications

Typical applications include:

- Detector orientation verification
- Customer display adjustment
- Image comparison
- Clinical display preference

---

# 7. Zoom

## Purpose

Zoom enlarges or reduces the displayed image.

Zoom is intended for image observation only.

It does not modify image resolution or image data.

---

## Engineering Applications

Typical applications include:

- Pixel inspection
- Image artifact observation
- Detector defect inspection
- ROI analysis

---

# 8. Image Properties

## Purpose

Image Properties displays the information associated with the current image.

Typical information may include:

- Image Width
- Image Height
- Bit Depth
- Image Size
- Acquisition Time
- Detector Information
- Acquisition Parameters

The displayed information depends on software version.

---

# 9. Typical Workflow

```text
Acquire Image

↓

Image Display

↓

Adjust WW/WL

↓

Zoom Image

↓

Select ROI

↓

Mirror (If Required)

↓

View Image Properties

↓

Save Image
```

---

# 10. Engineering Recommendations

When evaluating images:

- Adjust WW/WL before judging image quality.
- Use ROI when analyzing local image abnormalities.
- Use Zoom for pixel-level inspection.
- Verify Image Properties before exporting images.
- Mirror should only be used for display purposes.

---

# 11. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Image too dark | WW/WL setting inappropriate |
| Image too bright | Window Level incorrect |
| Image cannot zoom | Display refresh abnormal |
| ROI unavailable | No image loaded |
| Mirror ineffective | Display refresh issue |
| Image Properties incomplete | Image acquisition incomplete |

Detailed troubleshooting procedures are available in:

- 07_FailureKnowledge
- 09_DecisionTree
- 11_Case

---

# 12. Related Documents

## Acquire Module

- README.md
- Acquisition.md
- SequenceAcquisition.md
- ImageCorrection.md
- ImageList.md
- ImageSave.md
- FAQ.md

## Knowledge Base

- ../../08_ImageDiagnosis
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../11_Case

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Image Display documentation |