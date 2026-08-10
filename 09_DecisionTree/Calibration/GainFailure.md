# Gain Calibration Failed Decision Tree

> Module: Calibration
>
> Category: Decision Tree
>
> Version: v1.1
>
> Last Updated: 2026-08-10

---

# Symptom

Gain calibration cannot be completed successfully.

Typical symptoms include:

- Gain Calibration Failed
- Gain file generation failed
- Exposure verification failed
- Gain verification failed
- Calibration process terminated unexpectedly

---

# Diagnostic Flow

```
                 Gain Calibration Failed
                            │
                   Detector Connected?
                            │
               ┌────────────┴────────────┐
               │                         │
              NO                        YES
               │                         │
      Go to Connection Tree        Continue
                                        │
                                        ▼
                    Firmware Compatible?
                                        │
                        ┌───────────────┴───────────────┐
                        │                               │
                       NO                              YES
                        │                               │
               Go to Version Mismatch          Continue
                                                │
                                                ▼
                     Offset Calibration Passed?
                                                │
                        ┌───────────────┴───────────────┐
                        │                               │
                       NO                              YES
                        │                               │
                Run Offset First              Continue
                                                │
                                                ▼
                     Generator Ready?
                                                │
                        ┌───────────────┴───────────────┐
                        │                               │
                       NO                              YES
                        │                               │
                Verify Generator            Continue
                                                │
                                                ▼
                     Exposure Trigger OK?
                                                │
                        ┌───────────────┴───────────────┐
                        │                               │
                       NO                              YES
                        │                               │
                Check Trigger Signal         Continue
                                                │
                                                ▼
                    Image Acquired Correctly?
                                                │
                        ┌───────────────┴───────────────┐
                        │                               │
                       NO                              YES
                        │                               │
                Go to Image Tree            Continue
                                                │
                                                ▼
                  Gain File Generated?
                                                │
                        ┌───────────────┴───────────────┐
                        │                               │
                       YES                             NO
                        │                               │
                 Verify Gain File          Continue Investigation
```

---

# Quick Checklist

Verify the following before troubleshooting:

- □ Detector is Online.
- □ Offset calibration has completed successfully.
- □ Firmware version is supported.
- □ SDK version is compatible.
- □ Generator is powered on.
- □ Exposure parameters are correct.
- □ Trigger signal is normal.
- □ Detector temperature is within specification.

---

# Required Evidence

Collect before escalation:

- □ Detector Model
- □ Detector SN
- □ Firmware Version
- □ SDK Version
- □ Generator Model
- □ Exposure Parameters (kV / mA / ms)
- □ Trigger Mode
- □ Gain Calibration Log
- □ Calibration Screenshot

---

# Possible Root Causes

## Detector

- Detector status abnormal
- Gain acquisition interrupted

## Generator

- Exposure failure
- Incorrect exposure parameters
- Generator instability

## Trigger

- Trigger signal missing
- Trigger timing mismatch
- Synchronization failure

## Software

- SDK incompatibility
- Calibration configuration error

---

# Recommended Actions

Priority 1

- Verify Offset calibration.
- Verify generator operation.
- Verify exposure parameters.

Priority 2

- Verify trigger mode.
- Verify synchronization settings.

Priority 3

- Repeat Gain calibration.
- Compare with another generator if available.

Priority 4

- Collect logs and escalate if the problem persists.

---

# Escalation Criteria

Escalate when:

- Gain calibration repeatedly fails under verified exposure conditions.
- Multiple generators produce the same failure.
- Official calibration software also fails.
- Trigger and synchronization have been confirmed correct.
- Firmware and SDK compatibility have been verified.

---

# Related Documents

## Workflow

- [Calibration Workflow](../../06_Workflow/CalibrationWorkflow.md)

## Decision Trees

- [Offset Failure](OffsetFailure.md)
- [Version Mismatch](../Firmware/VersionMismatch.md)

## Case

- [Calibration Case Directory](../../11_Case/Calibration/)

## Tools

- [Calibration Tools](../../17_Tools/SDKTool/CalibrationTools.md)

## Failure Knowledge

- [Failure Analysis Method](../../07_FailureKnowledge/FailureAnalysisMethod.md)
- [Failure Classification](../../07_FailureKnowledge/FailureClassification.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Repaired obsolete Case, Tool, Reference and FailureKnowledge paths |
| v1.0 | 2026-08-06 | Initial release |