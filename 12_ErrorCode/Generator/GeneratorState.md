# Generator Error Code - Generator State

> Module: Generator
>
> Category: Generator State

---

# Overview

This document describes the operating states of the X-ray generator and their impact on detector operation.

Although the SDK does not define dedicated Generator State error codes, incorrect generator states are a common cause of acquisition failure, exposure timeout, synchronization abnormalities, and image loss.

Understanding the generator state helps engineers quickly determine whether the problem originates from the detector, SDK, communication, or the generator itself.

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

# Generator States

---

## Ready

### Description

The generator has completed initialization and is ready to perform an exposure.

### Detector Behavior

- Exposure permitted.
- Image acquisition can begin normally.
- Detector waits for the exposure signal.

### Expected SDK Events

- Evt_Exp_Enable
- Evt_Image

---

## Busy

### Description

The generator is currently executing another operation.

Examples include:

- Previous exposure not completed.
- Generator warm-up.
- Internal processing.
- System self-check.

### Possible Symptoms

- Exposure request rejected.
- Exposure delayed.
- Detector waits for image.
- Acquisition timeout.

### Recommended Actions

1. Wait until the generator returns to Ready.
2. Verify no previous exposure is active.
3. Retry the acquisition.

---

## Standby

### Description

The generator is powered on but not prepared for exposure.

### Possible Symptoms

- Exposure button has no effect.
- Detector waits indefinitely.
- No trigger output.

### Recommended Actions

1. Switch the generator to Ready mode.
2. Verify exposure preparation is complete.

---

## Warming Up

### Description

The generator is performing tube warm-up or internal stabilization.

### Possible Symptoms

- Exposure disabled.
- Generator refuses exposure commands.
- Detector receives no image.

### Recommended Actions

1. Complete the warm-up procedure.
2. Retry exposure after the generator reports Ready.

---

## Exposure Enabled

### Description

The generator is permitted to perform exposure.

Detector receives:

```
Evt_Exp_Enable
```

After this event, the detector waits for the exposure signal.

---

## Exposure Prohibited

### Description

Exposure is currently prohibited.

Detector receives:

```
Evt_Exp_Prohibit
```

### Possible Causes

- Generator interlock active.
- Detector not Ready.
- Safety condition not satisfied.
- Exposure disabled.

---

## Offline

### Description

The generator cannot communicate with the detector or control software.

### Possible Symptoms

- No trigger output.
- No exposure.
- Communication timeout.

### Recommended Actions

1. Verify communication cables.
2. Verify generator power.
3. Verify network or interface configuration.

---

## Fault

### Description

The generator reports an internal fault and cannot perform exposure.

Typical faults include:

- High-voltage fault.
- Tube fault.
- Interlock fault.
- Internal hardware fault.

Detailed fault descriptions are provided in:

```
GeneratorFault.md
```

---

# Relationship Between Generator State and Detector

| Generator State | Detector Behavior | Expected Result |
|-----------------|-------------------|-----------------|
| Ready | Waiting for exposure | Normal acquisition |
| Busy | Waiting | Exposure delayed |
| Standby | Waiting | No exposure |
| Warming Up | Waiting | Exposure unavailable |
| Exposure Enabled | Ready for image | Normal exposure |
| Exposure Prohibited | Exposure blocked | No image |
| Offline | Communication failure | Acquisition failure |
| Fault | Exposure rejected | No acquisition |

---

# Common Symptoms by State

| Symptom | Possible Generator State |
|----------|--------------------------|
| Cannot expose | Standby / Fault / Exposure Prohibited |
| Exposure timeout | Busy / Offline |
| No image | Offline / Exposure Prohibited |
| Trigger missing | Standby / Offline |
| Exposure delayed | Busy |
| Continuous acquisition interrupted | Fault / Busy |

---

# Diagnostic Procedure

1. Verify the generator reports **Ready**.
2. Confirm the detector status is **Ready**.
3. Check whether `Evt_Exp_Enable` has been received.
4. Verify that no `Evt_Exp_Prohibit` event is active.
5. Confirm the trigger signal is generated correctly.
6. Perform a test exposure.
7. Verify `Evt_Image` is received.
8. Review `Detector.log`.

---

# Inspection Checklist

- Generator Ready
- Detector Ready
- Generator not Busy
- Warm-up completed
- Exposure enabled
- Trigger output normal
- No active interlock
- Detector.log reviewed

---

# Related DecisionTree

- 09_DecisionTree/Connection/NoExposure.md
- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Image/ImageLoss.md

---

# Related Workflow

- 06_Workflow/PowerOnWorkflow.md
- 06_Workflow/ImageGenerationWorkflow.md
- 06_Workflow/ConfigurationWorkflow.md

---

# Related Case

- 11_Case/Communication
- 11_Case/Image

---

# Related Log

```text
Detector.log
```

Generator state abnormalities should always be analyzed together with detector status, trigger signals, exposure timing, communication status, and Detector.log.

---

# See Also

- GeneratorFault.md
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