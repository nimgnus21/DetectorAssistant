# API Error Decision Tree

> Module: Software
>
> Category: Decision Tree
>
> Version: v4.0
>
> Last Updated: 2026-08-06

---

# Purpose

This decision tree is used when an SDK API returns an error code or an unexpected return value.

Typical API sequence:

Application

↓

SDK Initialization

↓

Detector Discovery

↓

Open Detector

↓

Configure Parameters

↓

Acquire Image

↓

Receive Image

↓

Close Detector

↓

Release SDK

Failure at any API call should be isolated before continuing.

---

# Symptom

The SDK API returns an error code.

Typical symptoms include:

- API returns Error
- Function returns FALSE
- Return Code ≠ Success
- Invalid Handle
- Invalid Parameter
- Timeout
- Device Busy
- Unsupported Operation

---

# Symptom Classification

Identify the API failure category.

□ Initialization API

□ Discovery API

□ Open Device API

□ Configuration API

□ Acquisition API

□ Callback API

□ Close Device API

□ Unknown API Error

---

# API Execution Pipeline

```
Application
      │
      ▼
SDK API
      │
      ▼
Parameter Validation
      │
      ▼
Device Handle
      │
      ▼
Communication
      │
      ▼
Detector
      │
      ▼
Return Code
```

Verification Status

```
Application          □

SDK                  □

API Parameters       □

Handle               □

Communication        □

Detector             □

Return Code          □
```

---

# Diagnostic Flow

```
                  API Error
                      │
             SDK Initialized?
                      │
          ┌───────────┴───────────┐
          │                       │
         NO                      YES
          │                       │
SDKInitializationFailed     Continue
                                   │
                                   ▼
            Valid API Parameters?
                                   │
             ┌─────────────────────┴─────────────────────┐
             │                                           │
            NO                                          YES
             │                                           │
     Verify Parameters                         Continue
                                                 │
                                                 ▼
            Valid Detector Handle?
                                                 │
             ┌─────────────────────┴─────────────────────┐
             │                                           │
            NO                                          YES
             │                                           │
       Reopen Detector                         Continue
                                                 │
                                                 ▼
          Detector Ready?
                                                 │
             ┌─────────────────────┴─────────────────────┐
             │                                           │
            NO                                          YES
             │                                           │
      Detector Investigation                   Continue
                                                 │
                                                 ▼
        Communication Normal?
                                                 │
             ┌─────────────────────┴─────────────────────┐
             │                                           │
            NO                                          YES
             │                                           │
     Network Investigation                     Continue
                                                 │
                                                 ▼
         Error Reproducible?
                                                 │
             ┌─────────────────────┴─────────────────────┐
             │                                           │
            NO                                          YES
             │                                           │
 Application Logic                     SDK Investigation
```

---

# Error Classification

| Error Type | Possible Cause | Next Action |
|------------|----------------|-------------|
| Invalid Parameter | Incorrect API arguments | Verify parameters |
| Invalid Handle | Handle released or not opened | Reopen detector |
| Timeout | Acquisition timeout | AcquisitionTimeout.md |
| Device Busy | Detector occupied | DetectorBusy.md |
| Not Initialized | SDK not initialized | SDKInitializationFailed.md |
| Detector Not Found | No detector discovered | DetectorNotFound.md |
| Communication Error | Network failure | DetectorOffline.md |
| Unsupported Function | SDK / Firmware mismatch | VersionMismatch.md |

---

# Diagnosis Hint

API errors usually belong to one of the following categories:

1. API sequence error
2. Invalid parameters
3. Invalid detector handle
4. Communication failure
5. Detector state error
6. Firmware incompatibility
7. SDK internal exception

Always verify the API call sequence before suspecting hardware.

---

# Software Hint

Possible affected modules

★★★★★ SDK API

★★★★★ Application Logic

★★★★☆ Detector Handle

★★★★☆ Communication

★★★★☆ Firmware

★★★☆☆ Detector

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| SDK Demo | Verify API behavior | API Success |
| SDK Log | Check return codes | Error recorded |
| Debugger | Verify parameters | Correct values |
| Detector Utility | Verify detector state | Ready |
| Ping | Verify communication | Stable response |

---

# Expected Result

### API Call

Expected Result

- Return Code = Success.

---

### Detector Handle

Expected Result

- Handle is valid.
- Device opened successfully.

---

### Detector State

Expected Result

- Detector status = Ready.

---

### Communication

Expected Result

- Communication stable.
- No timeout.

---

# Quick Checklist

Verify

□ SDK initialized

□ API call sequence

□ Parameter values

□ Detector handle

□ Detector Ready

□ Firmware version

□ SDK version

□ Error code

□ SDK log

---

# Required Evidence

Collect before escalation

- Detector Model
- Detector SN
- SDK Version
- Firmware Version
- API Name
- API Return Code
- SDK Log
- Application Log
- Error Screenshot
- Source Code Snippet (optional)

---

# Possible Root Causes

## API

- Incorrect API sequence
- Invalid parameters
- Unsupported function

---

## SDK

- SDK version mismatch
- Internal SDK error

---

## Detector

- Detector not ready
- Detector disconnected

---

## Communication

- Network interruption
- Packet loss

---

## Firmware

- Firmware incompatible
- Unsupported protocol

---

# Recommended Actions

Priority 1

- Verify API call sequence.

Priority 2

- Verify parameters and detector handle.

Priority 3

- Verify detector state and communication.

Priority 4

- Verify firmware and SDK compatibility.

Priority 5

- Reproduce using SDK Demo.

Priority 6

- Escalate with complete logs and error code.

---

# Escalation Criteria

Escalate when:

- The error is reproducible.
- SDK Demo reproduces the same error.
- Parameters and API sequence are confirmed correct.
- Firmware compatibility has been verified.
- The issue cannot be explained by application logic.

---

# Related Documents

## Software

- 09_DecisionTree/Software/SDKInitializationFailed.md
- 09_DecisionTree/Software/DetectorNotFound.md
- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Software/SDKException.md

## Connection

- 09_DecisionTree/Connection/DetectorOffline.md

## Firmware

- 09_DecisionTree/Firmware/VersionMismatch.md

## Reference

- 15_Reference/SDKReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v4.0 | 2026-08-06 | Initial release |