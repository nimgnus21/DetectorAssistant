# Generator Error Code - Configuration

> Module: Generator
>
> Category: Configuration

---

# Overview

This document describes configuration-related issues between the detector and the X-ray generator.

Incorrect configuration is one of the most common causes of exposure failures, trigger abnormalities, synchronization errors, and image acquisition failures. These issues are often caused by inconsistent settings between the detector, SDK, and generator.

Although the SDK does not define dedicated generator configuration error codes, configuration problems frequently result in task failures, timeout events, or communication abnormalities.

---

# Related Commands

- Cmd_StartAcq
- Cmd_StopAcq
- Cmd_SetCaliSubset
- Cmd_ChangeParamsOfCurrentAppMode

---

# Related Events

- Evt_TaskResult_Failed
- Evt_WaitImage_Timeout
- Evt_Exp_Enable
- Evt_Exp_Prohibit

---

# Typical Symptoms

- Detector cannot receive images.
- Exposure completes but acquisition fails.
- Trigger is ineffective.
- Dynamic acquisition frame rate is abnormal.
- Synchronization failure.
- Image timeout.

---

# Common Configuration Items

## Detector Configuration

- Detector IP
- Detector Mode
- Static / Dynamic Mode
- Application Mode (Subset)
- Trigger Mode

---

## Generator Configuration

- Trigger Output
- Exposure Time
- Exposure Delay
- Trigger Polarity
- Pulse Width
- Synchronization Mode

---

## SDK Configuration

- Working Directory
- Calibration Subset
- Continuous Acquisition
- Timeout
- Image Buffer

---

# Common Configuration Mismatches

| Detector | Generator | Result |
|----------|-----------|--------|
| External Trigger | Software Trigger | No Exposure |
| Dynamic Mode | Static Exposure | Image Timeout |
| Wrong Application Mode | Correct Generator | Acquisition Failure |
| Incorrect FPS | Continuous Exposure | Frame Loss |
| Calibration Subset Mismatch | Correct Exposure | Image Correction Failure |

---

# Related SDK Errors

Configuration problems may lead to:

- Err_PreCondition
- Err_StateErr
- Err_InvalidParamValue
- Err_InvalidParamType
- Err_TaskTimeOut
- Err_DetectorRespTimeout

---

# Diagnostic Procedure

1. Verify detector configuration.
2. Verify generator configuration.
3. Confirm detector application mode.
4. Verify trigger mode.
5. Verify synchronization mode.
6. Check frame rate configuration (dynamic detectors).
7. Verify calibration subset.
8. Review Detector.log.

---

# Dynamic Detector Configuration

Before changing dynamic acquisition parameters:

1. Execute `Cmd_SetCaliSubset`.
2. Confirm the desired Application Mode.
3. Execute `Cmd_ChangeParamsOfCurrentAppMode`.
4. Verify FPS settings.
5. Restart acquisition if required.

---

# Calibration Configuration

When hardware calibration is enabled:

- Download the calibration template.
- Select the template.
- Verify template activation.
- Ensure HW_Gain and HW_PreOffset are used together.

---

# Inspection Checklist

- Detector Ready
- Generator Ready
- Trigger Mode
- Application Mode
- Calibration Subset
- Dynamic FPS
- Synchronization Mode
- Detector.log

---

# Related DecisionTree

- 09_DecisionTree/Connection/NoExposure.md
- 09_DecisionTree/Software/DetectorNotFound.md
- 09_DecisionTree/Software/AcquisitionTimeout.md

---

# Related Workflow

- 06_Workflow/ConfigurationWorkflow.md
- 06_Workflow/ImageGenerationWorkflow.md

---

# Related Case

- 11_Case/Communication
- 11_Case/Image

---

# Related Log

```
Detector.log
```

Configuration-related issues should always be analyzed together with detector settings, generator settings, SDK configuration, application mode, and Detector.log.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |