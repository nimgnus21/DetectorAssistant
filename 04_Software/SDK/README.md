# SDK

> iDetector SDK Module

---

# 1. Purpose

The **SDK** module provides configuration, management, and diagnostic functions related to the iDetector Software Development Kit (SDK).

This page allows engineers to verify the installed SDK, manage SDK-related settings, confirm compatibility, and perform basic SDK diagnostics.

Unlike the **02_SDK** module of DetectorAssistant, which documents SDK architecture and programming interfaces, this module focuses on the SDK-related functions exposed through the iDetector graphical user interface.

---

# 2. Scope

This module documents all functions available under the **SDK** page of the iDetector software.

Typical functions include:

- SDK information
- SDK version
- SDK status
- SDK configuration
- SDK diagnostics
- SDK compatibility

The descriptions in this module shall follow the corresponding iDetector software version.

---

# 3. Module Objectives

The SDK module enables engineers to:

- Verify the installed SDK
- Confirm SDK version
- Verify SDK operating status
- Check SDK compatibility
- Diagnose SDK-related problems
- Support software troubleshooting

---

# 4. Functional Overview

The SDK page provides management and diagnostic functions related to the detector SDK.

Typical functions include:

- SDK Information
- SDK Version
- SDK Status
- SDK Configuration
- SDK Diagnostic Information
- SDK Compatibility

The available functions may vary depending on the software version and SDK version.

---

# 5. Documentation Structure

The SDK module consists of documents describing each functional area of the SDK page.

Recommended documentation includes:

```text
SDK
│
├── README.md
├── SDKInformation.md
├── SDKVersion.md
├── SDKConfiguration.md
├── SDKStatus.md
├── SDKCompatibility.md
├── SDKDiagnosis.md
└── FAQ.md
```

Document names may be adjusted according to the actual iDetector interface.

---

# 6. Typical Engineering Workflow

Typical SDK verification workflow:

```text
Launch iDetector

↓

Open SDK Page

↓

Verify SDK Version

↓

Check SDK Status

↓

Verify Compatibility

↓

Configure SDK (if required)

↓

Complete Verification
```

---

# 7. Common Engineering Tasks

Typical engineering operations include:

- Confirming SDK version
- Checking SDK installation
- Verifying SDK compatibility
- Diagnosing SDK initialization issues
- Collecting SDK information
- Supporting software troubleshooting

---

# 8. Relationship with Other Modules

The SDK module works together with other software modules.

| Module | Relationship |
|----------|--------------|
| Detector | Provides detector communication |
| Acquire | Executes image acquisition |
| Calibrate | Performs calibration operations |
| Settings | Provides SDK-related configuration |
| Log | Records SDK events and diagnostic logs |

---

# 9. Related Knowledge Base Modules

The SDK page is closely related to the following DetectorAssistant modules.

| Knowledge Module | Purpose |
|------------------|---------|
| 02_SDK | SDK architecture and APIs |
| 06_Workflow | SDK operation workflow |
| 07_FailureKnowledge | SDK-related failures |
| 09_DecisionTree | SDK troubleshooting |
| 10_SOP | SDK operation procedures |
| 11_Case | SDK engineering cases |
| 12_ErrorCode | SDK-related error codes |
| 17_Tools | SDK engineering tools |

---

# 10. Documentation Principles

Each document within the SDK module should follow a consistent structure.

- Purpose
- Interface Location
- Functional Description
- Parameters
- Operating Procedure
- Notes
- Common Issues
- Related Documents
- Revision History

Descriptions should correspond to the actual iDetector interface and terminology.

---

# 11. Related Documents

### Software Module

- ../README.md
- ../Home/README.md
- ../Detector/README.md
- ../Acquire/README.md
- ../Calibrate/README.md
- ../Settings/README.md
- ../Upgrade/README.md
- ../Log/README.md

### Knowledge Base

- ../../02_SDK
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case
- ../../12_ErrorCode
- ../../17_Tools

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial SDK module documentation |