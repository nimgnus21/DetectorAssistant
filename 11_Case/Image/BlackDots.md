# BlackDots

Version: V1.1

Case ID: CASE-IMG-007

Module: 11_Case / Image

Status: Resolved

Case Classification: Field Case Record

Evidence Level: Resolved Event Evidence — repeated RAW images showed fixed detector-coordinate dark points, Offset/Gain templates were reported normal, the active Defect Template did not include the observed coordinates, and the corrected Defect Template removed the visible artifact. The underlying pixel condition was not independently characterized.

Promotion Rule: Promote the pixel mechanism to `Verified` only when the affected coordinates, raw response, template mapping, and correction effect are preserved and the defect classification is independently confirmed.

Severity: ★★★☆☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- [BlackDotsArtifact](../../08_ImageDiagnosis/BlackDotsArtifact/)
- [PixelFailure](../../07_FailureKnowledge/ImageFailure/PixelFailure.md)
- [BlackDots DecisionTree](../../09_DecisionTree/Image/BlackDots.md)
- [DefectCalibration](../../05_Calibration/DefectCalibration.md)
- [Calibration SOP](../../10_SOP/Calibration.md)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

The record contains one concrete field event with repeated RAW evidence, fixed-coordinate behavior, template inspection, a corrective calibration action, and successful verification. It remains a Case.

The original root-cause statement asserted that the issue was a calibration-data problem and explicitly excluded detector hardware damage. The recorded evidence proves that the active Defect Template did not compensate the visible coordinates and that correction removed the artifact. It does not independently determine whether the underlying pixel response was an intrinsic detector defect, a stale template mapping, or another product-specific condition.

---

# 2. Case Summary

## Case Name

Fixed Dark Points Not Compensated by Active Defect Template

## Case Boundary

This Case applies to image points that:

- remain at the same detector coordinates across repeated acquisitions;
- are visible in RAW evidence under the recorded condition;
- are not explained by a changing/random noise pattern.

It does not represent:

- random temporal noise;
- fixed row/column artifacts;
- exposure-object-dependent dark structures;
- transfer corruption.

---

# 3. Customer Environment

Customer Type:

- Hospital

Product:

- Pluto1717

Detector:

- Ethernet Detector

Working Mode:

- Static Imaging

Evidence limitations:

- detector SN not preserved;
- firmware version not preserved;
- calibration/template version identifiers not preserved;
- affected pixel coordinates not recorded;
- before/after RAW files not attached;
- SDK log not attached.

---

# 4. Fault Description

Customer reported multiple fixed black/dark points in the image.

Observed characteristics:

- point positions were fixed;
- repeated exposures showed the same coordinates;
- recorded behavior did not change with exposure parameters;
- recorded behavior did not depend on the imaged object.

Initial customer concern:

- internal detector pixel damage.

FAE diagnostic direction:

- first classify the artifact as fixed-coordinate behavior;
- compare RAW evidence with Dark/Offset and active correction/template data before deciding hardware replacement.

---

# 5. Evidence Classification

| Evidence | Observation | Supported Finding |
|---|---|---|
| Repeated RAW | Same dark coordinates | Fixed detector-coordinate behavior supported |
| Offset Template | Reported normal | No Offset abnormality identified in the recorded check |
| Gain Template | Reported normal | No Gain abnormality identified in the recorded check |
| Defect Template | Did not contain the observed coordinates | Active compensation gap supported |
| Defect recalibration | New template generated and loaded | Corrective template action applied |
| Post-correction image | Visible points disappeared | Active template correction was effective |
| Dark image / raw pixel values | Not attached | Underlying pixel response not independently characterized |

---

# 6. FAE Investigation

## Step 1 — Confirm Fixed Coordinates in RAW

Result:

- multiple RAW images showed the same point coordinates.

Finding:

The event entered the fixed-pattern / pixel-correction branch rather than the random-noise branch.

---

## Step 2 — Check Dark / Offset Path

Recorded result:

- Offset Template reported normal.

Evidence boundary:

A template being reported normal does not prove that the affected raw pixel response is normal. Future Cases should preserve Dark/Offset images and coordinate-level comparison.

---

## Step 3 — Check Gain Path

Recorded result:

- Gain Template reported normal.

Finding:

No Gain-related abnormality was identified in the recorded investigation.

---

## Step 4 — Check Active Defect Template

Finding:

- the observed coordinates were not included in the active Defect Template.

This is the strongest directly supported failure condition in the Case.

---

## Step 5 — Regenerate and Load Defect Compensation

Action:

1. perform Defect Calibration according to the approved product procedure;
2. generate a new Defect Template;
3. verify that the intended template is loaded for the active configuration;
4. repeat acquisition using the original condition.

Result:

- visible fixed dark points disappeared.

---

# 7. Current Conclusion

## Verified Findings

- dark points remained at fixed detector coordinates across repeated RAW acquisitions;
- Offset and Gain templates were reported normal;
- the active Defect Template did not include the observed coordinates;
- a new Defect Template was generated and loaded;
- the visible artifact disappeared after correction.

## Root Cause

Not Fully Confirmed.

## Supported Failure Condition

The active Defect Template did not compensate the observed fixed coordinates.

## Suspected Mechanism

Fixed pixel-response abnormality or stale/incomplete defect mapping required updated Defect compensation.

The Case does not prove that the detector itself had no underlying pixel abnormality; it proves that replacement was unnecessary for the recorded event after software/calibration compensation restored the output.

---

# 8. Corrective Action

Recorded corrective path:

- perform approved Defect Calibration;
- generate/update the Defect Template;
- verify template load state and applicable configuration;
- repeat acquisition under the original condition.

Do not regenerate Defect data solely because any dark point is visible. First confirm fixed coordinates and rule out random, row/column, processing, or object-dependent artifacts.

---

# 9. Verification

Recorded result:

- fixed dark points disappeared;
- repeated acquisition was normal;
- customer confirmed recovery.

For future verification preserve:

- at least three before/after RAW images;
- Dark/Offset evidence;
- affected coordinate list;
- Defect Template version before/after;
- correction-load evidence;
- repeat acquisition result.

---

# 10. Diagnostic Lessons

- Fixed position is the primary entry criterion, not black/white polarity alone.
- RAW should be checked before relying on displayed images.
- Dark/Offset, Gain, and Defect paths provide different evidence and should not be treated as interchangeable.
- Successful Defect compensation proves the corrective path, not necessarily the absence of an underlying pixel abnormality.
- Do not immediately classify fixed dark points as detector hardware requiring return/repair.

---

# 11. Knowledge Feedback Review

| Layer | Result | Action / Reason |
|---|---|---|
| FailureKnowledge | No direct update required | PixelFailure remains the generic mechanism layer |
| DecisionTree | No direct update required | BlackDots DecisionTree remains the routing entry |
| Calibration | No direct update required | DefectCalibration remains the execution path |
| Tools | No direct update required | CalibrationTools remains the evidence/operation entry |
| Case | Updated | Direct root-cause claim replaced by template evidence and suspected mechanism |

---

# 12. Evidence Gap for Promotion to Verified

Missing evidence:

- detector SN;
- firmware/SDK versions;
- affected pixel coordinates;
- before/after RAW files;
- Dark/Offset data;
- raw pixel response values;
- Defect Template versions and mapping;
- controlled proof of the underlying pixel condition.

Without these, the Case remains `Resolved` rather than `Verified`.

---

# 13. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Batch 5 paired audit: aligned BlackDots with fixed-coordinate evidence chain, separated active compensation evidence from underlying pixel mechanism |
| V1.0 | 2026-08 | Initial Black Dots field case |