# DecisionTree

> Field diagnostic routing layer: use observed behavior and available evidence to select the next verification action.

---

# Purpose

`09_DecisionTree` is the primary branching layer between symptom identification and execution.

Use this module when the question is:

- What should be checked next?
- Which branch best matches the observed behavior?
- What evidence can confirm or eliminate a suspected cause?
- When should troubleshooting stop and escalation begin?

DecisionTree does not replace SOPs, tools, or verified Cases.

```text
Observed Symptom / Error / Image Phenomenon
                    ↓
          08_ImageDiagnosis / 12_ErrorCode
                    ↓
              09_DecisionTree
                    ↓
          Evidence-based Branching
                    ↓
          10_SOP / 06_Workflow
                    ↓
               17_Tools
                    ↓
         Verification / Root Cause
                    ↓
          11_Case / Escalation
                    ↓
            Knowledge Feedback
```

---

# Main Diagnostic Categories

| Category | Enter When | Diagnostic Entry |
|---|---|---|
| Image | Acquired image is abnormal | [Image](Image/) |
| Connection | Detector discovery or communication is abnormal | [Connection](Connection/) |
| Calibration | Calibration cannot complete or result is abnormal | [Calibration](Calibration/) |
| Firmware | Upgrade, firmware state, or version behavior is abnormal | [Firmware](Firmware/) |
| Software | SDK, API, acquisition, save, license, or application behavior is abnormal | [Software](Software/) |

---

# Quick Field Entry

## Image Abnormality

Start with `08_ImageDiagnosis` if the observed phenomenon still needs classification:

- [Image Diagnosis](../08_ImageDiagnosis/README.md)

Then enter the corresponding branch:

- [Image DecisionTree](Image/)
- [Image Troubleshooting SOP](../10_SOP/ImageTroubleshooting.md)
- [Image Tools](../17_Tools/README.md)

For a fixed horizontal line that repeats across images, use:

- [HorizontalLine](Image/HorizontalLine.md)

Do not assign a hardware root cause before checking RAW / repeated-acquisition / calibration evidence.

---

## Connection or Network Problem

Use:

- [Connection DecisionTree](Connection/)
- [Network Configuration SOP](../10_SOP/NetworkConfiguration.md)
- [Ping](../17_Tools/Ping/README.md)
- [Wireshark](../17_Tools/Wireshark/README.md)

Preserve link state, IP configuration, Ping behavior, packet evidence where applicable, and the steps already attempted.

---

## Calibration Problem

Use:

- [Calibration DecisionTree](Calibration/)
- [Calibration SOP](../10_SOP/Calibration.md)
- [Calibration Tools](../17_Tools/SDKTool/CalibrationTools.md)
- [Failure Knowledge](../07_FailureKnowledge/README.md)

Do not treat a calibration failure message as sufficient root-cause evidence. Record calibration type, exposure conditions, template state, logs, and result.

---

## Firmware or Version Problem

Use:

- [Firmware DecisionTree](Firmware/)
- [Firmware Upgrade SOP](../10_SOP/FirmwareUpgrade.md)
- [Firmware Upgrade Tool Guidance](../17_Tools/SDKTool/FirmwareUpgrade.md)
- [ErrorCode](../12_ErrorCode/README.md)

Record the detector model, SN, current version, target version, upgrade package or configuration context, and upgrade result before retrying.

---

## SDK or Software Problem

Use:

- [Software DecisionTree](Software/)
- [Log Collection](../04_Software/Log/LogCollection.md)
- [SDK Tool Guidance](../17_Tools/SDKTool/README.md)
- [Log Viewer](../17_Tools/Log/README.md)
- [ErrorCode](../12_ErrorCode/README.md)

Preserve SDK / application version, API or error return, logs, reproduction steps, and whether the issue reproduces in the official SDK environment when applicable.

---

# Standard Decision Principle

Every DecisionTree should drive one concrete verification step at a time:

```text
Symptom
  ↓
Classification
  ↓
Evidence Available?
  ├── No  → collect evidence
  └── Yes → choose diagnostic branch
               ↓
         Verify / eliminate cause
               ↓
        Confirmed result?
          ├── No  → next branch
          └── Yes → SOP / action
                       ↓
                Verify result
                       ↓
             Case / escalation
```

Do not use a DecisionTree as a checklist of possible causes. Each branch should reduce uncertainty or define the next required action.

---

# Evidence Before Escalation

Collect what is applicable to the active branch:

- Detector model and SN
- Firmware version
- SDK / application version
- RAW / corrected / dark image
- Calibration type and result
- Debug or system log
- Network mode and configuration
- Error code or API return
- Exact reproduction steps
- Actions already attempted and their results

Use project templates under [13_Template](../13_Template/) where applicable.

---

# Relationship with FailureKnowledge

`07_FailureKnowledge` explains failure classes and mechanism-level reasoning.

`09_DecisionTree` converts observed evidence into a concrete next branch.

```text
FailureKnowledge
      ↓ supports reasoning
DecisionTree
      ↓ chooses next verification
SOP / Workflow / Tool
      ↓ executes action
Evidence
      ↓ confirms result
Case
```

Avoid duplicating mechanism explanations across every DecisionTree. Link to FailureKnowledge when mechanism-level analysis is required.

---

# Case Feedback

DecisionTree is a routing layer, not a substitute for a verified Case.

After resolution:

1. Search the relevant category under [11_Case](../11_Case/README.md).
2. Reuse an existing verified Case when the evidence and conditions match.
3. Create or admit a new Case only after the phenomenon, investigation, final cause or treatment, and verification result are recorded.
4. Record reusable findings through [Knowledge Feedback Record](../11_Case/KnowledgeFeedbackRecord.md).
5. Update FailureKnowledge, DecisionTree, SOP, Tools, ErrorCode, or Index only when the new knowledge is verified and reusable.

---

# Escalation Boundary

Escalate when the current branch has produced sufficient evidence but no supported local action remains, or when:

- The issue reproduces after standard verification.
- A hardware defect is strongly indicated.
- Firmware recovery or rollback risk exists.
- SDK Demo and customer application show inconsistent behavior requiring deeper analysis.
- Logs or evidence indicate an internal software / protocol / firmware fault.

Escalation must include the evidence package, not only a symptom description.

---

# Related Modules

- [Project README](../README.md)
- [Image Diagnosis](../08_ImageDiagnosis/README.md)
- [Failure Knowledge](../07_FailureKnowledge/README.md)
- [SOP](../10_SOP/README.md)
- [Case](../11_Case/README.md)
- [Tools](../17_Tools/README.md)
- [ErrorCode](../12_ErrorCode/README.md)

---

# Maintenance Rules

1. Keep the five existing top-level diagnostic categories unchanged unless repository structure is intentionally revised.
2. Add a new branch only when it represents a distinct diagnostic decision, not a duplicate symptom description.
3. Link each executable branch to the relevant SOP, Workflow, Tool, or evidence requirement where those resources exist.
4. Do not embed unverified root-cause conclusions as universal rules.
5. When a verified Case changes a diagnostic boundary, update the affected DecisionTree and its upstream/downstream links together.
6. Remove obsolete paths instead of retaining historical filenames as navigation targets.

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v2.0 | 2026-08-10 | Rebuilt project-level diagnostic entry around current five-category structure; strengthened ImageDiagnosis, SOP, Tool, Evidence, Case and escalation navigation |
| v1.0 | 2026-08-10 | Initial project-level DecisionTree entry |