# Acquisition

> iDetector Acquire Module - Image Acquisition

---

# 1. Purpose

The **Acquisition** function is the core function of the iDetector software and is responsible for controlling detector image acquisition.

It provides engineers with functions for detector preparation, image acquisition, acquisition interruption, and acquisition status monitoring. All image generation operations are initiated through this module.

---

# 2. Scope

This document describes the acquisition control functions available on the **Acquire** page.

The acquisition control area includes:

- PrepAcq
- Acquire
- Stop

These functions are used during detector testing, calibration verification, customer demonstrations, factory testing, and clinical image acquisition.

---

# 3. Function Overview

The acquisition workflow consists of three basic operations.

| Function | Description |
|----------|-------------|
| PrepAcq | Prepare detector for image acquisition |
| Acquire | Start image acquisition |
| Stop | Stop the current acquisition task |

These three operations form a complete acquisition workflow.

---

# 4. Typical Workflow

```text
Connect Detector

↓

Detector Ready

↓

PrepAcq

↓

Detector Enter Ready State

↓

Acquire

↓

Detector Waits for Exposure

↓

Image Received

↓

Image Displayed

↓

Stop (If Required)

↓

Return to Ready State
```

---

# 5. PrepAcq

## Purpose

PrepAcq (Prepare Acquisition) initializes the detector before image acquisition.

Depending on detector type and acquisition mode, this operation may:

- Initialize detector electronics
- Synchronize detector status
- Clear previous acquisition state
- Prepare communication buffers
- Enter acquisition-ready state

PrepAcq should normally be executed before Acquire.

---

## Typical Engineering Applications

- First acquisition after detector connection
- Acquisition after calibration
- Acquisition after firmware upgrade
- Detector recovery after communication interruption
- Continuous engineering testing

---

## Expected Result

After successful execution:

- Detector Status = Ready
- No Error Message
- Detector waits for acquisition command

---

# 6. Acquire

## Purpose

Acquire starts image acquisition.

After execution, the detector enters image acquisition mode and waits for an exposure trigger according to the configured trigger mode.

Possible trigger modes include:

- Internal Trigger
- External Trigger
- AED Trigger

The actual trigger mode depends on detector configuration.

---

## Typical Workflow

```text
PrepAcq

↓

Acquire

↓

Detector Waiting

↓

Exposure Trigger

↓

Image Readout

↓

Image Transfer

↓

Image Processing

↓

Image Display
```

---

## Engineering Applications

Acquire is commonly used for:

- Detector functional testing
- Clinical image acquisition
- Calibration verification
- Factory inspection
- Customer acceptance testing
- Dynamic acquisition
- Sequence acquisition

---

## Expected Result

A successful acquisition should produce:

- New image displayed
- Image added to Image List
- No communication error
- Detector returns to Ready state (depending on acquisition mode)

---

# 7. Stop

## Purpose

Stop terminates the current acquisition process.

Depending on the acquisition mode, Stop may:

- Cancel waiting for exposure
- Stop continuous acquisition
- Stop sequence acquisition
- Return detector to idle or ready state

---

## Engineering Applications

Typical scenarios include:

- End current acquisition
- Cancel incorrect operation
- Stop continuous acquisition
- Stop sequence acquisition
- Recover from abnormal acquisition state

---

## Expected Result

After Stop:

- Detector exits acquisition mode.
- Current task ends.
- Detector status returns to Ready or Idle.
- No acquisition task remains active.

---

# 8. Engineering Recommendations

Before acquisition:

- Verify detector connection.
- Verify detector status is Ready.
- Verify communication is stable.
- Verify trigger mode is correct.
- Verify detector calibration status.

During acquisition:

- Do not disconnect the detector.
- Do not restart the software.
- Observe Status and Message information.
- Verify image transfer completes successfully.

After acquisition:

- Confirm image quality.
- Verify image appears in Image List.
- Save images if required.
- Record abnormal behavior if observed.

---

# 9. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| PrepAcq failed | Detector communication abnormal |
| Acquire no response | Detector not Ready |
| No image received | No exposure trigger |
| Acquisition timeout | Communication timeout |
| Stop unavailable | Detector task not started |
| Detector Busy | Previous acquisition not completed |
| Image not displayed | Image transfer or processing abnormal |

Detailed troubleshooting procedures are available in:

- 07_FailureKnowledge
- 09_DecisionTree
- 11_Case

---

# 10. Related Documents

## Acquire Module

- README.md
- SequenceAcquisition.md
- ImageCorrection.md
- ImageDisplay.md
- ImageList.md
- ImageSave.md
- FAQ.md

## Knowledge Base

- ../../03_Hardware
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Acquisition documentation |