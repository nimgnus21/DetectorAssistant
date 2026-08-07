# Detector Busy Decision Tree

> Module: Software
>
> Category: Decision Tree
>
> Version: v4.0
>
> Last Updated: 2026-08-06

---

# Purpose

This decision tree is used when the detector cannot execute a requested operation because it is currently occupied, locked, or has not completed a previous operation.

Typical operation sequence:

Initialize SDK

↓

Open Detector

↓

Configure Detector

↓

Start Acquisition

↓

Receive Image

↓

Stop Acquisition

↓

Close Detector

↓

Release Resources

If any operation does not complete correctly, the detector may remain in a busy state.

---

# Symptom

The SDK reports that the detector is busy and rejects further operations.

Typical symptoms include:

- Detector Busy
- Device Busy
- Resource Busy
- Device Already Opened
- Detector Occupied
- Operation Rejected
- Previous Acquisition Running
- Open Detector Failed (Busy)

---

# Symptom Classification

Identify the observed behavior.

□ Busy immediately after startup

□ Busy after acquisition

□ Busy after application crash

□ Busy after timeout

□ Busy after calibration

□ Busy after firmware upgrade

□ Busy only on one PC

□ Busy on multiple PCs

---

# Detector State Pipeline

```
Application
      │
      ▼
SDK
      │
      ▼
Detector Handle
      │
      ▼
Acquisition Task
      │
      ▼
Detector Internal State
      │
      ▼
Ready
```

Verification Status

```
Application      □

SDK              □

Handle           □

Acquisition      □

Detector State   □

Ready            □
```

---

# Diagnostic Flow

```
                 Detector Busy
                       │
             SDK Initialized?
                       │
        ┌──────────────┴──────────────┐
        │                             │
       NO                            YES
        │                             │
SDKInitializationFailed        Continue
                                      │
                                      ▼
           Detector Already Open?
                                      │
        ┌──────────────┴──────────────┐
        │                             │
       YES                           NO
        │                             │
Close Existing Handle         Continue
                                      │
                                      ▼
        Previous Acquisition Finished?
                                      │
        ┌──────────────┴──────────────┐
        │                             │
       NO                            YES
        │                             │
Stop Acquisition             Continue
                                      │
                                      ▼
       Application Crashed Earlier?
                                      │
        ┌──────────────┴──────────────┐
        │                             │
       YES                           NO
        │                             │
Restart Detector              Continue
                                      │
                                      ▼
     Another Application Running?
                                      │
        ┌──────────────┴──────────────┐
        │                             │
       YES                           NO
        │                             │
Close Other Software         Continue
                                      │
                                      ▼
         Detector Status Ready?
                                      │
        ┌──────────────┴──────────────┐
        │                             │
       NO                            YES
        │                             │
Firmware / Hardware           Application Logic
```

---

# Busy State Classification

| Busy Condition | Possible Cause | Next Action |
|----------------|----------------|-------------|
| Device Already Open | Existing handle | Close detector |
| Acquisition Running | Previous acquisition not stopped | Stop acquisition |
| Calibration Running | Calibration not finished | Wait or cancel |
| Firmware Updating | Upgrade in progress | Wait for completion |
| Application Crash | Handle not released | Restart detector |
| Multiple Applications | Resource conflict | Close other applications |
| Unknown Busy | Internal detector state | Restart detector |

---

# Diagnosis Hint

Detector Busy is usually **not a hardware fault**.

Most cases are caused by:

1. Detector handle not released.
2. Previous acquisition still active.
3. Multiple applications using the detector.
4. Callback not completed.
5. Detector still processing a previous command.
6. Firmware still executing an operation.

Always verify software state before replacing hardware.

---

# Software Hint

Most likely affected modules

★★★★★ SDK Handle Management

★★★★★ Acquisition Control

★★★★★ Multi-Application Access

★★★★☆ Callback Processing

★★★★☆ Detector State Machine

★★★☆☆ Firmware

★★☆☆☆ Hardware

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| SDK Demo | Verify detector status | Detector Ready |
| Detector Utility | Read detector state | Ready |
| Task Manager | Check running applications | Only one application |
| SDK Log | Verify acquisition sequence | Complete Stop/Close |
| Detector Log | Verify detector state | No busy status |

---

# Expected Result

### Detector Handle

Expected Result

- Only one valid detector handle exists.

---

### Acquisition

Expected Result

- Previous acquisition completed successfully.

---

### Detector State

Expected Result

- Detector reports **Ready**.

---

### Application

Expected Result

- No duplicate detector access.

---

# Quick Checklist

Verify

□ SDK initialized

□ Detector opened once

□ Previous acquisition stopped

□ Detector closed correctly

□ Callback completed

□ SDK Demo tested

□ Detector Utility tested

□ No duplicate application

□ Detector Ready

---

# Required Evidence

Collect before escalation

- Detector Model

- Detector SN

- SDK Version

- Firmware Version

- Detector State Screenshot

- SDK Log

- Detector Log

- Error Code

- Running Process List

- Reproduction Steps

---

# Possible Root Causes

## Application

- Detector opened twice
- Handle not released
- Acquisition not stopped
- Callback blocked

---

## SDK

- Handle management abnormal
- Resource cleanup failure

---

## Detector

- Internal busy state
- Processing previous task

---

## Firmware

- Calibration running
- Firmware update incomplete
- Detector initialization incomplete

---

## Operating System

- Multiple SDK applications
- Process not terminated
- Driver resource occupied

---

# Recommended Actions

Priority 1

- Close all detector-related applications.

Priority 2

- Verify detector handle management.

Priority 3

- Stop current acquisition before reopening.

Priority 4

- Restart detector and reconnect.

Priority 5

- Verify with SDK Demo.

Priority 6

- Escalate if the detector remains busy after restart.

---

# Escalation Criteria

Escalate when:

- Detector remains busy after reboot.
- SDK Demo reports the same busy state.
- Only one application is running.
- Detector state cannot return to **Ready**.
- Firmware and SDK versions are verified.

---

# Related Documents

## Software

- 09_DecisionTree/Software/SDKInitializationFailed.md
- 09_DecisionTree/Software/DetectorNotFound.md
- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Software/APIError.md
- 09_DecisionTree/Software/SDKException.md

## Connection

- 09_DecisionTree/Connection/DetectorOffline.md

## Firmware

- 09_DecisionTree/Firmware/VersionMismatch.md

## Reference

- 15_Reference/SDKReference.md

## Tools

- 17_Tools/SDKDemo.md
- 17_Tools/DetectorUtility.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v4.0 | 2026-08-06 | Initial release |