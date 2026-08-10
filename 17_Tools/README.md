# Tools

> DetectorAssistant field-tool entry point
>
> Purpose: route a confirmed diagnostic task to the correct tool, define the expected evidence, and return the result to verification, Case, or escalation.

---

# Tool Role in the Support Loop

`17_Tools` is an execution and evidence layer. A tool should not be selected merely because it exists; it should be entered from a concrete diagnostic question raised by ImageDiagnosis, FailureKnowledge, DecisionTree, SOP, or ErrorCode.

```text
Customer Symptom
      ↓
ImageDiagnosis / FailureKnowledge / ErrorCode
      ↓
DecisionTree
      ↓
SOP or Workflow
      ↓
Select Tool
      ↓
Collect / Analyze Evidence
      ↓
Verification
      ├── Resolved → Case / Knowledge Feedback
      └── Unresolved → Escalation with Evidence
```

---

# Tool Map

The following entries reflect the current repository structure.

| Tool | Primary Use | Typical Entry |
|---|---|---|
| [SDKTool](SDKTool/README.md) | SDK configuration, calibration, firmware, license, mode configuration, log export | Software / Calibration / Firmware / Configuration |
| [Ping](Ping/README.md) | Basic IP reachability and communication verification | Connection / Detector Offline / Network Failure |
| [Wireshark](Wireshark/README.md) | Packet-level communication analysis | Communication timeout / unstable communication / protocol investigation |
| [Offset Viewer](Offset%20Viewer/README.md) | Offset image and fixed-pattern inspection | Image abnormality / Offset investigation / Calibration |
| [ImageJ](ImageJ/README.md) | Image measurement and artifact characterization | Image diagnosis / image abnormality comparison |
| [Log Viewer](Log%20Viewer/README.md) | Debug, SDK and application log analysis | Software failure / ErrorCode / abnormal runtime behavior |

---

# Quick Field Entry

## Detector Cannot Connect or Communicate

Start with:

1. [Ping](Ping/README.md)
2. [Wireshark](Wireshark/README.md) when packet-level verification is required
3. [SDKTool](SDKTool/README.md) when SDK or detector configuration must be checked

Then return to:

- [Connection DecisionTree](../09_DecisionTree/Connection/)
- [Network Configuration SOP](../10_SOP/NetworkConfiguration.md)

Expected evidence:

- Ping result
- Host and detector IP configuration
- Packet capture when required
- SDK / application log

---

## Image Artifact or Image Quality Abnormality

Start with:

1. [ImageJ](ImageJ/README.md) for measurement and pattern comparison
2. [Offset Viewer](Offset%20Viewer/README.md) for offset / fixed-pattern investigation
3. [SDKTool Calibration Tools](SDKTool/CalibrationTools.md) when calibration verification is required

Then return to:

- [Image Diagnosis](../08_ImageDiagnosis/README.md)
- [Image DecisionTree](../09_DecisionTree/Image/)
- [Image Troubleshooting SOP](../10_SOP/ImageTroubleshooting.md)

Expected evidence:

- RAW image where available
- Processed image
- Repeated acquisition samples
- Fixed coordinate / row / column information
- Calibration status or related files

---

## Calibration Task or Calibration Failure

Start with:

1. [SDKTool Calibration Tools](SDKTool/CalibrationTools.md)
2. [Offset Viewer](Offset%20Viewer/README.md) when offset evidence must be inspected
3. [SDKTool](SDKTool/README.md) for supporting configuration and log export

Then return to:

- [Calibration DecisionTree](../09_DecisionTree/Calibration/)
- [Calibration SOP](../10_SOP/Calibration.md)

Expected evidence:

- Calibration result
- Calibration log
- Input images or required image sets
- Offset / gain / defect-related outputs where applicable

---

## Firmware or License Issue

Start with the relevant SDK tool:

- [Firmware Upgrade](SDKTool/FirmwareUpgrade.md)
- [License Management](SDKTool/LicenseManagement.md)
- [Log Export](SDKTool/LogExport.md)

Then return to:

- [Firmware DecisionTree](../09_DecisionTree/Firmware/)
- [Firmware Upgrade SOP](../10_SOP/FirmwareUpgrade.md)
- [Firmware ErrorCode](../12_ErrorCode/Firmware/Upgrade.md)

Expected evidence:

- Detector model and SN
- Firmware version before and after operation
- Upgrade / SDK log
- Error code or status
- Reproduction result

---

## Software / SDK Runtime Issue

Start with:

1. [Log Viewer](Log%20Viewer/README.md)
2. [SDKTool Log Export](SDKTool/LogExport.md)
3. [iDetector Quick Troubleshooting](SDKTool/iDetectorQuickTroubleshooting.md)

Then return to:

- [Software DecisionTree](../09_DecisionTree/Software/)
- [SDK ErrorCode](../12_ErrorCode/SDK/)

Expected evidence:

- SDK version
- Detector model and firmware version
- Error code
- Complete relevant log segment
- Reproduction steps and result

---

# SDKTool Functional Entry

Use the specific file when the task is already known:

- [Calibration Tools](SDKTool/CalibrationTools.md)
- [DTDITool](SDKTool/DTDITool.md)
- [Firmware Upgrade](SDKTool/FirmwareUpgrade.md)
- [License Management](SDKTool/LicenseManagement.md)
- [Log Export](SDKTool/LogExport.md)
- [Mode Configuration](SDKTool/ModeConfiguration.md)
- [iDetector Quick Troubleshooting](SDKTool/iDetectorQuickTroubleshooting.md)

Do not force a user through the general SDKTool README when a concrete tool task is already identified.

---

# Evidence and Return Path

Every tool operation should produce one of the following outputs:

- Verification result
- Image evidence
- Network evidence
- Log evidence
- Calibration result
- Firmware / version result
- Configuration result
- Unresolved diagnostic evidence for escalation

After the tool result is obtained:

```text
Tool Result
    ↓
DecisionTree conclusion confirmed?
    ├── Yes → Update / admit Case if the result is reusable knowledge
    └── No  → Preserve evidence and continue the next diagnostic branch
```

A tool output alone is not a root-cause conclusion unless the corresponding diagnostic rule defines it as sufficient evidence.

---

# Key Cross-Module Navigation

- [Project README](../README.md)
- [Failure Knowledge](../07_FailureKnowledge/README.md)
- [Image Diagnosis](../08_ImageDiagnosis/README.md)
- [DecisionTree](../09_DecisionTree/README.md)
- [SOP](../10_SOP/README.md)
- [Case Module](../11_Case/README.md)
- [ErrorCode](../12_ErrorCode/README.md)

---

# Maintenance Rules

A tool or tool document must define, at minimum:

1. Applicable diagnostic scenario.
2. Input or precondition.
3. Operation objective.
4. Expected output or evidence.
5. Normal acceptance criteria.
6. Next action when the result is abnormal or inconclusive.
7. At least one real calling relationship from SOP, DecisionTree, FailureKnowledge, ErrorCode, or another approved support entry.

A tool that has no defined support use, no evidence output, or no traceable calling relationship should not be treated as a formal Tool Map entry.

---

# Related Documents

- [Tool Overview in Project README](../README.md)
- [DecisionTree](../09_DecisionTree/README.md)
- [SOP](../10_SOP/README.md)
- [Case](../11_Case/README.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v2.0 | 2026-08-10 | Rebuilt Tool Map from current directories; added concrete tool entry points, evidence outputs and cross-module return paths |
| v1.0 | 2026-08-10 | Initial tool module entry |