# Template

> DetectorAssistant Template Library

---

# Overview

The Template module provides standardized documents used by Field Application Engineers (FAEs) during daily technical support, installation, troubleshooting, remote assistance, firmware upgrades, calibration, and Return Material Authorization (RMA).

Unlike the **Workflow** module, which focuses on operational procedures, or the **Case** module, which records troubleshooting examples, this module provides reusable templates that can be directly applied during engineering work.

The objective is to standardize communication, improve troubleshooting efficiency, and reduce repetitive work.

---

# Module Structure

```text
13_Template
│
├── README.md
│
├── Communication
│   ├── CustomerReply.md
│   ├── InternalReply.md
│   ├── EmailTemplate.md
│   └── ChatTemplate.md
│
└── Work
    ├── Checklist.md
    ├── LogCollection.md
    ├── Calibration.md
    ├── FirmwareUpgrade.md
    ├── RemoteSupport.md
    └── RMA.md
```

---

# Communication Templates

## CustomerReply

Standard customer response templates.

Typical scenarios:

- Connection issues
- Image abnormalities
- Calibration problems
- Firmware issues
- License issues
- Information requests

---

## InternalReply

Templates for communication with:

- R&D
- Quality Assurance
- Production
- Distributors
- Technical Support Teams

---

## EmailTemplate

Formal email templates.

Typical scenarios:

- Technical support
- Firmware delivery
- Upgrade notification
- RMA confirmation
- Case closure

---

## ChatTemplate

Instant messaging templates.

Applicable to:

- Microsoft Teams
- WeChat
- DingTalk
- Slack
- KakaoTalk
- WhatsApp

---

# Work Templates

## Checklist

Standard engineering checklists.

Includes:

- Installation
- Connection
- Exposure
- Calibration
- Image Quality
- Firmware Upgrade
- OQC
- Remote Support
- RMA

---

## LogCollection

Defines the standard information required for troubleshooting.

Includes:

- Detector.log
- SDK Version
- Firmware Version
- Detector SN
- Images
- Network Information
- Error Information

---

## Calibration

Standard templates for calibration activities.

Includes:

- Offset
- Gain
- Defect
- Hardware Calibration
- Verification
- Troubleshooting

---

## FirmwareUpgrade

Standard firmware upgrade templates.

Includes:

- Upgrade preparation
- Upgrade execution
- Upgrade verification
- Failure collection
- Recovery checklist

---

## RemoteSupport

Templates for remote technical support.

Includes:

- Meeting preparation
- Information collection
- Troubleshooting workflow
- Remote support records
- Case closure

---

## RMA

Templates for detector return and repair.

Includes:

- RMA application
- Information collection
- Receiving inspection
- Repair records
- Final verification
- Return confirmation

---

# Recommended Workflow

A typical troubleshooting process is shown below.

```text
Customer Reports Issue

        │
        ▼

CustomerReply / ChatTemplate

        │
        ▼

LogCollection

        │
        ▼

09_DecisionTree

        │
        ▼

12_ErrorCode

        │
        ▼

11_Case

        │
        ▼

Calibration / FirmwareUpgrade /
RemoteSupport (if required)

        │
        ▼

InternalReply

        │
        ▼

EmailTemplate

        │
        ▼

Issue Resolved

        │
        ▼

RMA (if required)
```

---

# Related Modules

| Module | Description |
|---------|-------------|
| 05_Calibration | Calibration principles and technical documentation |
| 06_Workflow | Standard operating workflows |
| 07_FailureKnowledge | Failure mechanisms and analysis |
| 09_DecisionTree | Troubleshooting decision trees |
| 11_Case | Real-world troubleshooting cases |
| 12_ErrorCode | Error code reference |

---

# Engineering Principles

When using templates:

- Use the simplest template that satisfies the current task.
- Avoid requesting duplicate information.
- Always collect Detector.log whenever possible.
- Preserve original images and screenshots.
- Update the knowledge base after resolving new field issues.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |