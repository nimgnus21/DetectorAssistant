# Generator Error Code - Trigger

> Module: Generator
>
> Category: Trigger Control

---

# Overview

This document describes trigger-related abnormalities between the detector and the X-ray generator.

Trigger control determines when the detector starts image acquisition relative to the generator exposure. Incorrect trigger configuration is one of the most common causes of acquisition failures, image loss, and synchronization issues.

Although the SDK does not define dedicated trigger error codes, trigger failures are reflected through detector events, acquisition status, and image reception.

---

# Related Commands

- Cmd_StartAcq
- Cmd_StopAcq
- Cmd_SetCaliSubset

---

# Related Events

- Evt_Exp_Enable
- Evt_Exp_Prohibit
- Evt_WaitImage_Timeout
- Evt_Image
- Evt_TaskResult_Failed

---

# Typical Symptoms

- No exposure response.
- Exposure completed but no image received.
- Detector waits indefinitely for trigger.
- Exposure occurs before detector is ready.
- Trigger received multiple times.
- Continuous acquisition unexpectedly stops.

---

# Related SDK Errors

## Err_Cali_UnexpectImage_MistakeTrigger

### Description

The received image does not match the expected trigger mode or exposure request.

### Possible Causes

- Incorrect trigger mode.
- Generator trigger configuration mismatch.
- Detector acquisition mode mismatch.
- Exposure occurred outside the expected acquisition window.

### Recommended Actions

1. Verify detector trigger mode.
2. Verify generator trigger configuration.
3. Restart acquisition.
4. Repeat exposure.

---

## Evt_WaitImage_Timeout

Indicates that the detector waited for an image but no valid trigger or exposure was received within the configured timeout period.

---

# Common Trigger Modes

| Mode | Description |
|------|-------------|
| Software Trigger | Exposure initiated by software command |
| External Trigger | Exposure initiated by external trigger input |
| AED Trigger | Automatic Exposure Detection |
| Dynamic Trigger | Continuous frame acquisition synchronized with generator |

---

# Possible Causes

## Detector

- Detector not in Ready state.
- Acquisition not started.
- Incorrect application mode.
- Wrong trigger configuration.

---

## Generator

- Trigger output disabled.
- Incorrect trigger polarity.
- Trigger pulse width too short.
- Incorrect exposure timing.

---

## Wiring

- Trigger cable disconnected.
- Incorrect pin assignment.
- Poor connector contact.
- Damaged cable.

---

## Timing

- Exposure occurred before acquisition started.
- Trigger signal delayed.
- Synchronization timeout.

---

# Diagnostic Procedure

1. Confirm detector status is **Ready**.
2. Execute `Cmd_StartAcq`.
3. Verify acquisition has started.
4. Confirm trigger mode configuration.
5. Verify trigger signal using an oscilloscope if available.
6. Perform a test exposure.
7. Verify `Evt_Image` is received.
8. Review `Detector.log`.

---

# Inspection Checklist

- Detector Ready
- Acquisition started
- Trigger mode correct
- Trigger cable connected
- Trigger polarity correct
- Trigger pulse width sufficient
- Generator exposure output normal
- Detector.log reviewed

---

# Related DecisionTree

- 09_DecisionTree/Connection/NoExposure.md
- 09_DecisionTree/Image/ImageLoss.md
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

Trigger-related problems should be analyzed together with detector logs, trigger waveform, generator configuration, acquisition timing, and detector operating mode.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |