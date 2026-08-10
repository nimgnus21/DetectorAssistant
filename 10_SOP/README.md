# Standard Operating Procedures (SOP)

> DetectorAssistant standardized execution layer
>
> Purpose: convert a confirmed engineering task into a repeatable, verifiable, and recordable operation.

---

# Overview

`10_SOP` is the execution layer of DetectorAssistant.

Use this module after the engineer has identified the task to perform, or when a DecisionTree has routed the issue to a standardized action.

The SOP layer answers:

- What operation must be performed?
- What must be prepared before the operation?
- Which tool, file, or evidence is required?
- What result is acceptable?
- What should be done when the expected result is not achieved?
- What record must be retained after completion?

This module does not replace root-cause analysis. If the task itself is not yet clear, start from `08_ImageDiagnosis`, `09_DecisionTree`, `07_FailureKnowledge`, or `12_ErrorCode` as appropriate.

---

# Quick Field Entry

## Image Abnormality

Observed image is abnormal and the corrective procedure must be executed:

- [Image Troubleshooting SOP](ImageTroubleshooting.md)

Typical upstream entry:

- [Image Diagnosis](../08_ImageDiagnosis/README.md)
- [Image DecisionTree](../09_DecisionTree/Image/)

Typical supporting tools:

- [ImageJ](../17_Tools/ImageJ/README.md)
- [Offset Viewer](../17_Tools/OffsetViewer/README.md)
- [Log Viewer](../17_Tools/Log/README.md)

---

## Network Configuration or Communication Problem

Detector cannot communicate, cannot be reached, or requires network configuration:

- [Network Configuration SOP](NetworkConfiguration.md)

Typical upstream entry:

- [Connection DecisionTree](../09_DecisionTree/Connection/)
- [Communication ErrorCode](../12_ErrorCode/Communication/)

Typical supporting tools:

- [Ping](../17_Tools/Ping/README.md)
- [Wireshark](../17_Tools/Wireshark/README.md)

---

## Calibration Failure or Calibration Task

Offset, Gain, Defect, or other supported calibration operations require standardized execution:

- [Calibration SOP](Calibration.md)

Typical upstream entry:

- [Calibration DecisionTree](../09_DecisionTree/Calibration/)
- [Calibration ErrorCode](../12_ErrorCode/Calibration/)

Typical supporting tool:

- [Calibration Tools](../17_Tools/SDKTool/CalibrationTools.md)

---

## Firmware Upgrade or Recovery

A firmware upgrade, compatibility correction, or firmware recovery operation is required:

- [Firmware Upgrade SOP](FirmwareUpgrade.md)

Typical upstream entry:

- [Firmware DecisionTree](../09_DecisionTree/Firmware/)
- [Firmware ErrorCode](../12_ErrorCode/Firmware/)

Typical supporting tool:

- [Firmware Upgrade Tool Guide](../17_Tools/SDKTool/FirmwareUpgrade.md)

---

## Detector Installation

New detector installation or initial system deployment:

- [Detector Installation SOP](DetectorInstallation.md)

---

## Remote Technical Support

Remote diagnosis, evidence collection, or guided customer troubleshooting:

- [Remote Support SOP](RemoteSupport.md)

---

## Detector Replacement

Detector replacement and post-replacement verification:

- [Detector Replacement SOP](DetectorReplacement.md)

---

## Preventive Maintenance

Scheduled inspection or preventive maintenance activity:

- [Preventive Maintenance SOP](PreventiveMaintenance.md)

---

## RMA Processing

A detector or component must enter the return-material / failure-handling process:

- [RMA SOP](RMA.md)

---

# Current SOP Library

| SOP | Primary Use |
|---|---|
| [Detector Installation](DetectorInstallation.md) | New detector installation and initial verification |
| [Network Configuration](NetworkConfiguration.md) | Network setup and communication verification |
| [Calibration](Calibration.md) | Standard calibration execution and verification |
| [Firmware Upgrade](FirmwareUpgrade.md) | Firmware update and upgrade verification |
| [Image Troubleshooting](ImageTroubleshooting.md) | Standard response to image abnormalities |
| [Remote Support](RemoteSupport.md) | Remote diagnosis and evidence collection |
| [Detector Replacement](DetectorReplacement.md) | Replacement and post-replacement verification |
| [Preventive Maintenance](PreventiveMaintenance.md) | Periodic inspection and maintenance |
| [RMA](RMA.md) | Return-material and failure-handling process |

The table above is derived only from the current files in `10_SOP`.

---

# Standard Execution Model

Every SOP should be executable as the following closed loop:

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
  ↓
