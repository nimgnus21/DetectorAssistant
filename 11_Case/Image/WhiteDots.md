# WhiteDots

Version: V1.1

Module: 11_Case / Image

Status: Resolved

Case Classification: Field Case Record

Evidence Level: Resolved Event Evidence — repeated RAW images showed fixed detector-coordinate bright points, Offset/Gain templates were reported normal, the active Defect Template was identified as an old version after recalibration, and updating defect compensation removed the visible artifact. The underlying pixel condition was not independently characterized.

Promotion Rule: Promote the mechanism to `Verified` only when coordinate-level raw response, calibration/template version lineage, active load state, and controlled before/after evidence establish the cause.

Severity: ★★★☆☆

Typical Frequency: ★★★★☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- [WhiteDotsArtifact](../../08_ImageDiagnosis/WhiteDotsArtifact/)
- [PixelFailure](../../07_FailureKnowledge/ImageFailure/PixelFailure.md)
- [WhiteDots DecisionTree](../../09_DecisionTree/Image/WhiteDots.md)
- [DefectCalibration](../../05_Calibration/DefectCalibration.md)
- [Calibration SOP](../../10_SOP/Calibration.md)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

This record contains a concrete field event with repeated fixed-coordinate RAW evidence, calibration/template history, a corrective action, and successful verification. It remains a Case.

The original root-cause statement asserted that the detector continued using an old Defect Template after calibration data changed. The recorded evidence supports this as the strongest failure condition: the active Defect Template was old and correction with updated data removed the artifact. The Case does not independently prove that every underlying bright pixel response was caused by template age alone.

---

# 2. Case Summary

## Case Name

Fixed Bright Points Caused by Stale or Inapplicable Defect Compensation

## Case Boundary

This Case applies to bright/white points that:

- remain at the same detector coordinates across repeated acquisitions;
- remain independent of the imaged object in the recorded event;
- persist after exposure parameter changes in the recorded event;
- are associated with active calibration/template inconsistency.

It does not represent:

- random changing bright noise;
- saturation caused by exposure conditions;
- fixed row/column artifacts;
- display-only processing artifacts.

---

# 3. Customer Environment

Customer Type:

- Hospital

Product:

- Pluto1717

Application:

- General Radiography

Detector Status:

- In Service

Evidence limitations:

- detector SN not preserved;
- firmware/SDK version not preserved;
- exact calibration change date not preserved;
- Defect Template version identifiers not preserved;
- affected coordinates not recorded;
- before/after RAW and Dark/Offset evidence not attached.

---

# 4. Fault Description

Customer reported multiple fixed white/bright points in the image.

Observed characteristics:

- point positions were fixed;
- every exposure showed the same coordinates;
- exposure parameter changes did not remove the points;
- changing the imaged object did not remove the points.

Initial customer concern:

- large number of detector bad pixels requiring factory repair.

FAE diagnostic direction:

- classify fixed-coordinate behavior first;
- compare RAW, Dark/Offset, Gain, and active Defect Template before deciding return/repair.

---

# 5. Evidence Classification

| Evidence | Observation | Supported Finding |
|---|---|---|
| Repeated RAW | Same bright coordinates | Fixed detector-coordinate behavior supported |
| Offset Template | Reported normal | No Offset abnormality identified in the recorded check |
| Gain Template | Reported normal | No Gain abnormality identified in the recorded check |
| Calibration history | Detector had been recalibrated | Configuration/calibration lineage changed |
| Active Defect Template | Old version still in use | Template lineage/load inconsistency supported |
| Defect recalibration | New template generated and loaded | Corrective compensation updated |
| Post-correction image | Bright points disappeared | Updated compensation effective |
| Dark/raw response | Not attached | Underlying pixel mechanism not independently characterized |

---

# 6. FAE Investigation

## Step 1 — Confirm Fixed Coordinates in RAW

Result:

- multiple RAW images showed the same bright coordinates.

Finding:

The event entered the fixed-pattern / pixel-correction branch rather than the random-noise branch.

---

