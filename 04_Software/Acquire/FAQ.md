# FAQ

> Frequently Asked Questions — Acquire Module

---

# 1. Purpose

This document summarizes the most frequently encountered questions related to the **Acquire** module of the iDetector software.

It provides Field Application Engineers (FAEs), Technical Support Engineers, and Service Engineers with quick troubleshooting guidance for image acquisition, sequence acquisition, image correction, image display, and image saving.

Detailed troubleshooting procedures are available in the corresponding **Failure Knowledge**, **Decision Tree**, and **SOP** modules.

---

# 2. Frequently Asked Questions

---

## Q1. Why does Acquire not respond after clicking?

### Possible Causes

- Detector not connected
- Detector status is not Ready
- SDK initialization failed
- Detector is occupied by another application
- Communication interrupted

### Recommended Actions

- Verify detector connection.
- Check Detector Status.
- Restart detector communication.
- Verify SDK operation.
- Refer to the Connection Decision Tree if necessary.

---

## Q2. Why is no image displayed after exposure?

### Possible Causes

- Exposure not triggered
- Communication timeout
- Detector acquisition failed
- Image transmission interrupted

### Recommended Actions

- Verify X-ray generator exposure.
- Verify detector trigger mode.
- Check detector communication.
- Review software logs.

---

## Q3. Why does PrepAcq fail?

### Possible Causes

- Detector initialization failed
- Communication abnormal
- Detector Busy
- Previous acquisition not completed

### Recommended Actions

- Stop current acquisition.
- Reconnect detector.
- Restart iDetector.
- Retry PrepAcq.

---

## Q4. Why does the detector remain Busy?

### Possible Causes

- Sequence acquisition still running
- Previous acquisition not exited
- Communication timeout

### Recommended Actions

- Click Stop.
- Verify detector status.
- Restart detector if necessary.

---

## Q5. Why are images missing during sequence acquisition?

### Possible Causes

- Network instability
- Communication timeout
- Frame transmission interrupted
- Insufficient computer performance

### Recommended Actions

- Verify network stability.
- Reduce acquisition load if necessary.
- Collect software logs.
- Verify frame count.

---

## Q6. Why can't sequence images be saved?

### Possible Causes

- SeqSaveSet not configured
- Invalid save directory
- Insufficient disk space
- Save interrupted

### Recommended Actions

- Configure SeqSaveSet.
- Verify save path.
- Verify disk capacity.
- Repeat save operation.

According to the iDetector User Manual, **SeqSaveSet** is used to configure continuous image saving and cine playback. :contentReference[oaicite:0]{index=0}

---

## Q7. Which image formats are supported?

According to the iDetector User Manual, the Save function supports:

- RAW
- TIFF
- DICOM (DCM)

:contentReference[oaicite:1]{index=1}

---

## Q8. Why are bad pixels still visible?

### Possible Causes

- Defect correction disabled
- Incorrect defect template
- Detector requires recalibration

### Recommended Actions

- Verify SWDefect/HWDefect settings.
- Verify defect template.
- Perform Defect Calibration.

---

## Q9. Why is image brightness abnormal?

### Possible Causes

- Offset correction abnormal
- Gain correction abnormal
- WW/WL display settings inappropriate

### Recommended Actions

- Verify Offset calibration.
- Verify Gain calibration.
- Reset WW/WL.
- Compare with original RAW image.

---

## Q10. Why does the displayed image differ from the saved RAW image?

### Explanation

WW/WL, Mirror, Zoom, and ROI affect **display only**.

RAW image data is not modified by these display operations.

If image processing is enabled, the processed image may differ from the original RAW image.

---

# 3. Engineering Recommendations

When troubleshooting acquisition problems:

- Verify detector connection first.
- Confirm detector status is **Ready**.
- Check correction settings before exposure.
- Save RAW images whenever possible.
- Record firmware version, SDK version, and detector model.
- Export logs before escalating to R&D.

---

# 4. Related Documents

## Acquire Module

- README.md
- Acquisition.md
- SequenceAcquisition.md
- ImageCorrection.md
- ImageDisplay.md
- ImageList.md
- ImageSave.md

## Knowledge Base

- ../../03_Hardware
- ../../05_Calibration
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case
- ../../12_ErrorCode
- ../../17_Tools

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Acquire FAQ documentation based on iDetector User Manual |