# Error Code

> DetectorAssistant Error Code Knowledge Base

---

# Overview

The ErrorCode module provides a structured reference for all detector-related error codes encountered during installation, configuration, calibration, firmware upgrade, communication, image acquisition, and routine operation.

Rather than listing SDK error codes individually, this module groups related errors by functional area to support efficient troubleshooting and field service.

---

# Scope

This module covers:

- SDK Runtime
- Detector Communication
- Firmware
- Calibration
- Generator Interaction

---

# Directory Structure

```text
12_ErrorCode
├── README.md
├── SDK
│   ├── README.md
│   ├── Initialization.md
│   ├── Acquisition.md
│   ├── Device.md
│   ├── Image.md
│   └── License.md
│
├── Communication
│   ├── README.md
│   ├── Ethernet.md
│   ├── Network.md
│   ├── Packet.md
│   └── Timeout.md
│
├── Firmware
│   ├── README.md
│   ├── Boot.md
│   ├── EEPROM.md
│   └── Upgrade.md
│
├── Calibration
│   ├── README.md
│   ├── Offset.md
│   ├── Gain.md
│   └── Defect.md
│
└── Generator
    ├── README.md
    ├── Communication.md
    ├── Exposure.md
    ├── Trigger.md
    ├── Interlock.md
    └── Configuration.md
```

---

# Module Description

## SDK

Runtime errors reported directly by the SDK, including initialization, image acquisition, device management, image processing, and license-related issues.

---

## Communication

Errors related to Ethernet communication, network configuration, packet transmission, and communication timeout between the detector and host computer.

---

## Firmware

Detector firmware startup, upgrade, rollback, and persistent parameter storage.

---

## Calibration

Errors encountered during Offset, Gain, and Defect calibration, including template generation and hardware calibration.

---

## Generator

Failures caused by generator communication, exposure control, trigger synchronization, safety interlock, and configuration mismatch.

---

# Troubleshooting Workflow

```text
Observe Symptom

↓

Identify Error Code

↓

Locate Module

↓

Review Error Description

↓

Follow Diagnostic Procedure

↓

Check Detector.log

↓

Refer to DecisionTree

↓

Resolve or Escalate
```

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

## Log

```text
Detector.log
```

---

# Recommended Usage

When an error occurs:

1. Record the exact error code or event.
2. Locate the corresponding category in this module.
3. Review the documented causes and recommended actions.
4. Cross-reference the related DecisionTree, Workflow, and Case documents.
5. Collect Detector.log and supporting information before escalation.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |