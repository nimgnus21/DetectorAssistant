# Ghost

Version: V1.1

Module: 11_Case / Image

Status: Reference Candidate

Case Classification: Mixed Field Experience / Diagnostic Reference

Evidence Level: Mixed Candidate Evidence — this file summarizes the Ghost phenomenon, multiple candidate mechanisms, a generic diagnostic sequence, and several anonymous field experiences. It is not a single event-level Case and must not be treated as a universally verified root-cause record.

Promotion Rule: Any individual Ghost scenario may be promoted to a `Verified` Case only after the product/mode/version scope, preserved before/after evidence, actual diagnostic sequence, corrective action, and controlled dynamic retest are recorded.

Severity: ★★★★☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Dynamic Flat Panel Detector
- Pluto Series
- Dynamic Imaging System
- Continuous Acquisition System

Related Documents:

- [GhostArtifact](../../08_ImageDiagnosis/GhostArtifact/)
- [DynamicCalibration](../../05_Calibration/DynamicCalibration.md)
- [DynamicCorrectionWorkflow](../../06_Workflow/DynamicCorrectionWorkflow.md)
- [GhostFailure](../../07_FailureKnowledge/CalibrationFailure/GhostFailure.md)
- [Ghost DecisionTree](../../09_DecisionTree/Image/Ghost.md)
- [DynamicDetector Principles](../../13_Principles/DynamicDetector/)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

This file previously used `Status: Released`, but its content combines:

- a general Ghost phenomenon description;
- multiple possible mechanisms;
- a generic diagnostic process;
- four anonymous field experiences;
- engineering recommendations and prevention guidance.

Those elements do not describe one independently evidenced event. The file is therefore retained as a `Reference Candidate` rather than a `Verified` or single-event Case.

Important boundary:

> Ghost symptom confirmed does not automatically mean Ghost Template, Mode132, ROI, network, or detector lag is the root cause.

Each candidate branch requires event evidence.

---

# 2. Reference Phenomenon

Ghost（残影）可表现为连续动态采集中前一帧或前几帧的高对比结构、轮廓或灰度信息在后续图像中仍可见。

Typical observations:

- 上一帧人体轮廓残留；
- 高吸收区域残留；
- 图像拖尾；
- 曝光目标移动后仍保留旧位置轮廓；
- 连续图像存在历史影像。

This file is primarily applicable to dynamic/continuous acquisition scenarios. It must not be used to exclude all residual-image phenomena in other products without checking the actual product behavior.

---

# 3. Ghost vs Similar Phenomena

Before selecting a cause, distinguish the phenomenon from similar image behavior:

| Phenomenon | Key Observation | Primary Next Step |
|---|---|---|
| Ghost | Residual structure correlates with a previous image/history | Check temporal sequence and Ghost correction path |
| Lag | Pixel response or recovery appears slow and may not map cleanly to one previous frame | Enter [Lag](../../09_DecisionTree/Image/Lag.md) |
| Fixed line/dot | Artifact remains at the same detector coordinate | Enter the relevant spatial-artifact DecisionTree |
| Image transfer corruption | Artifact changes with transfer/acquisition behavior | Check Image Loss / communication evidence |
| Periodic interference | Repeating pattern not necessarily related to previous frame content | Check interference/calibration path |

Do not classify a phenomenon as Ghost solely because it appears as a shadow or trail.

---

# 4. Candidate Diagnostic Branches

The following are candidate branches, not universal root causes.

## 4.1 Ghost Correction Not Active or Not Applied

Candidate conditions may include:

- required correction/template not generated;
- correction/template not loaded;
- correction path not enabled for the actual mode.

Required evidence:

- mode configuration;
- correction/template load state;
- before/after output under the same acquisition condition.

## 4.2 Template Scope or Compatibility Mismatch

Candidate conditions may include:

- template generated for a different mode or acquisition configuration;
- template no longer applicable after a relevant configuration change;
- template file/load error.

Do not assume every ROI, Frame Rate, or Mode change invalidates every template; verify the applicable product rule.

## 4.3 Dynamic Mode / Configuration Change

Record the actual before/after configuration, including where applicable:

- ROI;
- Exposure Mode;
- Dynamic Mode;
- Frame Rate;
- correction-related parameters.

The change itself is evidence only after controlled comparison.

## 4.4 Calibration Data Quality / Acquisition Interruption

Candidate condition:

- calibration input was incomplete or abnormal because acquisition experienced image loss, timeout, or other interruption.

Boundary:

An interrupted calibration process is not proof that network instability is the ultimate Ghost mechanism. Preserve acquisition evidence and verify the generated correction result.

## 4.5 Detector Temporal Response / Long Continuous Exposure

Observed Ghost severity may increase under sustained or high-load dynamic operation.

This pattern requires controlled evidence before being classified as an intrinsic detector temporal-response limitation.

---

# 5. Reference Diagnostic Process

## Step 1 — Confirm Product and Acquisition Mode

Record:

- product/model;
- dynamic/static mode;
- acquisition mode;
- frame rate where applicable;
- software/SDK/firmware version.

Do not start by regenerating calibration data before preserving the original configuration.

## Step 2 — Confirm Temporal Correlation

Check whether the residual structure corresponds to a previous frame or earlier high-contrast exposure.

Preserve a short image sequence showing:

- source frame;
- subsequent affected frame(s);
- frame order/timestamp where available.

## Step 3 — Check Correction State

Verify the actual Ghost correction/template state for the active mode:

- generated;
- loaded;
- enabled/applied;
- compatible with the active configuration according to product requirements.

