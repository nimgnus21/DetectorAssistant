# Standard Operating Procedures (SOP)

> DetectorAssistant Standard Operating Procedures

---

# Overview

The SOP module defines standardized operational procedures for Field Application Engineers (FAEs), Technical Support Engineers, Production Engineers, and Quality Engineers.

Unlike other modules that explain principles, troubleshooting logic, or product knowledge, this module focuses on **how to perform tasks correctly, consistently, safely, and efficiently**.

Each SOP provides a step-by-step operational guide based on actual engineering workflows and references the corresponding knowledge modules where detailed technical explanations are available.

---

# Objectives

The SOP module aims to:

- Standardize engineering operations.
- Reduce human error.
- Improve troubleshooting efficiency.
- Ensure operation consistency.
- Shorten engineer training time.
- Preserve field engineering experience.

---

# Applicable Scope

This SOP library applies to:

- Detector Installation
- Network Configuration
- Detector Calibration
- Firmware Upgrade
- Image Troubleshooting
- Remote Technical Support
- Detector Replacement
- Preventive Maintenance
- RMA Processing

Applicable personnel:

- Field Application Engineer (FAE)
- Technical Support Engineer
- Production Engineer
- Quality Engineer
- R&D Engineer (Reference)

---

# SOP Writing Principles

All SOP documents follow the same structure to ensure consistency throughout the knowledge base.

Each SOP shall contain the following sections:

1. Scope
2. Objective
3. Responsibility
4. Preconditions
5. Required Tools
6. Required Files
7. Safety Precautions
8. Procedure
9. Decision Points
10. Expected Results
11. Exception Handling
12. Records
13. Related Documents

---

# Standard Workflow Format

Every operational step should follow the format below.

```text
Input

↓

Process

↓

Output

↓

Acceptance Criteria

↓

Exception Handling
```

Each step should describe only one action.

Use measurable descriptions whenever possible.

Avoid combining multiple operations into a single step.

---

# General SOP Workflow

```text
Preparation

↓

Environment Check

↓

Detector Check

↓

Software Preparation

↓

Operation Execution

↓

Verification

↓

Troubleshooting (if required)

↓

Completion

↓

Record Keeping
```

---

# Document Structure

```text
10_SOP
│
├── README.md
├── DetectorInstallation.md
├── NetworkConfiguration.md
├── Calibration.md
├── FirmwareUpgrade.md
├── ImageTroubleshooting.md
├── RemoteSupport.md
├── DetectorReplacement.md
├── PreventiveMaintenance.md
└── RMA.md
```

---

# Standard Responsibilities

## Field Application Engineer (FAE)

Responsible for:

- On-site installation
- Detector configuration
- Calibration
- Troubleshooting
- Customer support
- Technical verification

---

## Technical Support Engineer

Responsible for:

- Remote diagnosis
- Log analysis
- SDK troubleshooting
- Software support

---

## Production Engineer

Responsible for:

- Factory configuration
- Initial calibration
- Firmware programming
- Product verification

---

## Quality Engineer

Responsible for:

- Quality inspection
- OQC verification
- RMA evaluation
- Failure confirmation

---

# Standard Records

Every SOP should specify the records that must be retained.

Typical records include:

- Detector Serial Number
- Firmware Version
- SDK Version
- Calibration Version
- Detector.log
- Network Configuration
- Test Images
- Operation Time
- Operator
- Customer Information (if applicable)

---

# Safety Requirements

Before performing any operation:

- Confirm detector power status.
- Verify communication status.
- Confirm correct detector model.
- Confirm compatible SDK version.
- Verify firmware compatibility.
- Ensure calibration files are backed up before modification.
- Preserve original logs before troubleshooting.

---

# Decision Principles

When abnormal conditions occur:

1. Stop the current operation if there is a risk of data corruption or hardware damage.
2. Preserve all logs and original files before making changes.
3. Follow the corresponding DecisionTree document.
4. Refer to the associated ErrorCode document if an error is reported.
5. Escalate to R&D only after completing all standard troubleshooting steps.

---

# Related Modules

| Module | Purpose |
|---------|---------|
| 03_Hardware | Hardware architecture and components |
| 04_Communication | Communication mechanisms |
| 05_Calibration | Calibration principles |
| 06_Workflow | Business and engineering workflows |
| 07_FailureKnowledge | Failure mechanisms |
| 08_ImageDiagnosis | Image abnormalities and analysis |
| 09_DecisionTree | Troubleshooting decision logic |
| 11_Case | Field troubleshooting cases |
| 12_ErrorCode | Error code reference |
| 13_Template | Standard engineering templates |
| 14_Glossary | Standard terminology |

---

# SOP Usage Flow

```text
Receive Task

↓

Read Relevant SOP

↓

Prepare Environment

↓

Perform Operation

↓

Verify Result

↓

If Normal
    ↓
Complete Record

If Abnormal
    ↓
DecisionTree

↓

ErrorCode

↓

FailureKnowledge

↓

Case

↓

Escalation (if required)
```

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |