# SDK Reference

> Version: v1.0
>
> Status: Draft
>
> Last Updated: 2026-08-06

---

# 1. Purpose

This document provides the reference relationship between the official SDK documentation and the DetectorAssistant knowledge base.

It does **not** duplicate SDK documentation.

Instead, it establishes a traceable mapping between SDK functions, workflows, troubleshooting guides, and internal knowledge documents.

---

# 2. Reference Principles

The official SDK documentation remains the primary technical authority.

DetectorAssistant provides:

- Engineering interpretation
- Field troubleshooting experience
- Workflow guidance
- Best practices
- FAQ
- Case studies

Whenever SDK documentation is updated, this reference document should be reviewed first to identify affected knowledge-base documents.

---

# 3. Official SDK Documents

| Document | Purpose | Priority |
|----------|----------|----------|
| SDK Programming Guide | SDK architecture and programming interface | High |
| SDK API Reference | Interface definition | High |
| SDK Release Notes | Version changes | High |
| SDK Sample Code | Development reference | Medium |
| SDK Demo Application | Functional verification | High |

---

# 4. Knowledge Mapping

## SDK Initialization

Official Reference

- SDK Programming Guide
- Initialization Chapter

Knowledge Base

- 17_Tools/SDKTool/README.md
- 06_Workflow/SoftwareInitializationWorkflow.md
- 11_Case/Communication/ConnectionFailed.md

---

## Detector Discovery

Official Reference

- Device Discovery

Knowledge Base

- 17_Tools/SDKTool/README.md
- 09_DecisionTree/Communication
- 11_Case/Communication

---

## Connection Management

Official Reference

- Device Connection

Knowledge Base

- ConnectionWorkflow
- ConnectionFailed
- Communication Decision Tree

---

## Mode Configuration

Official Reference

- Mode Configuration

Knowledge Base

- 17_Tools/SDKTool/ModeConfiguration.md
- ConfigurationWorkflow
- ConnectionFailed

---

## License Management

Official Reference

- License Interface

Knowledge Base

- LicenseManagement.md
- LicenseInvalid.md

---

## Firmware Upgrade

Official Reference

- Firmware Upgrade

Knowledge Base

- FirmwareUpgrade.md
- FirmwareUpgradeFailed.md
- VersionMismatch.md
- ParameterRecovery.md

---

## Calibration

Official Reference

- Offset Calibration
- Gain Calibration
- Ghost Correction

Knowledge Base

05_Calibration/

- Offset
- Gain
- Ghost

11_Case/

- OffsetGenerationFailed
- GainCalibrationFailed
- GhostCorrection

---

## Image Acquisition

Official Reference

- Image Acquisition Interface

Knowledge Base

- DTDITool.md
- Image Workflow
- Communication Case
- Image Diagnosis

---

## Error Handling

Official Reference

- SDK Error Code

Knowledge Base

- 12_ErrorCode/
- Communication Case
- DecisionTree

---

# 5. Version Compatibility

| SDK Version | Firmware | Detector | Status |
|-------------|----------|----------|--------|
| TBD | TBD | TBD | TBD |

This table should be maintained together with each SDK release.

---

# 6. Impact Analysis

Whenever the SDK is upgraded, review the following modules:

Priority 1

- SDK Tool
- Workflow
- Error Code

Priority 2

- Case
- Decision Tree

Priority 3

- Reply Template
- FAQ

---

# 7. Best Practice

When integrating a new SDK version:

1. Verify SDK version.
2. Verify firmware compatibility.
3. Verify detector model.
4. Verify Mode.ini.
5. Verify License.
6. Verify Demo Application.
7. Verify image acquisition.
8. Verify calibration.
9. Verify communication stability.

---

# 8. Related Documents

## SDK Tool

- 17_Tools/SDKTool/README.md
- DTDITool.md
- FirmwareUpgrade.md
- LicenseManagement.md
- ModeConfiguration.md

## Workflow

- ConfigurationWorkflow.md
- CalibrationWorkflow.md
- FirmwareUpgradeWorkflow.md

## Case

- Communication
- Firmware
- Calibration

## Decision Tree

- Communication
- Firmware
- Calibration

## Error Code

- 12_ErrorCode/

---

# 9. Maintenance Rules

This document should be updated when:

- A new SDK version is released.
- SDK interfaces are added or removed.
- SDK workflow changes.
- Compatibility requirements change.
- New SDK troubleshooting experience is accumulated.

This document serves as the entry point for SDK-related knowledge within DetectorAssistant.