# Generator Error Code - Exposure

> Module: Generator
>
> Category: Exposure Control

---

# Overview

This document describes exposure-related abnormalities between the detector and the X-ray generator.

The detector relies on the generator to provide a valid exposure signal. If exposure timing, trigger mode, or generator configuration is incorrect, image acquisition may fail or produce abnormal images.

Although the SDK does not define dedicated generator exposure error codes, exposure failures are commonly reflected through SDK events and detector behavior.

---

# Related Commands

- Cmd_StartAcq
- Cmd_StopAcq
- Cmd_ClearAcq

---

# Related Events

- Evt_Exp_Enable
- Evt_Exp_Prohibit
- Evt_WaitImage_Timeout
- Evt_TaskResult_Failed

---

# Typical Symptoms

- Exposure cannot start.
- Exposure starts but no image is received.
- Exposure ends immediately.
- Detector remains waiting for exposure.
- Exposure timeout.
- Continuous acquisition stops unexpectedly.

---

# Related SDK Errors

## Err_TaskTimeOut

The acquisition task exceeded the allowed execution time.

---

## Err_DetectorRespTimeout

The detector did not respond within the expected time.

---

## Evt_WaitImage_Timeout

The detector waited for an image but no valid image was received within the timeout period.

Possible causes include:

- Generator did not expose.
- Exposure signal not received.
- Trigger configuration mismatch.
- Image transmission failure.

---

# Possible Causes

## Generator

- Generator not ready.
- Exposure inhibited.
- Incorrect exposure parameters.
- Generator fault.

---

## Detector

- Detector not in Ready state.
- Acquisition not started.
- Incorrect application mode.
- Detector busy.

---

## Trigger

- Wrong trigger mode.
- Trigger pulse not generated.
- Trigger polarity mismatch.
- Trigger cable disconnected.

---

## Configuration

- Exposure time too short.
- Exposure synchronization incorrect.
- Detector and generator configuration inconsistent.

---

# Diagnostic Procedure

1. Verify detector status is **Ready**.
2. Execute `Cmd_StartAcq`.
3. Confirm `Evt_Exp_Enable` is received.
4. Verify generator Ready status.
5. Verify trigger signal.
6. Perform an exposure.
7. Confirm `Evt_Image` is received.
8. Check `Detector.log`.

---

# Recommended Inspection Items

- Detector Ready
- Generator Ready
- Trigger cable
- Exposure cable
- Exposure parameters
- Trigger mode
- Synchronization mode
- Detector.log

---

# Related DecisionTree

- 09_DecisionTree/Connection/NoExposure.md
- 09_DecisionTree/Image/ImageLoss.md
- 09_DecisionTree/Software/AcquisitionTimeout.md

---

# Related Workflow

- 06_Workflow/ImageGenerationWorkflow.md
- 06_Workflow/ConfigurationWorkflow.md

---

# Related Case

- 11_Case/Image
- 11_Case/Communication

---

# Related Log

```
Detector.log
```

Exposure-related problems should be analyzed together with detector logs, generator configuration, trigger waveform, and acquisition timing.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |