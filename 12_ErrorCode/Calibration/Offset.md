# Calibration Error Code - Offset

> Module: Calibration
>
> Category: Offset Calibration Error Codes

---

# Overview

This document describes error codes that may occur during Offset calibration.

Offset calibration is the foundation of detector image correction. It compensates for detector dark current and electronic offset before Gain and Defect calibration.

An abnormal Offset template will directly affect subsequent image quality and may lead to Gain or Defect calibration failures.

---

# Related Commands

- Cmd_OffsetGeneration
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

General error occurred during Offset calibration.

### Possible Causes

- Calibration process interrupted.
- Detector communication abnormal.
- Detector state changed during calibration.
- Internal calibration algorithm failed.

### Recommended Actions

1. Verify detector status is **Ready**.
2. Restart the Offset calibration process.
3. Check Detector.log.
4. Restart the detector if necessary.

---

## Err_Cali_DataNotReadyForGen

### Description

The SDK has not received sufficient image data to generate the Offset template.

### Possible Causes

- Offset image acquisition not completed.
- Calibration interrupted.
- Image acquisition failed.
- Selected images are insufficient.

### Recommended Actions

1. Complete the required Offset image acquisition.
2. Verify all images were received successfully.
3. Restart Offset calibration.
4. Execute template generation again.

---

## Err_Cali_NotEnoughIntervalTime_OffsetTmpl

### Description

Insufficient idle time has elapsed since the previous acquisition to generate a valid Offset template.

Residual signal (ghost image) may still exist in the detector.

### Possible Causes

- Offset calibration started immediately after exposure.
- Detector has not completely recovered.
- Previous exposure dose was high.
- Detector temperature has not stabilized.

### Recommended Actions

1. Wait several minutes before generating the Offset template.
2. Ensure no residual exposure exists.
3. Restart Offset calibration.
4. If necessary, perform additional dark acquisitions.

---

# Field Experience

## Residual Image (Ghost)

If Offset calibration is started immediately after a high-dose exposure, detector residual signal may remain.

Typical symptoms include:

- Ghost artifacts after Offset correction.
- Offset template instability.
- Increased image noise.

Always allow sufficient recovery time before generating the Offset template.

---

## Generation Process

A complete Offset calibration workflow should be:

```
Cmd_OffsetGeneration

↓

Acquire Offset Images

↓

Evt_TaskResult_Succeed

↓

Generate Offset Template

↓

Cmd_FinishGenerationProcess
```

Do **not** interrupt the process before `Cmd_FinishGenerationProcess` completes.

---

## Hardware Calibration

When using hardware calibration:

1. Generate the Offset template.
2. Download the template using `Cmd_DownloadCaliFile`.
3. Select the template using `Cmd_SelectCaliFile`.
4. Verify the template has been loaded successfully before acquisition.

---

# Diagnostic Checklist

Verify the following items before regenerating the Offset template:

- Detector status is **Ready**.
- Detector temperature is stable.
- No recent high-dose exposure.
- Offset image acquisition completed.
- Detector communication is stable.
- Detector.log contains no calibration exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Calibration/OffsetFailure.md

---

# Related Case

- 11_Case/Calibration/OffsetGenerationFailed.md

---

# Related Workflow

- 05_Calibration/OffsetCalibration.md
- 06_Workflow/CalibrationWorkflow.md

---

# Related FailureKnowledge

- 07_FailureKnowledge/CalibrationFailure/OffsetFailure.md

---

# Related Log

```
Detector.log
```

Offset calibration failures should always be analyzed together with Detector.log, detector temperature, exposure history, and calibration image completeness.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |