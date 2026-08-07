# Generator Error Code - Generator Fault

> Module: Generator
>
> Category: Generator Fault

---

# Overview

This document describes common generator faults that may affect detector operation.

Unlike detector or SDK errors, generator faults are reported by the X-ray generator itself. Although these faults are not returned as SDK error codes, they frequently result in acquisition failures, exposure timeout, missing images, or communication abnormalities.

This document provides engineering guidance for identifying generator-originated failures during field troubleshooting.

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

- Generator cannot perform exposure.
- Exposure request rejected.
- Detector waits indefinitely.
- No trigger signal.
- Exposure interrupted.
- Image acquisition timeout.
- No image received.

---

# Common Generator Faults

---

## Generator Not Ready

### Description

The generator has not entered the Ready state and cannot execute an exposure.

### Possible Causes

- Startup incomplete.
- Initialization failed.
- Warm-up not finished.
- Internal self-test in progress.

### Recommended Actions

1. Verify generator status.
2. Wait until Ready.
3. Retry exposure.

---

## Warm-up Required

### Description

The X-ray tube requires a warm-up procedure before exposure.

### Possible Causes

- Generator powered on after a long shutdown.
- Tube protection mechanism activated.
- Warm-up sequence incomplete.

### Recommended Actions

1. Execute the manufacturer's warm-up procedure.
2. Wait until Ready is reported.
3. Retry acquisition.

---

## High Voltage Fault

### Description

The generator cannot establish or maintain the required high voltage.

### Possible Causes

- HV power supply failure.
- Generator internal protection.
- Electrical abnormality.

### Typical Symptoms

- Exposure cannot begin.
- Exposure stops immediately.
- Detector receives no image.

### Recommended Actions

1. Check generator fault information.
2. Restart the generator if permitted.
3. Contact generator manufacturer if the fault persists.

---

## Tube Fault

### Description

The X-ray tube reports an abnormal operating condition.

### Possible Causes

- Tube overload.
- Tube overheating.
- Tube aging.
- Tube protection activated.

### Recommended Actions

1. Allow the tube to cool.
2. Verify exposure parameters.
3. Reduce continuous exposure load.
4. Replace the tube if necessary.

---

## Exposure Fault

### Description

The exposure sequence cannot be completed successfully.

### Possible Causes

- Exposure interrupted.
- Incorrect exposure parameters.
- Generator protection activated.
- Internal control failure.

### Recommended Actions

1. Verify exposure settings.
2. Perform a test exposure.
3. Check generator fault logs.

---

## Interlock Fault

### Description

Exposure is blocked because one or more safety interlocks remain active.

### Possible Causes

- Door interlock active.
- Emergency stop activated.
- External safety circuit open.
- Generator safety condition not satisfied.

### Recommended Actions

1. Release all safety interlocks.
2. Verify emergency stop status.
3. Confirm exposure permission is restored.

---

## Communication Fault

### Description

The generator cannot communicate correctly with the detector or host system.

### Possible Causes

- Communication cable disconnected.
- Network abnormal.
- Incorrect communication parameters.
- Hardware communication failure.

### Typical Symptoms

- Exposure command ignored.
- Trigger not received.
- Acquisition timeout.

### Recommended Actions

1. Verify communication cables.
2. Check network settings.
3. Restart communication devices.

---

## Trigger Output Fault

### Description

The generator fails to output the expected trigger signal.

### Possible Causes

- Trigger disabled.
- Incorrect trigger polarity.
- Trigger hardware failure.
- Incorrect configuration.

### Recommended Actions

1. Verify trigger output configuration.
2. Measure the trigger signal.
3. Verify trigger wiring.

---

## Emergency Stop Active

### Description

The emergency stop circuit is active, preventing exposure.

### Possible Causes

- Emergency stop button pressed.
- Safety circuit open.
- External emergency input active.

### Recommended Actions

1. Reset the emergency stop.
2. Verify all safety circuits.
3. Confirm generator returns to Ready.

---

# Fault Impact on Detector

| Generator Fault | Detector Behavior |
|-----------------|-------------------|
| Generator Not Ready | Wait for exposure |
| Warm-up Required | Exposure unavailable |
| High Voltage Fault | No exposure |
| Tube Fault | Exposure interrupted |
| Exposure Fault | Acquisition failed |
| Interlock Fault | Evt_Exp_Prohibit |
| Communication Fault | Timeout / No Image |
| Trigger Output Fault | No trigger detected |
| Emergency Stop | Exposure prohibited |

---

# Related SDK Events

Generator faults commonly result in one or more of the following SDK events:

- Evt_Exp_Prohibit
- Evt_WaitImage_Timeout
- Evt_TaskResult_Failed

Common related SDK errors include:

- Err_TaskTimeOut
- Err_DetectorRespTimeout
- Err_StateErr

---

# Diagnostic Procedure

1. Verify generator status is **Ready**.
2. Check whether any generator fault is active.
3. Verify warm-up has completed.
4. Confirm no interlock is active.
5. Verify trigger output.
6. Perform a test exposure.
7. Confirm the detector receives `Evt_Image`.
8. Review `Detector.log` together with the generator fault log.

---

# Inspection Checklist

- Generator Ready
- No active fault
- Warm-up completed
- High voltage normal
- Tube status normal
- Trigger output normal
- Safety interlocks released
- Communication normal
- Detector Ready
- Detector.log reviewed

---

# Related DecisionTree

- 09_DecisionTree/Connection/NoExposure.md
- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Image/ImageLoss.md

---

# Related Workflow

- 06_Workflow/PowerOnWorkflow.md
- 06_Workflow/ConfigurationWorkflow.md
- 06_Workflow/ImageGenerationWorkflow.md

---

# Related Case

- 11_Case/Communication
- 11_Case/Image

---

# Related Log

```text
Detector.log
```

Generator fault analysis should always be performed together with the generator's own fault records, detector status, trigger signals, and Detector.log to determine whether the failure originates from the generator or the detector.

---

# See Also

- GeneratorState.md
- Communication.md
- Exposure.md
- Trigger.md
- Interlock.md
- Configuration.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |