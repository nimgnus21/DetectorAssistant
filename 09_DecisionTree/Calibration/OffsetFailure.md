# Offset Generation Failed Decision Tree

> Module: Calibration
>
> Category: Decision Tree
>
> Version: v1.1
>
> Last Updated: 2026-08-10

---

# Symptom

Offset calibration cannot be completed successfully.

Typical symptoms include:

- Offset Generation Failed
- Offset Calibration Failed
- Offset file cannot be generated
- Calibration process interrupted
- Offset verification failed

---

# Diagnostic Flow

```
                Offset Generation Failed
                          │
                  Detector Connected?
                          │
              ┌───────────┴───────────┐
              │                       │
             NO                      YES
              │                       │
     Go to Connection Tree      Continue
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
                  Detector Ready Status?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
             Check Detector Status          Continue
                                              │
                                              ▼
                 Exposure Disabled?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
           Stop Generator Trigger          Continue
                                              │
                                              ▼
                  Previous Offset Exists?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     YES                             NO
                      │                               │
           Backup Existing File             Continue
                                              │
                                              ▼
                 Offset Generation Success?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     YES                             NO
                      │                               │
               Verify Offset File          Continue Investigation
```

---

# Quick Checklist

Before troubleshooting, verify:

- □ Detector is Online.
- □ Firmware version is supported.
- □ SDK version is compatible.
- □ Detector status is Ready.
- □ No X-ray exposure is active.
- □ Calibration environment is stable.
- □ Detector temperature is normal.
- □ Sufficient disk space is available.

---

# Required Evidence

Collect before escalation:

- □ Detector Model
- □ Detector Serial Number
- □ Firmware Version
- □ SDK Version
- □ Offset Log File
- □ Calibration Screenshot
- □ Detector Status Screenshot
- □ Calibration Configuration
- □ Error Message

---

# Possible Root Causes

## Detector

- Detector not ready
- Detector communication abnormal
- Detector internal status error

## Firmware

- Firmware version mismatch
- Calibration interface abnormal

## Environment

- Detector exposed during Offset
- Unstable power supply
- Detector temperature abnormal

## Software

- SDK incompatibility
- Calibration configuration error
- Insufficient storage permission

---

# Recommended Actions

Priority 1

- Verify detector communication.
- Verify detector Ready status.
- Ensure no exposure is active.

Priority 2

- Verify firmware compatibility.
- Verify SDK version.

Priority 3

- Restart detector.
- Retry Offset generation.

Priority 4

- Restore detector parameters if required.
- Escalate with collected logs.

---

# Escalation Criteria

Escalate when:

- Offset generation fails repeatedly.
- Official calibration tool also fails.
- Detector reports internal calibration error.
- Offset cannot be generated on multiple computers.
- Firmware and SDK have been verified compatible.

---

# Related Documents

## Workflow

- [Calibration Workflow](../../06_Workflow/CalibrationWorkflow.md)

## Decision Trees

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