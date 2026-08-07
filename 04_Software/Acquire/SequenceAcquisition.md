# Sequence Acquisition

> iDetector Acquire Module - Continuous & Sequence Acquisition

---

# 1. Purpose

The **Sequence Acquisition** function is used to perform continuous image acquisition and manage sequential image storage.

It supports dynamic detector testing, fluoroscopy verification, engineering evaluation, and continuous image acquisition. The function includes sequence acquisition control, automatic image saving, and cine playback.

The Sequence Acquisition module consists of the following functions:

- FreeSeq
- SeqAcq
- SeqSaveSet

---

# 2. Scope

This document describes the sequence acquisition functions available in the **Acquire** page of iDetector.

The module is primarily used for:

- Dynamic detector testing
- Fluoroscopy
- Continuous image acquisition
- Engineering verification
- Detector performance evaluation
- Cine playback
- Batch image storage

---

# 3. Function Overview

| Function | Description |
|----------|-------------|
| FreeSeq | Start free sequence acquisition mode |
| SeqAcq | Start sequence acquisition |
| SeqSaveSet | Configure continuous image saving and cine playback |

---

# 4. Typical Workflow

```text
Connect Detector

↓

Detector Ready

↓

Configure Acquisition Parameters

↓

Configure SeqSaveSet (Optional)

↓

FreeSeq / SeqAcq

↓

Continuous Image Acquisition

↓

Image Display

↓

Image Automatically Added To Image List

↓

Stop

↓

Playback / Save Images
```

---

# 5. FreeSeq

## Purpose

FreeSeq starts free sequence acquisition.

After activation, the detector continuously acquires images according to the configured trigger mode until acquisition is stopped.

This mode is commonly used for:

- Dynamic detector verification
- Continuous detector testing
- Engineering performance evaluation
- Fluoroscopy testing

---

## Typical Engineering Applications

- Dynamic detector testing
- Continuous exposure verification
- Frame rate evaluation
- Communication stability testing

---

## Expected Result

- Detector enters sequence acquisition mode.
- Images are continuously displayed.
- Images are added to the Image List.
- Detector remains in acquisition mode until Stop is executed.

---

# 6. SeqAcq

## Purpose

SeqAcq starts continuous sequence acquisition.

Compared with single-image acquisition, SeqAcq is designed for obtaining multiple consecutive images.

Typical applications include:

- Dynamic imaging
- Continuous detector verification
- Engineering testing
- Long-duration acquisition

---

## Typical Workflow

```text
Detector Ready

↓

SeqAcq

↓

Continuous Exposure

↓

Image Readout

↓

Image Transfer

↓

Image Processing

↓

Image Display

↓

Image List Update

↓

Stop
```

---

## Expected Result

During sequence acquisition:

- Images are continuously generated.
- Frame count increases continuously.
- FPS information is updated.
- Image List is refreshed automatically.

---

# 7. SeqSaveSet

## Purpose

SeqSaveSet configures continuous image saving and cine playback.

According to the iDetector User Manual, this function is used to configure **BufferCine** parameters before sequence acquisition and to save cine image data after acquisition. It also provides options for image post-processing and playback. :contentReference[oaicite:0]{index=0}

---

## Available Functions

SeqSaveSet may include the following functions:

### BufferCine Configuration

Configure:

- BufferCine Enable
- Maximum Frame Count
- Buffer Size

---

### Cine Playback

After sequence acquisition is completed, cine playback functions are available.

Typical controls include:

- Play
- Stop
- Forward
- Backward

---

### Image Saving

Sequence images can be saved after acquisition.

Typical save information includes:

- Save Path
- File Name
- Image Quantity

Supported image formats include:

- RAW
- TIFF
- DICOM

The supported formats are consistent with the image saving function described in the user manual. :contentReference[oaicite:1]{index=1}

---

### Image Processing Options

The user manual describes optional post-processing functions, including:

- ProcessImage
- EnableSuperposition
- EnableRecusiveDenoising

These options are intended for post-processing and quality enhancement of sequence images. :contentReference[oaicite:2]{index=2}

---

# 8. Typical Cine Workflow

```text
Open SeqSaveSet

↓

Enable BufferCine

↓

Configure Frame Count

↓

FreeSeq / SeqAcq

↓

Acquire Images

↓

Stop

↓

Playback Images

↓

Configure Save Path

↓

Save Sequence Images
```

This workflow follows the operation sequence described in the iDetector User Manual. :contentReference[oaicite:3]{index=3}

---

# 9. Engineering Recommendations

Before sequence acquisition:

- Verify detector communication.
- Confirm detector status is Ready.
- Verify sufficient storage space.
- Configure BufferCine if cine playback is required.

During acquisition:

- Do not disconnect the detector.
- Monitor communication quality.
- Observe FPS and frame count.
- Verify images are received continuously.

After acquisition:

- Verify image completeness.
- Review cine playback if required.
- Save image data promptly.
- Archive engineering test data.

---

# 10. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| FreeSeq cannot start | Detector not Ready |
| SeqAcq fails | Communication abnormal |
| Acquisition stops unexpectedly | Trigger interruption or communication failure |
| Cine playback unavailable | BufferCine not enabled |
| Images not saved | Save path unavailable |
| Missing frames | Communication interruption or acquisition timeout |
| Playback abnormal | Incomplete sequence acquisition |

Detailed troubleshooting procedures are available in:

- 07_FailureKnowledge
- 09_DecisionTree
- 11_Case

---

# 11. Related Documents

## Acquire Module

- README.md
- Acquisition.md
- ImageCorrection.md
- ImageDisplay.md
- ImageList.md
- ImageSave.md
- FAQ.md

## Knowledge Base

- ../../03_Hardware
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Sequence Acquisition documentation based on iDetector User Manual |