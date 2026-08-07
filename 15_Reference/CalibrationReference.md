# Calibration Reference

> Version: v1.0
>
> Status: Draft
>
> Last Updated: 2026-08-06

---

# 1. Purpose

This document establishes the reference relationship between calibration-related documents and the DetectorAssistant knowledge base.

It does not replace calibration procedures or engineering manuals.

Its purpose is to provide a unified entry point for calibration workflows, troubleshooting, engineering experience, and supporting tools.

---

# 2. Calibration Scope

The calibration system includes:

- Offset Calibration
- Gain Calibration
- Ghost Correction
- Calibration Verification
- Calibration Data Management
- Calibration Recovery

---

# 3. Knowledge Mapping

## Offset Calibration

Knowledge Base

05_Calibration/

- OffsetCalibration.md

Workflow

- CalibrationWorkflow.md

Case

- OffsetGenerationFailed.md

Decision Tree

- Offset Decision Tree

Tool

- CalibrationTools.md

---

## Gain Calibration

Knowledge Base

05_Calibration/

- GainCalibration.md

Workflow

- CalibrationWorkflow.md

Case

- GainCalibrationFailed.md

Decision Tree

- Gain Decision Tree

Tool

- CalibrationTools.md

---

## Ghost Correction

Knowledge Base

05_Calibration/

- GhostCorrection.md

Case

- GhostCorrection.md

Image Diagnosis

- Ghost.md

Decision Tree

- Ghost Decision Tree

---

## Calibration Verification

Knowledge Base

05_Calibration/

- CalibrationVerification.md

Workflow

- CalibrationWorkflow.md

Tool

- CalibrationTools.md

---

## Calibration Recovery

Knowledge Base

05_Calibration/

- CalibrationRecovery.md

Case

- ParameterRecovery.md

Tool

- CalibrationTools.md

---

# 4. Related Image Problems

Calibration abnormalities may lead to:

| Image Symptom | Related Module |
|---------------|----------------|
| Noise | 08_ImageDiagnosis/Noise.md |
| Ghost | 08_ImageDiagnosis/Ghost.md |
| Vertical Line | 08_ImageDiagnosis/VerticalLine.md |
| Horizontal Line | 08_ImageDiagnosis/HorizontalLine.md |
| Black Dots | 08_ImageDiagnosis/BlackDots.md |
| White Dots | 08_ImageDiagnosis/WhiteDots.md |

---

# 5. Related Decision Trees

- Calibration Failure
- Offset Failure
- Gain Failure
- Ghost Failure

---

# 6. Related Tools

17_Tools/

- CalibrationTools.md
- SDKTool/
- FirmwareUpgrade.md

---

# 7. Engineering Best Practice

Before recalibration:

1. Verify detector communication.
2. Verify firmware compatibility.
3. Verify detector temperature.
4. Verify exposure conditions.
5. Verify generator stability.
6. Verify calibration environment.

After calibration:

1. Verify Offset.
2. Verify Gain.
3. Verify Ghost.
4. Perform image quality verification.
5. Archive calibration records.

---

# 8. Typical Engineering Mistakes

- Repeating calibration without root cause analysis.
- Using calibration files from another detector.
- Ignoring generator instability.
- Performing calibration before firmware verification.
- Skipping image verification after calibration.

---

# 9. Maintenance Rules

Review this document when:

- Calibration workflow changes.
- Calibration algorithms are updated.
- New detector models are introduced.
- New engineering experience is accumulated.

---

# 10. Related Documents

## Calibration

- 05_Calibration/

## Workflow

- CalibrationWorkflow.md

## Case

- 11_Case/Calibration/

## Image Diagnosis

- 08_ImageDiagnosis/

## Decision Tree

- 09_DecisionTree/

## Tools

- CalibrationTools.md