## Step 2 — Check Dark / Offset Path

Recorded result:

- Offset Template reported normal.

Evidence boundary:

Future Cases should preserve Dark/Offset images and coordinate-level comparison. A normal template status alone does not prove normal raw pixel response.

---

## Step 3 — Check Gain Path

Recorded result:

- Gain Template reported normal.

Finding:

No Gain-related abnormality was identified in the recorded investigation.

---

## Step 4 — Check Calibration and Defect Template Lineage

Finding:

- detector had undergone recalibration;
- the active Defect Template remained an older version and had not been synchronized with the current calibration state.

This is the strongest directly supported failure condition in the Case.

---

## Step 5 — Regenerate and Load Defect Compensation

Action:

1. perform Defect Calibration according to the approved product procedure;
2. generate/update the Defect Template;
3. verify that the intended template is loaded for the active configuration;
4. repeat acquisition using the original condition.

Result:

- fixed bright points disappeared.

---

# 7. Current Conclusion

## Verified Findings

- bright points remained at fixed detector coordinates across repeated RAW acquisitions;
- Offset and Gain templates were reported normal;
- detector calibration state had changed;
- an old Defect Template remained active;
- updated Defect compensation was generated and loaded;
- the visible artifact disappeared after the correction.

## Root Cause

Not Fully Confirmed.

## Supported Failure Condition

The active Defect Template was stale or inconsistent with the current calibration state and did not correctly compensate the observed coordinates.

## Suspected Mechanism

Fixed pixel-response abnormality or calibration/template lineage mismatch required updated Defect compensation.

The Case proves that correcting the active compensation restored output. It does not independently prove that the detector had no underlying pixel abnormality.

---

# 8. Corrective Action

Recorded corrective path:

- perform approved Defect Calibration;
- generate/update the Defect Template;
- verify template version/load state and applicable configuration;
- repeat acquisition under the original condition.

Do not treat every bright point as a Defect Template issue. First distinguish fixed detector-coordinate behavior from random noise, saturation, row/column artifacts, and display processing.

---

# 9. Verification

Recorded result:

- fixed bright points disappeared;
- image uniformity returned to normal appearance;
- repeated acquisition was normal;
- customer confirmed recovery.

For future verification preserve:

- at least three before/after RAW images;
- Dark/Offset evidence;
- affected coordinate list;
- calibration/template version lineage;
- active template load evidence;
- repeat acquisition result.

---

# 10. Diagnostic Lessons

- Fixed position is the primary entry criterion; bright polarity alone is not a root cause.
- RAW evidence should be checked before relying on displayed output.
- Calibration/template version lineage is a critical diagnostic dimension after recalibration.
- Offset, Gain, and Defect evidence should be checked as separate layers.
- Successful compensation proves that the active correction path was effective, not necessarily that no underlying pixel abnormality existed.
- Random bright points should enter the Noise branch rather than the fixed-pixel branch.

---

# 11. Knowledge Feedback Review

| Layer | Result | Action / Reason |
|---|---|---|
| FailureKnowledge | No direct update required | PixelFailure remains the generic mechanism layer |
| DecisionTree | No direct update required | WhiteDots DecisionTree remains the routing entry |
| Calibration | No direct update required | DefectCalibration remains the execution path |
| Tools | No direct update required | CalibrationTools remains the evidence/operation entry |
| Case | Updated | Direct hardware-exclusion claim replaced by template-lineage evidence and suspected mechanism |

---

# 12. Evidence Gap for Promotion to Verified

Missing evidence:

- detector SN;
- firmware/SDK versions;
- affected pixel coordinates;
- before/after RAW files;
- Dark/Offset data;
- raw pixel response values;
- exact calibration/template version lineage;
- active template load record;
- controlled proof of the underlying pixel condition.

Without these, the Case remains `Resolved` rather than `Verified`.

---

# 13. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Batch 5 paired audit: aligned WhiteDots with fixed-coordinate evidence chain and template-lineage verification model |
| V1.0 | 2026-08 | Initial White Dots field case |