## Step 4 — Check Configuration Change History

Compare the current configuration with the configuration under which the correction/template was created.

Focus on changes that the applicable product documentation identifies as relevant to correction validity.

## Step 5 — Check Calibration Evidence

If regeneration is required:

- preserve the existing state first;
- record the calibration input and completion result;
- record Image Loss/Timeout or other interruptions;
- do not overwrite the original evidence without backup.

## Step 6 — Controlled Retest

Repeat a representative dynamic sequence and compare:

- before/after residual severity;
- frame-to-frame persistence;
- reproducibility under the same operating condition.

Use [Ghost DecisionTree](../../09_DecisionTree/Image/Ghost.md) for branch routing and [DynamicCorrectionWorkflow](../../06_Workflow/DynamicCorrectionWorkflow.md) for the applicable correction workflow.

---

# 6. Candidate Field Experiences

## Candidate A — Correction/Template Not Loaded

Observed pattern:

- dynamic images show residual structure consistent with earlier frames;
- correction/template state is found not to be loaded or applied;
- symptom improves after restoring the intended correction state.

Promotion evidence:

- product/mode/version;
- correction state before/after;
- source and affected frame sequence;
- controlled retest.

## Candidate B — Configuration Changed After Template Creation

Observed pattern:

- correction effectiveness is reduced after a relevant acquisition configuration change;
- a new or product-approved correction procedure restores expected output.

Promotion evidence:

- exact changed parameter;
- template generation scope;
- before/after image sequence;
- repeatability.

## Candidate C — Mode/Swap Configuration Candidate

Observed pattern:

- dynamic residual behavior is associated with a specific mode configuration;
- the original record references Mode132 / Swap Mode and related acquisition behavior.

Evidence boundary:

The current record does not provide sufficient event-level evidence to state that Mode132 is a universal Ghost root cause. Verify product-specific configuration requirements before modification.

## Candidate D — Calibration Acquisition Interruption

Observed pattern:

- correction/calibration input is affected by acquisition interruption;
- regenerating valid calibration data after resolving the interruption improves the output.

Promotion evidence:

- interruption log/evidence;
- calibration result;
- before/after image sequence;
- controlled verification.

---

# 7. Resolution Boundary

A corrective action may be considered effective only when the affected dynamic sequence is retested under the relevant original operating condition.

Recommended verification includes:

- continuous multi-frame acquisition;
- comparison with the original source/residual pattern;
- confirmation that the intended correction state is active;
- repeatability over a documented number of sequences.

A single visually acceptable frame is insufficient to prove a Ghost mechanism is resolved.

---

# 8. Current Knowledge Conclusions

## Supported Reference Findings

- Ghost-like residual artifacts are primarily investigated through temporal frame relationships.
- Dynamic acquisition mode and correction state are relevant diagnostic dimensions.
- Correction/template state and configuration compatibility should be checked before concluding detector hardware failure.
- Ghost and Lag require separate diagnostic paths.
- Interrupted calibration/acquisition can affect correction data quality and requires evidence review.

## Root Cause Status

Not Applicable at file level.

This document contains multiple candidate mechanisms and does not represent one event-level root cause.

---

# 9. Knowledge Feedback Review

| Layer | Result | Action / Reason |
|---|---|---|
| FailureKnowledge | No direct update required | [GhostFailure](../../07_FailureKnowledge/CalibrationFailure/GhostFailure.md) remains the generic mechanism layer |
| DecisionTree | No direct update required | Existing Ghost routing remains the primary diagnostic entry |
| Workflow | No direct update required | [DynamicCorrectionWorkflow](../../06_Workflow/DynamicCorrectionWorkflow.md) remains the execution path |
| Calibration | No direct update required | No new verified calibration rule was established from mixed evidence |
| Tools | No direct update required | [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md) remains the relevant tool entry |
| Case | Reclassified | Retained as Reference Candidate; future verified events should be independent Case records |

---

# 10. Promotion Requirements for a Verified Ghost Case

A future event should contain at minimum:

- Case ID;
- customer/project identifier where permitted;
- detector model and SN or anonymized unique identifier;
- software/SDK/firmware version;
- dynamic mode and key acquisition parameters;
- before/after image sequence;
- correction/template status;
- actual diagnostic sequence;
- corrective action;
- controlled multi-frame verification;
- root-cause evidence or explicit unresolved status.

---

# 11. Prevention Guidance

Use only product-approved procedures.

Recommended operational controls:

- preserve correction/template version information where supported;
- verify correction applicability after relevant approved configuration changes;
- validate Ghost behavior with multi-frame sequences rather than a single image;
- preserve acquisition interruption evidence during calibration;
- do not overwrite the only copy of a known-good template during investigation.

---

# 12. Related Documents

- [GhostArtifact](../../08_ImageDiagnosis/GhostArtifact/)
- [DynamicCalibration](../../05_Calibration/DynamicCalibration.md)
- [DynamicCorrectionWorkflow](../../06_Workflow/DynamicCorrectionWorkflow.md)
- [GhostFailure](../../07_FailureKnowledge/CalibrationFailure/GhostFailure.md)
- [Ghost DecisionTree](../../09_DecisionTree/Image/Ghost.md)
- [DynamicDetector Principles](../../13_Principles/DynamicDetector/)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 13. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Batch 5 admission audit: reclassified as Reference Candidate, separated Ghost phenomenon from candidate mechanisms, added evidence boundaries and promotion rules |
| V1.0 | 2026-08 | Initial Ghost field-experience and diagnostic summary |