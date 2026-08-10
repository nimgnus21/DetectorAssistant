# Noise

Version: V1.1

Module: 11_Case / Image

Status: Resolved

Case Classification: Field Case Record

Evidence Level: Resolved Event Evidence — the primary event records spatially non-fixed random noise, abnormal calibration environment, recovery after controlled recalibration, and successful repeated verification. The exact environmental interference mechanism was not instrumented or independently measured.

Promotion Rule: Promote the root-cause conclusion to `Verified` only when the interfering source or calibration-input abnormality is directly evidenced and the causal relationship is confirmed by controlled comparison.

Severity: ★★★☆☆

Typical Frequency: ★★★★☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- [NoiseArtifact](../../08_ImageDiagnosis/NoiseArtifact/)
- [NoiseFailure](../../07_FailureKnowledge/ImageFailure/NoiseFailure.md)
- [Noise DecisionTree](../../09_DecisionTree/Image/Noise.md)
- [Calibration SOP](../../10_SOP/Calibration.md)
- [ImageTroubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

The primary record describes one field event: excessive spatially random image noise after calibration on a Pluto1717 installation, with non-fixed noise behavior, abnormal calibration environment, recovery after recalibration, and repeated customer verification.

The original file also contained a separate Mercu1724 anti-scatter grid installation case, duplicated as both `Case 03` and `Field Experience 01`. That experience describes image non-uniformity caused by an external imaging component and is not a Noise case.

The Grid material is intentionally removed from this Noise record to prevent incorrect symptom-to-root-cause retrieval. It should be retained or reconstructed as an independent external-system / image-uniformity Case only if a proper event-level record and evidence boundary are available.

---

# 2. Case Summary

## Case Name

Excessive Spatially Random Image Noise After Calibration

## Case Boundary

This Case applies to image noise with changing spatial locations across repeated acquisitions.

It does not represent:

- fixed defective pixels;
- fixed row/column artifacts;
- periodic interference patterns;
- image transfer corruption;
- anti-scatter grid orientation or general image non-uniformity.

Primary routing: [Noise DecisionTree](../../09_DecisionTree/Image/Noise.md).

---

# 3. Customer Environment

Product:

- Pluto1717

Detector Status:

- New Installation

Operation:

- Offset Calibration completed;
- Gain Calibration completed.

Environment:

- Hospital DR Room.

Evidence limitations:

- detector SN not preserved;
- SDK / firmware version not preserved;
- calibration timestamp not preserved;
- environmental interference source was not instrumented or measured;
- before/after RAW and noise statistics are not attached.

---

# 4. Fault Description

Customer reported:

- detector could acquire images normally;
- the image contained a large amount of random noise;
- abnormal points did not remain at fixed detector coordinates;
- after repeated exposure, the apparent noise positions changed.

Initial customer concern:

- large number of detector defective pixels.

Initial FAE classification:

- random / non-fixed noise candidate;
- fixed Defect mechanism not supported by the observed spatial behavior.

---

# 5. Evidence Classification

| Evidence | Observation | Supported Finding |
|---|---|---|
| Detector communication | Normal | Communication failure was not observed in the recorded event |
| Image acquisition | Successful | Detector could complete acquisition |
| Defect Template | Loaded; defect count reported normal | Large fixed-pixel defect pattern was not supported |
| Repeated images | Noise location changed | Spatially non-fixed/random behavior supported |
| Consecutive dark images | Random noise pattern changed between acquisitions | Fixed detector-coordinate defect was not supported |
| Calibration environment | Abnormal interference reported during Offset Calibration | Calibration-input/environment issue became a candidate path |
| Recalibration | Offset and Gain recalibration completed after interference handling | Corrective action applied |
| Verification | Noise returned to normal; repeated acquisition passed | Resolution supported |
| Interference measurement | Not preserved | Exact environmental mechanism not verified |

Important boundary:

Changing noise positions support a random/temporal-noise branch, but do not by themselves prove that calibration was the sole cause.

---

# 6. Troubleshooting Timeline

## Step 1 — Confirm Detector Communication and Acquisition

Result:

- detector communication normal;
- image acquisition successful.

Finding:

No communication failure was recorded in this event.

---

## Step 2 — Check Defect Template and Fixed-Pixel Evidence

Observed:

- Defect Template loaded normally;
- defect count reported within the expected range;
- noise did not remain at fixed pixel coordinates.

Finding:

The recorded evidence did not support a large fixed Defect population as the primary explanation.

---

## Step 3 — Compare Consecutive Dark Images

Observation:

- random noise locations changed between acquisitions;
- the same detector coordinates were not persistently abnormal.

Finding:

Spatially non-fixed/random behavior was confirmed.

Recommended evidence for future Cases:

- preserve multiple RAW/dark images;
- record acquisition timestamps;
- compare fixed-pattern versus temporal variation;
- calculate applicable image statistics where tools are available.

---

## Step 4 — Review Calibration Conditions

Investigation found:

- abnormal environmental interference was present during Offset Calibration.

Evidence boundary:

The specific interference source was not preserved or measured. Therefore the record supports an abnormal calibration environment as a strong candidate, not a fully verified physical mechanism.

---

## Step 5 — Controlled Corrective Recalibration

After removing or avoiding the identified abnormal environmental condition:

1. perform Offset Calibration using the approved procedure;
2. perform Gain Calibration where required by the applicable product workflow;
3. preserve calibration completion results;
4. repeat representative image acquisition.

Result:

- image noise returned to normal appearance.

---

# 7. Current Conclusion

## Verified Findings

- image noise was spatially non-fixed across repeated acquisitions;
- detector communication and acquisition were normal;
- Defect Template was loaded and no large abnormal fixed-defect pattern was reported;
- abnormal environmental interference was reported during Offset Calibration;
- recalibration after environmental handling was followed by normal image quality;
- repeated customer acquisition verification passed.

## Root Cause

Not Fully Confirmed.

## Supported Finding

The recorded event is consistent with abnormal calibration input/environment contributing to increased random image noise.

## Suspected Failure Mechanism

Abnormal Offset calibration data caused by environmental interference or unstable calibration conditions, resulting in increased residual/random image noise.

The exact interference source and causal mechanism were not measured in the current Case.

---

# 8. Resolution

Recorded corrective path:

- identify and remove/avoid abnormal environmental interference;
- repeat Offset Calibration according to the approved procedure;
- repeat Gain Calibration where required;
- verify image quality under the original operating condition.

The Case does not establish that all random noise should be solved by recalibration. If noise remains unchanged after controlled calibration, continue through the relevant Noise DecisionTree branches for:

- exposure/generator variation;
- power/environmental interference;
- temporal detector behavior;
- transfer/processing path;
- other product-specific causes.

---

# 9. Verification

Recorded result:

- image noise returned to normal;
- no obvious random abnormality remained;
- image uniformity returned to normal appearance;
- customer continuous-acquisition verification passed.

For future Cases, verification should preserve:

- before/after RAW and corrected images;
- repeated acquisition count;
- calibration logs;
- environment record;
- exposure conditions;
- noise statistics where available.

---

# 10. Diagnostic Lessons

- Random noise and fixed Defect should be separated before selecting a correction path.
- Spatial position is an important diagnostic discriminator: fixed-pattern versus changing-pattern behavior.
- A successful recalibration proves that the corrective path was effective, but does not automatically prove the exact physical source of the original noise.
- Preserve calibration environment evidence before recalibration whenever possible.
- Do not regenerate a Defect Template solely because random noise is visible.
- Image non-uniformity caused by external components such as an anti-scatter grid belongs to a different diagnostic category.

---

# 11. Knowledge Feedback Review

| Layer | Result | Action / Reason |
|---|---|---|
| FailureKnowledge | No direct update required | [NoiseFailure](../../07_FailureKnowledge/ImageFailure/NoiseFailure.md) remains the generic mechanism layer |
| DecisionTree | No direct update required | Existing Noise DecisionTree remains the correct routing entry |
| SOP | No direct update required | Existing calibration/image troubleshooting procedures remain applicable |
| Tools | Evidence enhancement recommended | CalibrationTools can support future calibration evidence preservation |
| Case | Updated | Retained one primary Noise event and removed unrelated duplicated Grid experience |
| External-system Case | Follow-up required | Grid installation event should be independently admitted before reuse |

---

# 12. Evidence Gap for Promotion to Verified

Missing evidence:

- detector SN;
- SDK / firmware versions;
- calibration logs and exact parameter set;
- before/after RAW and dark images;
- noise statistics;
- measured interference source;
- controlled comparison isolating the environmental variable.

Without these, the Case remains `Resolved` rather than `Verified`.

---

# 13. Related Documents

- [NoiseArtifact](../../08_ImageDiagnosis/NoiseArtifact/)
- [NoiseFailure](../../07_FailureKnowledge/ImageFailure/NoiseFailure.md)
- [Noise DecisionTree](../../09_DecisionTree/Image/Noise.md)
- [Calibration SOP](../../10_SOP/Calibration.md)
- [ImageTroubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 14. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Batch 5 admission audit: retained primary random-noise event, changed status to Resolved, separated evidence from suspected mechanism, removed duplicated unrelated Grid experience |
| V1.0 | 2026-08 | Initial Noise field case |