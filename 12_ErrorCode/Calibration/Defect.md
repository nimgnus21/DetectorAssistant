# Calibration Error Code - Defect

> Module: Calibration
>
> Category: Defect Calibration Error Codes

---

# Overview

This document describes error codes that may occur during Defect calibration.

Defect calibration identifies defective pixels and generates a defect template for image correction. The quality of the acquired calibration images directly affects the accuracy of the generated defect map.

---

# Related Commands

- Cmd_DefectInit
- Cmd_LoadTemporaryDefectFile
- Cmd_DefectSelectCurrent
- Cmd_DefectSelectAll
- Cmd_DefectGeneration
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

General error occurred during Defect calibration.

### Possible Causes

- Calibration interrupted.
- Detector communication failure.
- Internal calibration algorithm exception.
- Detector state changed during generation.

### Recommended Actions

1. Verify detector status is **Ready**.
2. Restart Defect calibration.
3. Check Detector.log.
4. Repeat the calibration process.

---

## Err_Cali_DataNotReadyForGen

### Description

The SDK has not received sufficient image data to generate the defect template.

### Possible Causes

- Image acquisition incomplete.
- Missing calibration images.
- Incorrect image selection.
- Acquisition interrupted.

### Recommended Actions

1. Verify all calibration images are available.
2. Repeat image acquisition if necessary.
3. Execute `Cmd_DefectGeneration` again.

---

## Err_Cali_UnexpectImage_DoseHighHigh

### Description

The acquired image dose is too high for Defect calibration.

### Possible Causes

- Exposure dose exceeds calibration requirements.
- Incorrect generator settings.
- Wrong calibration procedure.

### Recommended Actions

1. Reduce exposure dose.
2. Verify calibration protocol.
3. Acquire a new image set.

---

## Err_Cali_UnexpectImage_MistakeTrigger

### Description

The received image does not match the expected trigger or exposure mode.

### Possible Causes

- Wrong trigger mode.
- Exposure request mismatch.
- Incorrect acquisition configuration.

### Recommended Actions

1. Verify trigger mode.
2. Verify generator configuration.
3. Restart Defect calibration.

---

## Err_TooMuchDefectPoints

### Description

The generated defect map exceeds the FPGA hardware correction capacity.

### Possible Causes

- Excessive detector defects.
- Incorrect defect threshold.
- Detector hardware degradation.

### Recommended Actions

1. Review the generated defect map.
2. Reduce false defect detection.
3. Replace the detector if the defect count exceeds hardware limits.

---

## Err_FPD_HWCaliFileError

### Description

The detector cannot execute hardware calibration because the calibration template is unavailable or invalid.

### Possible Causes

- Defect template not downloaded.
- Wrong template selected.
- Template file corrupted.
- Hardware calibration configuration incorrect.

### Recommended Actions

1. Download the defect template again.
2. Select the correct hardware template.
3. Verify template integrity.

---

# Field Experience

## Pluto0900X Defect Calibration

During Defect calibration of the **Pluto0900X** series, the SDK changes its internal processing state when the **63rd image** of the third image group is received.

**Do not stop exposure after image 63.**

Image acquisition **must continue until image 64 has been received**. Stopping at image 63 may interrupt the calibration workflow and prevent successful template generation.

Recommended practice:

- Allow the third image group to complete all 64 images.
- Wait for the acquisition task to finish normally.
- Execute `Cmd_DefectGeneration`.
- Execute `Cmd_FinishGenerationProcess`.

---

## Hardware Defect Calibration

When using hardware Defect correction:

```
Cmd_DownloadCaliFile

↓

Cmd_SelectCaliFile

↓

Hardware Defect Correction Enabled
```

The detector will not use the generated template until it has been downloaded and selected.

---

## Template Generation Workflow

```
Cmd_DefectInit

↓

Acquire Defect Images

↓

Cmd_DefectSelectAll

↓

Cmd_DefectGeneration

↓

Cmd_FinishGenerationProcess
```

Do not terminate the process before `Cmd_FinishGenerationProcess` completes.

---

# Diagnostic Checklist

Verify the following items:

- Detector status is Ready.
- Trigger mode is correct.
- Exposure dose meets calibration requirements.
- Complete calibration image set acquired.
- Third image group completed successfully.
- Hardware template downloaded (if applicable).
- Detector.log contains no calibration exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Calibration/DefectFailure.md

---

# Related Case

- 11_Case/Calibration/DefectGenerationFailed.md

---

# Related Workflow

- 05_Calibration/DefectCalibration.md
- 06_Workflow/CalibrationWorkflow.md

---

# Related FailureKnowledge

- 07_FailureKnowledge/CalibrationFailure/DefectFailure.md

---

# Related Log

```
Detector.log
```

Defect calibration failures should always be analyzed together with Detector.log, calibration image completeness, trigger configuration, exposure parameters, and hardware calibration settings.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |