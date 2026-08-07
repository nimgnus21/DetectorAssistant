# SDK Error Code

> Module: SDK
>
> Category: Error Code Reference

---

# Overview

This module provides a categorized reference for all SDK-related error codes defined in the SDK Programming Reference.

The purpose of this module is to help FAE engineers, software engineers, and technical support personnel quickly understand the meaning of SDK error codes, identify possible causes, and locate related troubleshooting documents.

This module does not replace the SDK Programming Guide. Instead, it serves as an engineering-oriented troubleshooting reference within the DetectorAssistant knowledge base.

---

# Scope

This document applies to:

- Detector SDK
- Detector communication
- Detector initialization
- Image acquisition
- Image transmission
- Detector status management
- License-related operations

---

# Document Structure

```
SDK
├── README.md
├── Initialization.md
├── Network.md
├── Device.md
├── Acquisition.md
├── Image.md
└── License.md
```

---

# Category Description

## Initialization

Initialization-related errors occurring before normal detector operation.

Typical topics include:

- SDK initialization
- Detector object creation
- Runtime state
- Parameter validation
- Command preconditions

---

## Network

Detector communication and network connection errors.

Typical topics include:

- Detector connection
- Socket communication
- Network timeout
- Communication device
- Network configuration

---

## Device

Detector hardware and firmware execution errors.

Typical topics include:

- Detector status
- Detector identification
- Product information
- Firmware response
- Detector internal storage
- Hardware calibration files

---

## Acquisition

Errors occurring during image acquisition.

Typical topics include:

- Task timeout
- Frame loss
- Packet loss
- Buffer overflow
- Acquisition interruption

---

## Image

Errors related to image transmission and image quality.

Typical topics include:

- Image channel interruption
- Image quality
- Callback processing
- Image timeout

---

## License

Errors related to SDK authorization and licensed features.

Current SDK versions do not define dedicated license error codes.

This document summarizes authorization-related troubleshooting based on existing SDK error codes and field experience.

---

# Error Handling Workflow

When an SDK error occurs, follow the recommended troubleshooting sequence:

```
Error Code

↓

Locate the corresponding document

↓

Read Description

↓

Analyze Possible Causes

↓

Perform Recommended Actions

↓

Open Related DecisionTree

↓

Reference Related Case

↓

Resolve or Escalate
```

---

# Related Modules

## DecisionTree

Used to locate the fault systematically.

```
09_DecisionTree
```

---

## FailureKnowledge

Explains the technical principles behind failures.

```
07_FailureKnowledge
```

---

## Case

Provides real-world troubleshooting examples.

```
11_Case
```

---

## Workflow

Provides standard operating procedures.

```
06_Workflow
```

---

## Calibration

Provides calibration principles and template generation workflows.

```
05_Calibration
```

---

# Log File

The SDK runtime log is generated automatically in the detector working directory.

```
Detector.log
```

The log should always be collected together with:

- SDK Version
- Detector Firmware Version
- Detector Serial Number
- Configuration Files
- Error Code
- Reproduction Procedure

---

# Applicable Events

Most SDK error codes are returned through the following events:

- Evt_GeneralError
- Evt_GeneralWarn
- Evt_TaskResult_Failed
- Evt_TransactionAborted

For task failures:

- nParam1 = Command ID
- nParam2 = Error Code

---

# Applicable Commands

Error codes may be generated during execution of commands such as:

- Cmd_Connect
- Cmd_Disconnect
- Cmd_Reset
- Cmd_StartAcq
- Cmd_StopAcq
- Cmd_ClearAcq
- Cmd_UpdateFirmware
- Cmd_OffsetGeneration
- Cmd_GainGeneration
- Cmd_DefectGeneration

---

# Troubleshooting Recommendations

When analyzing SDK-related errors:

1. Record the complete error code.
2. Record the command that generated the error.
3. Check Detector.log.
4. Verify detector status.
5. Verify firmware version.
6. Verify SDK version.
7. Check the corresponding DecisionTree.
8. Review related troubleshooting cases before escalation.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |