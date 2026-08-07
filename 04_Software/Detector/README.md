# Detector

> iDetector Detector Module

---

# 1. Purpose

The **Detector** module is responsible for detector discovery, connection, management, configuration, and status monitoring within the iDetector software.

It provides the interface for establishing communication between the host computer and the detector, displaying detector information, configuring device parameters, and monitoring operating status.

This module serves as the primary management interface for all supported detectors.

---

# 2. Scope

This module documents all functions available under the **Detector** page of the iDetector software.

Typical topics include:

- Detector discovery
- Detector connection
- Detector information
- Detector status
- Detector configuration
- Detector management
- Communication status

The descriptions in this module should follow the corresponding iDetector software version.

---

# 3. Module Objectives

The Detector module enables engineers to:

- Detect available detectors
- Establish communication with a detector
- Verify detector identity
- Monitor detector operating status
- Configure detector parameters
- Manage detector information
- Diagnose basic communication problems

---

# 4. Functional Overview

The Detector page provides centralized management of detector devices.

Typical functions include:

- Detector List
- Detector Information
- Connection Management
- Detector Status
- Network Information
- Device Configuration
- Detector Control

The available functions may vary depending on the software version, detector model, and user permissions.

---

# 5. Documentation Structure

The Detector module consists of documents describing each functional area of the Detector page.

Recommended documentation includes:

```text
Detector
│
├── README.md
├── DetectorList.md
├── DetectorInformation.md
├── DetectorConnection.md
├── DetectorStatus.md
├── NetworkConfiguration.md
├── DetectorConfiguration.md
├── DetectorActivation.md
└── FAQ.md
```

Document names may be adjusted to match the actual function names used in the corresponding iDetector version.

---

# 6. Typical Engineering Workflow

Typical detector management workflow:

```text
Launch iDetector

↓

Open Detector Page

↓

Search Detector

↓

Select Detector

↓

Establish Connection

↓

Verify Detector Information

↓

Check Detector Status

↓

Configure Parameters (if required)

↓

Ready for Image Acquisition
```

---

# 7. Common Engineering Tasks

Typical engineering operations include:

- Connecting a new detector
- Reconnecting an offline detector
- Verifying detector information
- Checking communication status
- Confirming firmware version
- Confirming detector serial number
- Configuring detector parameters
- Verifying detector readiness

---

# 8. Relationship with Other Modules

The Detector module interacts with multiple software modules.

| Module | Relationship |
|----------|--------------|
| Home | Displays detector summary information |
| Acquire | Uses the connected detector for image acquisition |
| Calibrate | Performs detector calibration |
| SDK | Uses SDK services for detector communication |
| Settings | Applies detector-related configuration |
| Upgrade | Updates detector firmware |
| Log | Records detector operation logs |

---

# 9. Related Knowledge Base Modules

The Detector page is closely related to the following DetectorAssistant modules.

| Knowledge Module | Purpose |
|------------------|---------|
| 02_SDK | Detector communication interfaces |
| 03_Hardware | Detector hardware architecture |
| 05_Calibration | Detector calibration principles |
| 06_Workflow | Detector operation workflow |
| 07_FailureKnowledge | Detector-related failures |
| 09_DecisionTree | Detector troubleshooting |
| 10_SOP | Standard operating procedures |
| 11_Case | Engineering case studies |
| 12_ErrorCode | Detector error interpretation |
| 17_Tools | Engineering support tools |

---

# 10. Documentation Principles

Each document within the Detector module should follow a consistent structure.

- Purpose
- Interface Location
- Functional Description
- Parameters
- Operating Procedure
- Notes
- Common Issues
- Related Documents
- Revision History

The descriptions should correspond to the actual iDetector interface and terminology.

---

# 11. Related Documents

### Software Module

- ../README.md
- ../Home/README.md
- ../Acquire/README.md
- ../Calibrate/README.md
- ../SDK/README.md
- ../Settings/README.md
- ../Upgrade/README.md
- ../Log/README.md

### Knowledge Base

- ../../02_SDK
- ../../03_Hardware
- ../../05_Calibration
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case
- ../../12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Detector module documentation |