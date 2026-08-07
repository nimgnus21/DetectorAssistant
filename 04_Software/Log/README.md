# Log

> iDetector Log Management Module

---

# 1. Purpose

The **Log** module provides log management and diagnostic information collection functions within the iDetector software.

It enables engineers to collect, export, and analyze software and detector logs for troubleshooting, technical support, quality analysis, and communication with R&D teams.

Log information is one of the primary sources for diagnosing communication failures, acquisition abnormalities, calibration failures, firmware upgrade issues, and unexpected software behavior.

---

# 2. Scope

This module documents all functions available under the **Log** page of the iDetector software.

Typical functions include:

- Log Collection
- Log Viewing
- Log Export
- Diagnostic Information
- System Information
- Software Information
- Detector Log Management

The descriptions in this module shall follow the corresponding iDetector software version.

---

# 3. Module Objectives

The Log module enables engineers to:

- Collect diagnostic logs
- View software logs
- Export log packages
- Verify software operation records
- Collect detector diagnostic information
- Support remote troubleshooting
- Provide log evidence for R&D analysis

---

# 4. Functional Overview

The Log page provides centralized log collection and management functions.

Typical functions include:

- Software Log
- Detector Log
- SDK Log
- Communication Log
- Export Log
- Diagnostic Information
- System Information
- Log Package Generation

Available functions may vary depending on the software version, detector model, SDK version, and user permissions.

---

# 5. Documentation Structure

The Log module consists of documents describing each functional area of the Log page.

Recommended documentation includes:

```text
Log
│
├── README.md
├── SoftwareLog.md
├── DetectorLog.md
├── SDKLog.md
├── CommunicationLog.md
├── ExportLog.md
├── DiagnosticInformation.md
├── LogPackage.md
└── FAQ.md
```

Document names may be adjusted according to the actual iDetector interface.

---

# 6. Typical Engineering Workflow

Typical log collection workflow:

```text
Launch iDetector

↓

Reproduce the Issue

↓

Open Log Page

↓

Select Log Type

↓

Collect Diagnostic Information

↓

Export Log Package

↓

Verify Export Result

↓

Provide Logs to Technical Support or R&D
```

---

# 7. Common Engineering Tasks

Typical engineering operations include:

- Collecting software logs
- Exporting detector logs
- Collecting SDK logs
- Exporting communication logs
- Packaging diagnostic information
- Verifying software operation history
- Supporting remote troubleshooting
- Providing evidence for failure analysis

---

# 8. Relationship with Other Modules

The Log module supports all major software modules.

| Module | Relationship |
|----------|--------------|
| Home | Records software operation events |
| Detector | Records detector communication events |
| Acquire | Records acquisition operations |
| Calibrate | Records calibration processes |
| SDK | Records SDK events |
| Settings | Records configuration changes |
| Upgrade | Records firmware upgrade activities |

---

# 9. Related Knowledge Base Modules

The Log page is closely related to the following DetectorAssistant modules.

| Knowledge Module | Purpose |
|------------------|---------|
| 02_SDK | SDK logging and diagnostics |
| 06_Workflow | Log collection workflow |
| 07_FailureKnowledge | Failure diagnosis |
| 09_DecisionTree | Troubleshooting procedures |
| 10_SOP | Log collection procedures |
| 11_Case | Engineering case analysis |
| 12_ErrorCode | Error code interpretation |
| 17_Tools | Diagnostic and support tools |

---

# 10. Documentation Principles

Each document within the Log module should follow a consistent structure.

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

# 11. Engineering Recommendations

During technical support, engineers are recommended to:

- Collect logs immediately after reproducing the issue.
- Preserve the original log files without modification.
- Export complete log packages whenever possible.
- Record the detector model, firmware version, SDK version, and software version together with the logs.
- Attach screenshots or images that correspond to the logged event.
- Store exported logs in the project archive for future reference.

---

# 12. Related Documents

### Software Module

- ../README.md
- ../Home/README.md
- ../Detector/README.md
- ../Acquire/README.md
- ../Calibrate/README.md
- ../SDK/README.md
- ../Settings/README.md
- ../Upgrade/README.md

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
| v1.0 | 2026-08-07 | Initial Log module documentation |