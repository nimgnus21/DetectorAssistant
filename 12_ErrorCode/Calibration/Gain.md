# Calibration Error Code - Gain

> Module: Calibration
>
> Category: Gain Calibration Error Codes

---

# Overview

This document describes error codes that may occur during Gain calibration.

Gain calibration compensates for pixel sensitivity differences and ensures detector output uniformity.

An abnormal Gain template may result in image non-uniformity, brightness inconsistency, vertical or horizontal banding, and calibration failure.

---

# Related Commands

- Cmd_GainInit
- Cmd_GainSelectCurrent
- Cmd_GainSelectAll
- Cmd_GainGeneration
- Cmd_FinishGenerationProcess
- Cmd_DownloadCaliFile
- Cmd_SelectCaliFile

---

# Related Events

- Evt_TaskResult_Succeed
- Evt_TaskResult_Failed
- Evt_GeneralError

---

# Error Codes

---

## Err_Cali_GeneralError

### Description

A general error occurred during Gain calibration.

### Possible Causes

- Calibration process interrupted.
- Detector communication abnormal.
- Detector disconnected during acquisition.
- Internal calibration algorithm failed.

### Recommended Actions

1. Verify detector status is **Ready**.
2. Restart Gain calibration.
3. Check Detector.log.
4. Verify detector communication.

---

## Err_Cali_DataNotReadyForGen

### Description

The SDK has not received enough images to generate the Gain template.

### Possible Causes

- Gain image acquisition incomplete.
- Some images were lost.
- Selected images are insufficient.
- Calibration process interrupted.

### Recommended Actions

1. Verify all Gain images have been acquired.
2. Reacquire missing images.
3. Execute `Cmd_GainGeneration` again.
4. Complete the calibration process.

---

# Field Experience

## Image Completeness

Gain calibration requires a complete image set.

If even a small number of images are missing:

- GainGeneration may fail.
- The generated template may be inaccurate.
- Brightness correction may become unstable.

Always verify that all required images have been received before template generation.

---

## Image Selection

Before generating the Gain template, images must be selected using:

- Cmd_GainSelectCurrent
- Cmd_GainSelectAll

Selecting incorrect images or an incomplete image set may lead to template generation failure.

---

## Hardware Gain

When **HW_Gain** is used:

- Gain templates must first be downloaded to the detector.
- The hardware Gain template must be selected before image acquisition.

Required commands:

```
Cmd_DownloadCaliFile

↓

Cmd_SelectCaliFile
```

If HW_Gain is enabled, **PreOffset must also use hardware calibration**.

Mixing software Offset with hardware Gain is not recommended and may result in incorrect correction.

---

## Calibration Workflow

```
Cmd_GainInit

↓

Acquire Gain Images

↓

Cmd_GainSelectAll

↓

Cmd_GainGeneration

↓

Cmd_FinishGenerationProcess
```

Do not interrupt the workflow before `Cmd_FinishGenerationProcess` completes.

---

# Diagnostic Checklist

Verify the following items before generating the Gain template:

- Detector status is **Ready**.
- Exposure parameters are correct.
- All Gain images have been acquired.
- Image sequence is complete.
- Detector communication is stable.
- Detector.log contains no calibration exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Calibration/GainFailure.md

---

# Related Case

- 11_Case/Calibration/GainGenerationFailed.md

---

# Related Workflow

- 05_Calibration/GainCalibration.md
- 06_Workflow/CalibrationWorkflow.md

---

# Related FailureKnowledge

- 07_FailureKnowledge/CalibrationFailure/GainFailure.md

---

# Related Log

```
Detector.log
```

Gain calibration failures should always be analyzed together with Detector.log, exposure parameters, image completeness, and hardware calibration configuration.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |