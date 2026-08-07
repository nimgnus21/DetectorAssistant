# Generator Error Code - Interlock

> Module: Generator
>
> Category: Interlock

---

# Overview

This document describes interlock-related issues between the detector and the X-ray generator.

The generator interlock mechanism prevents X-ray exposure when required safety or operational conditions are not satisfied. If an interlock remains active, the detector will not receive a valid exposure even though acquisition has started.

Although the SDK does not define dedicated interlock error codes, interlock problems commonly result in acquisition timeout, no exposure, or missing images.

---

# Related Commands

- Cmd_StartAcq
- Cmd_StopAcq

---

# Related Events

- Evt_Exp_Enable
- Evt_Exp_Prohibit
- Evt_WaitImage_Timeout
- Evt_TaskResult_Failed

---

# Typical Symptoms

- Generator cannot expose.
- Exposure button has no effect.
- Detector remains waiting for exposure.
- Exposure is immediately prohibited.
- Acquisition times out.
- No image is received.

---

# Related SDK Events

## Evt_Exp_Prohibit

### Description

The detector reports that exposure is currently prohibited.

### Possible Causes

- Generator interlock active.
- Detector not ready.
- Acquisition not started.
- Exposure conditions not satisfied.

---

## Evt_Exp_Enable

### Description

The detector reports that exposure is permitted.

Parameter:

- Exposure window duration (ms)

This event indicates that the detector is ready to receive an exposure signal.

---

## Evt_WaitImage_Timeout

Occurs when no valid exposure or image is received before the timeout expires.

---

# Common Interlock Conditions

Exposure may be prohibited when:

- Detector is not Ready.
- Generator is not Ready.
- Trigger signal unavailable.
- Generator reports a fault.
- Emergency stop is active.
- Door safety interlock is active.
- Exposure permission has not been granted.

---

# Possible Causes

## Detector

- Detector initialization incomplete.
- Detector Busy.
- Detector disconnected.
- Incorrect acquisition mode.

---

## Generator

- Generator fault.
- Warm-up incomplete.
- Exposure disabled.
- Generator not Ready.

---

## Safety System

- Door interlock active.
- Emergency stop active.
- External safety input active.
- Radiation safety interlock active.

---

## Communication

- Trigger cable disconnected.
- Generator status not updated.
- Communication interrupted.

---

# Diagnostic Procedure

1. Verify detector status is **Ready**.
2. Verify generator status is **Ready**.
3. Confirm `Cmd_StartAcq` has completed successfully.
4. Check whether `Evt_Exp_Enable` has been received.
5. Verify that `Evt_Exp_Prohibit` is not continuously reported.
6. Check generator safety interlock status.
7. Verify trigger wiring.
8. Review `Detector.log`.

---

# Inspection Checklist

- Detector Ready
- Generator Ready
- No emergency stop
- Door interlock released
- Exposure enabled
- Trigger cable connected
- Acquisition started
- Detector.log reviewed

---

# Related DecisionTree

- 09_DecisionTree/Connection/NoExposure.md
- 09_DecisionTree/Software/AcquisitionTimeout.md

---

# Related Workflow

- 06_Workflow/PowerOnWorkflow.md
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

Interlock-related issues should always be analyzed together with generator status, detector status, safety system status, trigger configuration, and Detector.log.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |