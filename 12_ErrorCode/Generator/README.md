# Generator Error Code

> Module: Generator
>
> Category: Error Code Reference

---

# Overview

This module describes common generator-related abnormalities that may affect detector operation.

Unlike SDK or detector firmware errors, generator-related problems usually originate from generator configuration, trigger synchronization, exposure control, safety interlock, communication, or generator hardware faults.

Although most generators do not return standardized SDK error codes, these failures frequently manifest as detector acquisition timeout, missing images, exposure failure, or synchronization abnormalities.

This module provides engineering-oriented troubleshooting guidance for generator-related issues encountered during detector installation, integration, and field service.

---

# Scope

This module applies to:

- Generator communication
- Exposure control
- Trigger synchronization
- Safety interlock
- Generator operating state
- Generator hardware fault
- Generator configuration

---

# Directory Structure

```text
Generator
├── README.md
├── Communication.md
├── Exposure.md
├── Trigger.md
├── Interlock.md
├── GeneratorState.md
├── GeneratorFault.md
└── Configuration.md
```

---

# Module Description

## Communication

Communication between the detector and the generator.

Typical topics include:

- Communication interruption
- Trigger cable problems
- Network or interface failures
- Generator connectivity

---

## Exposure

Exposure execution and detector synchronization.

Typical topics include:

- Exposure timeout
- No exposure
- Exposure interruption
- Image acquisition timeout

---

## Trigger

Trigger signal generation and synchronization.

Typical topics include:

- Trigger mode mismatch
- Trigger polarity
- Trigger timing
- Missing trigger signal

---

## Interlock

Safety mechanisms that prevent exposure.

Typical topics include:

- Exposure prohibited
- Door interlock
- Emergency stop
- Safety input
- Exposure permission

---

## GeneratorState

Operating status of the generator.

Typical topics include:

- Ready
- Busy
- Standby
- Warming Up
- Exposure Enabled
- Exposure Prohibited
- Offline
- Fault

---

## GeneratorFault

Generator hardware or internal system faults.

Typical topics include:

- High Voltage Fault
- Tube Fault
- Exposure Fault
- Communication Fault
- Trigger Output Fault
- Interlock Fault
- Emergency Stop
- Generator Not Ready

---

## Configuration

Generator and detector configuration consistency.

Typical topics include:

- Trigger mode
- Synchronization mode
- Exposure parameters
- Application Mode
- Dynamic configuration
- Calibration configuration

---

# Typical Troubleshooting Workflow

```text
Problem Observed

↓

Generator Ready?

↓

Detector Ready?

↓

Exposure Enabled?

↓

Trigger Generated?

↓

Image Received?

↓

Detector.log Analysis

↓

Generator Fault Check

↓

Resolve or Escalate
```

---

# Common Symptoms

| Symptom | Possible Module |
|----------|-----------------|
| Cannot expose | Interlock / GeneratorFault |
| No trigger signal | Trigger / Communication |
| Exposure timeout | Exposure / Communication |
| Detector waits indefinitely | GeneratorState / Trigger |
| No image received | Exposure / Communication |
| Generator reports fault | GeneratorFault |
| Exposure prohibited | Interlock |
| Acquisition abnormal | Configuration |

---

# Related SDK Events

Generator-related issues commonly result in one or more of the following SDK events:

- Evt_Exp_Enable
- Evt_Exp_Prohibit
- Evt_WaitImage_Timeout
- Evt_TaskResult_Failed
- Evt_Image

---

# Related SDK Error Codes

Although the SDK does not define dedicated generator error codes, the following errors are frequently associated with generator-related problems:

- Err_TaskTimeOut
- Err_DetectorRespTimeout
- Err_StateErr
- Err_Cali_UnexpectImage_MistakeTrigger

---

# Recommended Troubleshooting Procedure

When generator-related abnormalities occur:

1. Verify the generator status is **Ready**.
2. Verify the detector status is **Ready**.
3. Confirm acquisition has started successfully.
4. Verify exposure permission (`Evt_Exp_Enable`).
5. Check trigger mode and synchronization.
6. Verify trigger cable and communication interface.
7. Perform a test exposure.
8. Confirm `Evt_Image` is received.
9. Review `Detector.log`.
10. Review the generator fault log if available.
11. Follow the corresponding DecisionTree.

---

# Related Modules

## DecisionTree

```text
09_DecisionTree
```

---

## Workflow

```text
06_Workflow
```

Especially:

- PowerOnWorkflow.md
- ConfigurationWorkflow.md
- ImageGenerationWorkflow.md

---

## FailureKnowledge

```text
07_FailureKnowledge
```

---

## Case

```text
11_Case
```

---

# Related Log

```text
Detector.log
```

For generator-related issues, it is recommended to collect:

- Detector.log
- Generator fault log (if available)
- Detector Model
- Detector Serial Number
- Generator Model
- SDK Version
- Firmware Version
- Trigger Configuration
- Exposure Parameters
- Communication Configuration
- Reproduction Procedure

---

# Engineering Notes

Generator-related issues are often caused by configuration mismatches rather than hardware failures. During troubleshooting, always verify the following in order:

1. Generator status
2. Detector status
3. Trigger configuration
4. Exposure synchronization
5. Communication
6. Hardware faults

Following this sequence can significantly improve troubleshooting efficiency and reduce unnecessary hardware replacement.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |