# HorizontalLine

Version: V1.1

Module: 11_Case / Image

Status: Resolved

Case Classification: Field Case Record

Evidence Level: Resolved — the event-level symptom, diagnostic observations, corrective path, and post-repair verification are recorded. The exact failed Row Readout hardware mechanism is not independently documented.

Promotion Rule: Promote the root-cause conclusion to `Verified` only when hardware/return analysis, component diagnosis, or equivalent technical evidence confirms the specific failed mechanism.

Severity: ★★★★★

Typical Frequency: ★★★★☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- [HorizontalLineArtifact](../../08_ImageDiagnosis/HorizontalLineArtifact/)
- [RowFailure](../../07_FailureKnowledge/ImageFailure/RowFailure.md)
- [HorizontalLine DecisionTree](../../09_DecisionTree/Image/HorizontalLine.md)
- [TFTReadout](../../13_Principles/TFTReadout/)
- [GateDriver](../../13_Principles/GateDriver/)
- [ImageTroubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)
- [Offset Calibration](../../10_SOP/Calibration.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

This record contains a concrete product, operating scenario, observed symptom, actual diagnostic sequence, corrective disposition, and post-repair verification. It therefore remains a Case record.

However, the available evidence supports the following conclusion:

> A persistent fixed-row artifact was observed in corrected images, dark images, and multiple RAW images, and the symptom was resolved after hardware repair.

The available record does **not** independently document the exact failed electronic component or Row Readout channel. Therefore:

- `Status: Resolved`
- `Verified Root Cause: Not Fully Confirmed`
- `Suspected Failure Mechanism: Row Readout Path / related hardware`

The symptom evidence is stronger than the mechanism evidence.

---

# 2. Case Summary

## Case Name

Persistent Horizontal Line Appears Across the Entire Image

## Case Boundary

This Case describes a persistent fixed-position horizontal line. It must not be used as a universal root-cause template for all horizontal stripe artifacts.

For other horizontal-line patterns, first distinguish:

- fixed row artifact;
- repeating periodic stripe;
- calibration-related stripe;
- communication/image-transfer corruption;
- exposure/generator-related artifact;
- transient or environment-dependent interference.

Primary routing: [HorizontalLine DecisionTree](../../09_DecisionTree/Image/HorizontalLine.md).

---

# 3. Customer Environment

Customer:

- Orthopedic Hospital

Product:

- Pluto1717

Operation:

- Static Radiography

Detector:

- Wired Ethernet Detector

Recorded environment limitation:

- exact detector SN not preserved in the current Case;
- software / SDK / firmware versions are not recorded;
- repair report or hardware analysis result is not attached.

These missing records prevent promotion of the failure mechanism to `Verified`.

---

# 4. Fault Description

Customer reported a persistent bright horizontal line extending across the image width.

Observed characteristics:

- present on every exposure;
- fixed row position;
- no visible change after exposure-parameter change;
- no visible change after changing the imaged object;
- remained after application restart.

Initial FAE finding:

- fixed-row artifact;
- Row Readout path considered a candidate mechanism requiring further confirmation.

---

# 5. Evidence Classification

| Evidence | Observation | Supported Finding |
|---|---|---|
| Detector communication | Online; no Image Loss; no Timeout recorded | Communication failure was not supported by the recorded event |
| Offset reacquisition | No improvement | Simple Offset reacquisition did not remove the artifact |
| Template reload | No improvement | Reloading Offset/Gain/Defect templates did not remove the artifact |
| Dark image | Same row-position anomaly remained | Artifact was not dependent on normal exposure content |
| Multiple RAW images | Anomaly remained at the same row coordinate | Persistent fixed-row pattern supported |
| Hardware repair | Symptom disappeared after repair | Hardware intervention was associated with recovery |
| Repair analysis | Not preserved | Exact failed hardware mechanism not verified |

Important boundary:

The evidence supports a persistent detector-side or readout-related candidate path, but does not identify a specific component solely from image morphology.

---

# 6. Troubleshooting Timeline

## Step 1 — Check Communication State

Observed:

- Detector Online;
- no Image Loss recorded;
- no Timeout recorded.

Result:

The recorded event did not support communication interruption as the primary explanation.

---

## Step 2 — Reacquire Offset

Action:

- reacquire Offset according to the applicable calibration procedure.

Result:

- horizontal line remained.

Finding:

Simple Offset reacquisition did not resolve the artifact.

---

## Step 3 — Reload Existing Correction Templates

Reloaded:

- Offset Template;
- Gain Template;
- Defect Template.

Result:

- no visible improvement.

Finding:

The recorded template reload path did not remove the artifact.

---

## Step 4 — Acquire Dark Image

Observation:

- the anomaly remained at the same row position.

Finding:

The event evidence did not support normal exposure content as the direct source of the fixed-row artifact.

This does not, by itself, prove a specific readout component failure.

---

## Step 5 — Compare Multiple RAW Images

Observation:

- the anomaly remained at the same row coordinate across multiple RAW images.

Finding:

- persistent fixed-row abnormality confirmed.

Required record for future Cases:

- affected RAW files;
- row coordinate;
- image dimensions / binning / ROI;
- acquisition mode;
- timestamp and detector/software version.

---

## Step 6 — Failure Mechanism Assessment

Based on the fixed-row pattern, dark-image persistence, and RAW consistency:

- suspected mechanism: Row Readout Path or related detector-side hardware;
- confidence: diagnostic candidate, not independently verified root cause.

Recommended next action:

- preserve RAW and corrected images;
- record abnormal row coordinate;
- verify whether an applicable defect-correction mechanism can safely compensate for the defect;
- submit the evidence package for hardware/R&D analysis when the artifact cannot be corrected within product requirements.

---

# 7. Current Conclusion

## Verified Findings

The following findings are supported by the Case record:

- a horizontal artifact occurred at a fixed row position;
- the artifact persisted across repeated exposures;
- the artifact persisted after Offset reacquisition and template reload;
- the artifact was visible in a dark image at the same row position;
- the artifact was visible in multiple RAW images at the same row coordinate;
- the symptom disappeared after hardware repair and controlled post-repair verification.

## Root Cause

Not Fully Confirmed.

## Suspected Failure Mechanism

Row Readout Path abnormality or related detector-side hardware abnormality.

This mechanism must remain explicitly marked as suspected until supported by:

- hardware diagnostic result;
- return/factory analysis;
- component-level repair record;
- or equivalent technical confirmation.

For general mechanism reference, see [RowFailure](../../07_FailureKnowledge/ImageFailure/RowFailure.md).

---

# 8. Resolution

Field handling:

- preserve RAW images;
- record the abnormal row coordinate;
- verify whether the applicable Defect Template path can correct the artifact within product requirements;
- if correction is ineffective or outside the supported compensation boundary, submit the detector for further hardware/R&D analysis;
- complete hardware repair through the approved service path.

The Case does not establish that every fixed-row artifact requires the same repair action.

---

# 9. Verification

After repair, the following were recorded:

- horizontal line disappeared;
- image uniformity returned to normal appearance;
- dark image no longer showed the fixed-row artifact;
- repeated exposure verification was normal.

Current Case result:

`Resolved`.

Additional verification required for future similar Cases:

- preserve before/after images;
- record test count and acquisition conditions;
- confirm whether the same detector configuration and correction templates were used;
- attach repair analysis where available.

---

# 10. Diagnostic Lessons

- A fixed-position horizontal line should first be classified as a phenomenon, not immediately as a root cause.
- Persistence in dark images and RAW images is strong evidence for a detector/readout-side candidate path.
- Failure of Offset reacquisition or template reload does not by itself prove hardware failure, but it is useful branch evidence.
- Repeated calibration should not replace evidence collection.
- Record the abnormal row coordinate to support later R&D/hardware correlation.
- Do not generalize this Case to periodic horizontal stripes or transfer corruption without checking the appropriate DecisionTree branches.

---

# 11. Knowledge Feedback Review

| Layer | Checked Entry | Result | Action / Reason |
|---|---|---|---|
| FailureKnowledge | [RowFailure](../../07_FailureKnowledge/ImageFailure/RowFailure.md) | No update required | Existing mechanism reference already covers the candidate path; this Case does not add a verified component-level mechanism |
| DecisionTree | [HorizontalLine](../../09_DecisionTree/Image/HorizontalLine.md) | No update required | Existing DecisionTree remains the correct entry; this Case reinforces fixed-position / dark / RAW evidence usage |
| SOP | [ImageTroubleshooting](../../10_SOP/ImageTroubleshooting.md) | No update required | No new universal step was verified |
| Calibration SOP | [Calibration](../../10_SOP/Calibration.md) | No update required | Offset/template failure is Case evidence, not a new calibration procedure |
| Tools | Existing image/RAW evidence tools | Additional evidence recommended | Future Case should preserve RAW and coordinate metadata |
| ErrorCode | Not applicable | No update required | No error-code event established |
| Index | Case retained | Update not required | Existing HorizontalLine search entry remains valid; status is now Resolved |

---

# 12. Evidence Gap for Promotion to Verified

The following evidence is missing from the current record:

- detector SN;
- software / SDK / firmware version;
- original RAW and dark images;
- abnormal row coordinate;
- repair report;
- confirmed failed component or circuit;
- before/after configuration record.

Without this evidence, the Case remains `Resolved` rather than `Verified`.

---

# 13. Related Documents

- [HorizontalLineArtifact](../../08_ImageDiagnosis/HorizontalLineArtifact/)
- [RowFailure](../../07_FailureKnowledge/ImageFailure/RowFailure.md)
- [HorizontalLine DecisionTree](../../09_DecisionTree/Image/HorizontalLine.md)
- [ImageTroubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)
- [Calibration SOP](../../10_SOP/Calibration.md)
- [TFTReadout](../../13_Principles/TFTReadout/)
- [GateDriver](../../13_Principles/GateDriver/)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 14. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Batch 5 admission audit: retained as field Case, changed status to Resolved, separated verified findings from suspected Row Readout mechanism, added evidence gaps and knowledge feedback |
| V1.0 | 2026-08 | Initial horizontal-line field case |