Record / Evidence
```

The minimum operational principles are:

1. Start each step with an action.
2. Perform one primary action per step.
3. Use measurable acceptance criteria where possible.
4. Preserve original logs and files before destructive changes.
5. Do not skip the verification step after the operation.
6. Route unresolved exceptions back to the appropriate DecisionTree or ErrorCode.

---

# Standard SOP Structure

The target structure for SOP documents is:

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

The mandatory opening concepts are:

- Scope
- Objective
- Responsibility

Where practical, the procedure itself should follow the `Input → Process → Output → Acceptance Criteria → Exception Handling` model.

---

# When Not to Start with an SOP

Do not use an SOP as a substitute for diagnosis when the problem category is still unknown.

Use the following routing first:

```text
Unknown Field Problem
        ↓
Symptom / Error Classification
        ↓
08_ImageDiagnosis or 12_ErrorCode
        ↓
09_DecisionTree
        ↓
Confirmed Task
        ↓
10_SOP
        ↓
17_Tools + Evidence
        ↓
11_Case / Knowledge Feedback
```

For a known operational task, entering the corresponding SOP directly is appropriate.

---

# Evidence and Record Requirements

Before modifying detector configuration, calibration data, firmware, or other operational state, preserve the relevant evidence.

Typical records include:

- Detector model and serial number
- Firmware version
- SDK version
- Calibration version or status
- Detector log
- Network configuration
- Test images
- Operation time
- Operator
- Customer information where applicable

The exact record set should follow the specific SOP and failure scenario.

---

# Roles

## Field Application Engineer

Typical responsibilities:

- On-site installation
- Detector configuration
- Calibration
- Troubleshooting execution
- Customer technical support
- On-site verification

## Technical Support Engineer

Typical responsibilities:

- Remote diagnosis
- Log analysis
- SDK and software support
- Evidence review
- Escalation coordination

## Production Engineer

Typical responsibilities:

- Factory configuration
- Initial calibration
- Firmware programming
- Product verification

## Quality Engineer

Typical responsibilities:

- Quality inspection
- OQC verification
- RMA evaluation
- Failure confirmation

---

# Relationship with Other Modules

| Module | Relationship to SOP |
|---|---|
| [Workflow](../06_Workflow/README.md) | Defines broader engineering or business flow |
| [Failure Knowledge](../07_FailureKnowledge/README.md) | Explains failure classes and mechanisms |
| [Image Diagnosis](../08_ImageDiagnosis/README.md) | Classifies observed image phenomena |
| [DecisionTree](../09_DecisionTree/README.md) | Determines which diagnostic or operational branch to take |
| [Case](../11_Case/README.md) | Preserves verified field conclusions and evidence |
| [ErrorCode](../12_ErrorCode/README.md) | Interprets reported SDK, communication, firmware, calibration, or generator errors |
| [Tools](../17_Tools/README.md) | Provides execution, verification, and evidence tools |

---

# SOP Usage Flow

```text
Receive Task or Confirmed Diagnosis
        ↓
Select SOP
        ↓
Check Preconditions
        ↓
Prepare Tools and Files
        ↓
Preserve Original Evidence
        ↓
Execute Procedure
        ↓
Verify Acceptance Criteria
        ↓
     ┌───┴───┐
     │       │
   PASS     FAIL
     │       │
     ▼       ▼
Record    DecisionTree / ErrorCode
     │       ↓
     │   Next Diagnostic Branch
     │
     ▼
Close Task / Update Case if Verified Knowledge Is New
```

---

# Maintenance Rules

1. Do not change the frozen first-level directory structure through this README.
2. Add a new SOP only when a repeatable operational procedure exists.
3. Every new SOP should define scope, objective, responsibility, procedure, acceptance criteria, exception handling, records, and related documents.
4. A new SOP must link to the relevant DecisionTree, Tool, ErrorCode, Workflow, or Case where those modules exist.
5. Do not create placeholder links for future documents.
6. If a real field case exposes a missing or unsafe operation, update the SOP only after the corrective procedure is technically verified.

---

# Related Modules

- [Project README](../README.md)
- [Workflow](../06_Workflow/README.md)
- [Failure Knowledge](../07_FailureKnowledge/README.md)
- [Image Diagnosis](../08_ImageDiagnosis/README.md)
- [DecisionTree](../09_DecisionTree/README.md)
- [Case](../11_Case/README.md)
- [ErrorCode](../12_ErrorCode/README.md)
- [Tools](../17_Tools/README.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.1 | 2026-08-10 | Rebuilt README as a field-task navigation layer using the current SOP file set; preserved SOP execution and maintenance standards |
| v1.0 | 2026-08-07 | Initial release |