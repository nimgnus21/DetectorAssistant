# ImageShift

Version: V1.1

Case ID: CASE-IMG-008

Module: 11_Case / Image

Status: Resolved

Case Classification: Mixed Field Evidence / Event Record

Evidence Level: Resolved Event Evidence — the primary Pluto0900X event records a repeatable dynamic-mode image shift and recovery after configuration/timing correction. The file also contains a separate field experience with software-side candidates. These records must not be merged into one universal root cause.

Promotion Rule: Promote the primary root cause to `Verified` only when preserved timing/configuration evidence demonstrates the mismatch and controlled before/after testing isolates the causal variable.

Severity: ★★★★☆

Typical Frequency: ★★☆☆☆

Applicable Products:

- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- [ImageShiftArtifact](../../08_ImageDiagnosis/ImageShiftArtifact/)
- [ImageShift FailureKnowledge](../../07_FailureKnowledge/ImageFailure/ImageShift.md)
- [ImageShift DecisionTree](../../09_DecisionTree/Image/ImageShift.md)
- [ImageGenerationWorkflow](../../06_Workflow/ImageGenerationWorkflow.md)
- [ReadoutWorkflow](../../06_Workflow/ReadoutWorkflow.md)
- [ModeConfiguration](../../17_Tools/SDKTool/ModeConfiguration.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

The file contains two evidence streams:

1. Primary Case: Pluto0900X dynamic acquisition with a repeatable image-position shift and recovery after Mode/Trigger-related correction.
2. Field Experience 01: a separate pre-sales report in which detector hardware was reported normal and investigation focused on reconstruction, synchronization, display offset, and application-side processing.

These records do not establish one universal ImageShift root cause. The primary event remains `Resolved`; the additional experience is retained as a candidate diagnostic branch.

---

# 2. Primary Case Summary

## Case Name

Repeatable Image Position Shift During Dynamic Acquisition

## Product / Environment

Customer Type:

- OEM Customer

Product:

- Pluto0900X

Detector:

- Dynamic Detector

Working Mode:

- Continuous Acquisition

Evidence limitations:

- detector SN not preserved;
- firmware/FPGA version not preserved;
- original Mode/Trigger configuration snapshot not attached;
- SDK/Detector log not attached.

---

# 3. Fault Description

Customer reported that during continuous acquisition the complete image shifted left or right.

Observed characteristics:

- image content remained present;
- image position changed as a whole;
- shift amount was approximately fixed under the recorded condition;
- abnormality persisted during continuous acquisition;
- static mode was reported normal while dynamic mode was abnormal.

This pattern should first be distinguished from:

- detector-coordinate artifact;
- ROI/display cropping;
- software reconstruction offset;
- frame synchronization mismatch;
- trigger/exposure timing mismatch.

---

# 4. Evidence Classification

| Evidence | Observation | Supported Finding |
|---|---|---|
| Static mode | Reported normal | Problem was mode-dependent in the recorded event |
| ROI check | Reported normal | No ROI abnormality was found in the recorded investigation |
| Mode configuration | Frame configuration inconsistent with customer software | Configuration mismatch candidate supported |
| Trigger timing | Trigger reported to arrive early | Timing mismatch candidate supported |
| Reconfiguration | Mode reconfigured | Corrective change applied |
| Retest | Image position returned to normal; continuous acquisition stable | Resolution supported |
| Timing capture/log | Not preserved | Exact causal timing relationship not independently verified |

---

# 5. Troubleshooting Timeline

## Step 1 — Compare Static and Dynamic Modes

Result:

- static mode normal;
- dynamic/continuous mode abnormal.

Finding:

The recorded symptom was mode-dependent.

## Step 2 — Check ROI Configuration

Checks included:

- alignment requirement applicable to the product;
- whether ROI had changed.

Recorded result:

- configuration reported normal.

## Step 3 — Check Mode Configuration

Focus:

- Frame Rate;
- Exposure Mode;
- Readout Timing.

Recorded result:

- Frame configuration was inconsistent with the customer software configuration.

## Step 4 — Check Trigger Timing

Signals reviewed:

- Acquire;
- Enable;
- X-Ray;
- FrameReq.

Recorded result:

- Trigger was reported to arrive early relative to the expected sequence.

Evidence boundary:

No preserved timing trace is attached. The timing mismatch is therefore a supported candidate, not a fully verified mechanism.

## Step 5 — Reconfigure and Retest

Action:

- correct Mode-related configuration;
- restart according to the applicable procedure;
- repeat continuous acquisition.

Result:

- image position returned to normal;
- continuous acquisition remained stable;
- customer confirmed resolution.

---

# 6. Current Conclusion

## Verified Findings

- the event was repeatable in dynamic acquisition;
- static operation was reported normal;
- a Frame/Mode configuration inconsistency was found;
- Trigger timing was reported inconsistent with the expected sequence;
- image position recovered after configuration correction and retest.

## Root Cause

Not Fully Confirmed.

## Suspected Failure Mechanism

Mismatch between the detector operating Mode and acquisition/trigger synchronization, potentially causing incorrect frame/readout alignment.

Alternative branches remain possible without preserved traces:

- application-side synchronization;
- image reconstruction parameters;
- display offset/processing logic.

---

# 7. Resolution

The recorded field action was:

1. verify ROI configuration;
2. inspect Mode configuration;
3. inspect Trigger/acquisition timing;
4. correct the applicable configuration;
5. restart according to the approved procedure;
6. repeat continuous acquisition under the original operating condition.

The Case does not establish that every ImageShift event should be solved by Mode or Trigger changes.

---

# 8. Verification

Recorded result:

- image position returned to normal;
- continuous acquisition stable;
- no repeated shift observed during the recorded verification;
- customer confirmed resolution.

For future promotion to `Verified`, preserve:

- before/after Mode file or parameter set;
- trigger timing trace or timestamp correlation;
- original and corrected image sequence;
- SDK/Detector logs;
- product and software/firmware versions.

---

# 9. Associated Field Experience — Software / Display Branch

Source:

- FAE Pre-sales Weekly Report

Observed pattern:

- detector communication normal;
- image acquisition succeeds;
- displayed image shifts horizontally or vertically;
- shift repeatable under the same condition;
- detector hardware and calibration reported normal.

Candidate branches:

- incorrect image reconstruction parameters;
- synchronization mismatch between detector output and software processing;
- display offset configuration;
- application-side image processing logic.

Recommended branch test:

1. verify detector output resolution;
2. compare software reconstruction parameters;
3. verify synchronization settings;
4. compare with the official SDK Demo where applicable;
5. repeat acquisition after one documented parameter change.

Evidence boundary:

This is a separate field experience, not proof that the primary Pluto0900X event had a software-display root cause.

---

# 10. Diagnostic Lessons

- Image Shift is a phenomenon, not a root cause.
- First distinguish detector-coordinate shift from display/reconstruction shift.
- Dynamic-only symptoms justify checking Mode, Frame Rate, readout, and synchronization boundaries.
- Do not replace detector hardware before checking configuration and software-processing evidence.
- Do not assume all ImageShift events are Trigger problems.
- Preserve timing/configuration evidence before correction whenever possible.

---

# 11. Knowledge Feedback Review

| Layer | Result | Action / Reason |
|---|---|---|
| FailureKnowledge | No update required | Existing ImageShift knowledge already represents the generic mechanism layer |
| DecisionTree | No update required | Existing ImageShift DecisionTree remains the primary routing entry |
| Workflow | No update required | ImageGeneration/Readout workflows remain applicable |
| Tools | No update required | ModeConfiguration is the existing configuration entry |
| Case | Updated | Separated primary event from software/display field experience |
| ErrorCode | Not applicable | No error-code evidence recorded |

---

# 12. Evidence Gap for Promotion to Verified

Missing evidence:

- detector SN;
- firmware/FPGA/software/SDK versions;
- before/after Mode configuration;
- Trigger timing trace;
- original image sequence;
- SDK/Detector logs.

Without these, the Case remains `Resolved`.

---

# 13. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Batch 5 admission audit: retained primary event as Resolved, separated Trigger/Mode findings from software/display field experience, added evidence boundaries |
| V1.0 | 2026-08 | Initial Image Shift field case |