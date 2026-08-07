# 04_Software

> iDetector Software Documentation

---

# 1. Purpose

This module documents the operation, configuration, maintenance, and troubleshooting of the **iDetector** software.

Unlike the SDK documentation (02_SDK), which focuses on software development interfaces, this module focuses on the graphical user interface (GUI) and operational workflow used by Field Application Engineers (FAEs), Technical Support Engineers, and end users.

The objective is to provide standardized guidance for software operation, parameter configuration, detector management, calibration, firmware upgrade, log collection, and troubleshooting.

---

# 2. Scope

This module covers all functional pages of the iDetector software.

Including:

- Home
- Detector
- Acquire
- Calibrate
- SDK
- Settings
- Upgrade
- Log

The documentation is organized according to the software navigation structure to match the actual user workflow.

---

# 3. Module Structure

```text
04_Software
│
├── README.md
│
├── Home
│
├── Detector
│
├── Acquire
│
├── Calibrate
│
├── SDK
│
├── Settings
│
├── Upgrade
│
└── Log
```

---

# 4. Module Overview

## Home

Provides the software entry page and overall system status.

Typical contents include:

- Software overview
- Detector status
- Shortcut functions
- Notification information

---

## Detector

Provides detector management functions.

Typical contents include:

- Detector discovery
- Detector information
- Connection status
- Detector configuration
- Device management

---

## Acquire

Provides image acquisition functions.

Typical contents include:

- Exposure
- Image acquisition
- Image preview
- Image storage
- Image export

---

## Calibrate

Provides detector calibration functions.

Typical contents include:

- Offset Calibration
- Gain Calibration
- Defect Calibration
- Dynamic Correction
- Calibration Result

---

## SDK

Provides SDK-related configuration and information.

Typical contents include:

- SDK version
- SDK configuration
- SDK compatibility
- SDK diagnostic information

---

## Settings

Provides software configuration.

Typical contents include:

- General settings
- Network settings
- Storage settings
- Display settings
- Language settings
- License settings

---

## Upgrade

Provides firmware upgrade functions.

Typical contents include:

- Firmware upgrade
- Version verification
- Upgrade process
- Upgrade recovery

---

## Log

Provides log management functions.

Typical contents include:

- Log collection
- Log export
- Log analysis
- Diagnostic information

---

# 5. Relationship with Other Modules

This module works together with other DetectorAssistant modules.

| Module | Relationship |
|---------|--------------|
| 02_SDK | Software uses SDK interfaces |
| 03_Hardware | Software manages detector hardware |
| 05_Calibration | Calibration theory and algorithms |
| 06_Workflow | Standard engineering workflows |
| 07_FailureKnowledge | Software-related failure analysis |
| 09_DecisionTree | Troubleshooting guidance |
| 10_SOP | Standard operating procedures |
| 11_Case | Engineering case studies |
| 12_ErrorCode | Error code interpretation |
| 17_Tools | Engineering support tools |

---

# 6. Documentation Principles

The Software module follows the actual navigation of the iDetector application.

Each software page should document:

- Purpose
- Interface location
- Functional description
- Parameters
- Operating procedure
- Notes
- Common issues
- Related documents

This ensures consistency with the user interface and improves engineering efficiency.

---

# 7. Intended Users

This module is intended for:

- Field Application Engineers (FAE)
- Technical Support Engineers
- Service Engineers
- R&D Engineers
- Quality Engineers
- Internal Trainers

---

# 8. Related Documents

- 02_SDK
- 03_Hardware
- 05_Calibration
- 06_Workflow
- 07_FailureKnowledge
- 09_DecisionTree
- 10_SOP
- 11_Case
- 12_ErrorCode
- 17_Tools

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Software module documentation |