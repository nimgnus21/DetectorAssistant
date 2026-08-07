# SDK Initialization Failed Decision Tree

> Module: Software
>
> Category: Master Decision Tree
>
> Version: v4.0
>
> Last Updated: 2026-08-06

---

# Purpose

This decision tree is the primary entry point for all SDK initialization failures.

Typical initialization sequence:

Application

↓

Load SDK Library

↓

Initialize SDK

↓

Enumerate Detector

↓

Open Detector

↓

Read Detector Information

↓

Configure Detector

↓

Detector Ready

↓

Start Acquisition

Failure at any stage should be isolated before proceeding.

---

# Symptom

The SDK cannot be initialized successfully.

Typical symptoms include:

- SDK initialization failed
- SDK Init Failed
- Failed to load SDK
- SDK returns initialization error
- Detector cannot be opened
- No detector detected
- SDK crashes during initialization

---

# Symptom Classification

Identify the observed behavior.

□ DLL Load Failed

□ SDK Init Failed

□ Detector Not Found

□ Detector Open Failed

□ Read Information Failed

□ Detector Busy

□ Timeout

□ Unknown Error Code

---

# Software Initialization Pipeline

```
Application
      │
      ▼
SDK DLL
      │
      ▼
SDK Runtime
      │
      ▼
Driver
      │
      ▼
Communication
      │
      ▼
Detector
      │
      ▼
Firmware
      │
      ▼
Ready
```

Verification Status

```
Application        □

DLL                □

Runtime            □

Driver             □

Network            □

Detector           □

Firmware           □

Ready              □
```

---

# Diagnostic Flow

```
              SDK Initialization Failed
                        │
                DLL Loaded Successfully?
                        │
          ┌─────────────┴─────────────┐
          │                           │
         NO                          YES
          │                           │
Check DLL Installation         Continue
                                      │
                                      ▼
                SDK Init Success?
                                      │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
          SDK Environment                         Continue
                                                   │
                                                   ▼
               Detector Detected?
                                                   │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
         DetectorNotFound.md                     Continue
                                                   │
                                                   ▼
               Detector Open Success?
                                                   │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
          Detector Busy / Network                Continue
                                                   │
                                                   ▼
         Read Detector Information Success?
                                                   │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
           Firmware Investigation                 Continue
                                                   │
                                                   ▼
               Detector Ready?
                                                   │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
        Initialization Failure                  Initialization Complete
```

---

# Diagnosis Hint

SDK initialization problems are usually caused by one of the following layers:

1. SDK installation
2. Runtime environment
3. Driver
4. Network communication
5. Detector discovery
6. Firmware compatibility
7. Detector state

Always isolate software problems before investigating hardware.

---

# Software Hint

Most likely affected modules

★★★★★ SDK Runtime

★★★★★ DLL

★★★★★ Driver

★★★★☆ Network

★★★★☆ Firmware

★★★☆☆ Detector

★★☆☆☆ Application

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| SDK Demo | Verify SDK operation | SDK initializes successfully |
| Dependency Walker | Verify DLL dependencies | No missing DLLs |
| Device Manager | Verify driver | Driver installed correctly |
| Ping | Verify detector communication | Stable response |
| Detector Utility | Read detector information | Detector identified |
| Firmware Tool | Read firmware version | Version displayed |

---

# Expected Result

### DLL

Expected Result

- SDK DLL loaded successfully.
- No dependency errors.

---

### SDK

Expected Result

- SDK initialization returns Success.

---

### Detector

Expected Result

- Detector is detected.
- Detector can be opened.

---

### Firmware

Expected Result

- Firmware version successfully read.
- Version compatible with SDK.

---

### Ready

Expected Result

- Detector status = Ready.

---

# Quick Checklist

Verify

□ SDK Version

□ DLL Exists

□ DLL Dependency

□ Driver Installed

□ Detector Online

□ Network Connected

□ Firmware Version

□ SDK Demo Tested

---

# Required Evidence

Collect before escalation

- SDK Version
- DLL Version
- Driver Version
- Firmware Version
- Detector Model
- Detector SN
- SDK Log
- Application Log
- Detector Status
- Error Code
- Error Screenshot

---

# Possible Root Causes

## SDK

- SDK installation incomplete
- Incorrect SDK version
- Missing runtime libraries

---

## Driver

- Driver not installed
- Driver corrupted

---

## Network

- Detector unreachable
- IP configuration incorrect

---

## Firmware

- Firmware incompatible
- Firmware initialization failure

---

## Detector

- Detector busy
- Detector offline

---

## Application

- Incorrect API sequence
- Unsupported SDK version

---

# Recommended Actions

Priority 1

- Verify SDK installation.
- Verify SDK Demo.

Priority 2

- Verify DLL dependencies.
- Verify driver installation.

Priority 3

- Verify detector communication.
- Verify firmware compatibility.

Priority 4

- Compare with another PC if available.

Priority 5

- Escalate if initialization still fails.

---

# Escalation Criteria

Escalate when:

- SDK Demo also fails.
- DLL and driver have been verified.
- Detector communication is normal.
- Firmware version is compatible.
- Initialization consistently fails across multiple systems.

---

# Related Documents

## Software

- 09_DecisionTree/Software/DetectorNotFound.md
- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Software/SDKException.md
- 09_DecisionTree/Software/APIError.md

## Firmware

- 09_DecisionTree/Firmware/VersionMismatch.md

## Connection

- 09_DecisionTree/Connection/DetectorOffline.md

## Reference

- 15_Reference/SDKReference.md

## Tools

- 17_Tools/SDKDemo.md
- 17_Tools/FirmwareTool.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v4.0 | 2026-08-06 | Initial Master Decision Tree |