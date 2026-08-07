# Image Save

> iDetector Acquire Module - Image Saving

---

# 1. Purpose

The **Image Save** function is responsible for saving acquired images to the local computer.

It supports multiple image formats for engineering verification, clinical testing, calibration validation, quality inspection, and technical support.

Image saving can be performed for both single-image acquisition and sequence acquisition.

---

# 2. Scope

This document describes the image saving functions available in the **Acquire** page.

Image saving includes:

- Save Current Image
- Select Image Format
- Save Sequence Images
- Configure Sequence Save Parameters

According to the iDetector User Manual, supported image formats include:

- RAW
- TIFF
- DICOM (DCM)

:contentReference[oaicite:2]{index=2}

---

# 3. Function Overview

The Image Save function allows engineers to store acquired images for later analysis or documentation.

Typical functions include:

- Save current image
- Select image format
- Specify save location
- Save sequence images
- Export cine images

---

# 4. Supported Image Formats

According to the iDetector User Manual, the following formats are supported.

| Format | Description | Typical Application |
|---------|-------------|---------------------|
| RAW | Original detector image | Engineering analysis |
| TIFF | Standard lossless image | Image processing and evaluation |
| DICOM (DCM) | Medical image format | PACS / Clinical workflow |

:contentReference[oaicite:3]{index=3}

---

# 5. Save Current Image

## Purpose

Save the currently displayed image to the local computer.

Typical workflow:

```text
Acquire Image

↓

Display Image

↓

Click Save

↓

Select Image Format

↓

Select Save Location

↓

Save Image
```

---

## Expected Result

- Image is successfully written to disk.
- File format matches the selected format.
- Image can be opened normally.

---

# 6. Sequence Image Saving

Sequence acquisition images can be saved using **SeqSaveSet**.

According to the iDetector User Manual, SeqSaveSet is used to configure continuous image saving and cine playback parameters before or after sequence acquisition. :contentReference[oaicite:4]{index=4}

Typical workflow:

```text
Configure SeqSaveSet

↓

Sequence Acquisition

↓

Stop

↓

Playback (Optional)

↓

Configure Save Path

↓

Save Sequence Images
```

---

# 7. Engineering Applications

Typical engineering scenarios include:

- Saving engineering test images
- Saving customer verification images
- Saving calibration verification images
- Saving firmware verification images
- Exporting images for technical support
- Recording detector performance
- Archiving quality inspection results

---

# 8. Engineering Recommendations

When saving images:

- Verify image quality before saving.
- Select the appropriate file format for the intended use.
- Save important engineering images immediately after acquisition.
- Keep the original RAW images whenever possible for troubleshooting.
- Record detector information together with exported images.

---

# 9. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Save button unavailable | No image loaded |
| Save failed | Invalid save path |
| File not generated | Disk write failure |
| Unsupported format | Incorrect save configuration |
| Sequence images not saved | SeqSaveSet not configured |
| Incomplete sequence | Acquisition interrupted |

For detailed troubleshooting, refer to:

- 07_FailureKnowledge
- 09_DecisionTree
- 11_Case

---

# 10. Related Documents

## Acquire Module

- README.md
- Acquisition.md
- SequenceAcquisition.md
- ImageCorrection.md
- ImageDisplay.md
- ImageList.md
- FAQ.md

## Knowledge Base

- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Image Save documentation based on iDetector User Manual |