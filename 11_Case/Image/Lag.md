# Lag

Version: V1.1

Module: 11_Case / Image

Status: Mixed Reference

Case Classification: Primary Lag Event + Misclassified Related Field Experiences

Evidence Level: Mixed — the primary event supports a temporal Lag-like recovery pattern after long continuous exposure. The appended first-frame gray-value and exposure-synchronization records describe different failure phenomena and must not be treated as Lag root-cause evidence.

Promotion Rule: A Lag mechanism may be promoted to `Verified` only when the temporal decay pattern, exposure history, acquisition conditions, and product-specific technical analysis support the mechanism beyond symptom classification.

Severity: ★★★★☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Dynamic Flat Panel Detector
- Static Flat Panel Detector where applicable after high-dose exposure
- Pluto Series

Related Documents:

- [LagArtifact](../../08_ImageDiagnosis/LagArtifact/)
- [LagFailure](../../07_FailureKnowledge/ImageFailure/LagFailure.md)
- [Lag DecisionTree](../../09_DecisionTree/Image/Lag.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

This file contains three different evidence types:

1. Primary Case — residual image gradually decays after long continuous/high-dose exposure.
2. Experience 02 — first acquired image has low gray value while subsequent images normalize.
3. Experience 03 — first-image/acquisition instability associated with exposure synchronization timing.

Only the first record belongs to the Lag diagnostic family. The latter two must not be used as evidence that a Lag mechanism occurred.

The file is therefore retained as a `Mixed Reference` until the non-Lag experiences are moved into independent Case records or another appropriate category.

---

# 2. Primary Lag Case Summary

## Case Name

Gradually Decaying Residual Artifact After Long Continuous Exposure

## Product / Environment

Product:

- Pluto Dynamic Detector

Application:

- Dynamic Fluoroscopy

Exposure:

- Long Continuous Exposure

SDK:

- SDK_AIO

Evidence limitations:

- detector SN not preserved;
- firmware/SDK version boundary incomplete;
- exposure dose/time values not recorded;
- original image sequence and decay duration are not attached.

---

# 3. Primary Fault Description

Customer reported that after continuous exposure stopped, image abnormality required several seconds to gradually return to normal.

Observed characteristics:

- higher-gray/high-contrast regions recovered more slowly than other regions;
- residual intensity decayed over time;
- the image did not remain as a fixed copy of one previous frame;
- the customer initially considered Ghost.

This record supports temporal decay as the key diagnostic feature.

---

# 4. Evidence Classification

| Evidence | Observation | Supported Finding |
|---|---|---|
| Communication | Normal | No communication failure recorded |
| Image Loss / Timeout | Not found | No transfer interruption recorded in the Case |
| Ghost correction state | Template loaded; Ghost calibration reported normal | Ghost correction configuration failure was not supported by the record |
| Image sequence | Residual gradually weakened after exposure stopped | Temporal decay pattern supported |
| Prior-frame copy | Not reported as a fixed retained frame | Pure previous-frame retention was not supported |
| Recovery | Subsequent acquisition returned to normal | Symptom resolved over recovery time |
| Exposure/dose measurement | Not preserved | Exposure-dependent mechanism not quantitatively verified |

---

# 5. Troubleshooting Timeline

## Step 1 — Check Communication State

Result:

- normal.

## Step 2 — Check Image Loss and Timeout

Result:

- no abnormal event recorded.

## Step 3 — Check Ghost Correction State

Result:

- Ghost Template reported loaded;
- Ghost Calibration reported normal.

Finding:

The recorded event did not support a simple missing-Ghost-template explanation.

## Step 4 — Observe Temporal Behavior

During continuous dynamic acquisition, after X-Ray stopped:

- residual image gradually weakened;
- abnormality did not remain as a fixed unchanged copy of a prior frame.

## Step 5 — Phenomenon Classification

Based on the recorded temporal decay pattern:

- Lag was the primary diagnostic classification.

Evidence boundary:

Phenomenon classification does not independently prove a specific pixel-level recovery mechanism.

---

# 6. Current Conclusion

## Verified Findings

- the abnormality followed long continuous exposure in the recorded event;
- communication was normal;
- no Image Loss/Timeout was recorded;
- Ghost correction/template state was reported normal;
- residual intensity gradually decayed after exposure stopped;
- subsequent acquisition returned to normal.

## Root Cause

Not Fully Confirmed.

## Supported Classification

Lag-like temporal residual behavior.

## Suspected Mechanism

Exposure-history-dependent detector temporal response / pixel recovery behavior, consistent with the generic mechanism described in [LagFailure](../../07_FailureKnowledge/ImageFailure/LagFailure.md).

The current Case does not contain dose, timing, or technical analysis sufficient to verify the exact mechanism.

---

# 7. Resolution and Verification

Recorded handling:

- stop the continuous exposure;
- allow the detector/image response to recover;
- review exposure conditions;
- perform additional correction verification only when indicated by the diagnostic branch.

Recorded verification:

- image gradually returned to normal;
- no fixed residual remained;
- subsequent acquisition was normal;
- detector operation was reported normal.

A future verified Lag Case should preserve a multi-frame sequence and quantify:

- exposure duration;
- dose or applicable exposure parameters;
- recovery time;
- residual decay across frames;
- repeatability.

---

# 8. Associated Experience 02 — First-Frame Low Gray Value

Source:

- FAE Pre-sales Weekly Report

Observed pattern:

- first acquired image has noticeably lower gray value;
- subsequent images return to normal;
- issue can recur after application restart.

Recorded investigation:

- detector communication normal;
- Offset/Gain calibration passed;
- firmware reported compatible;
- generator output reported stable.

Candidate branches:

- detector/application initialization sequence;
- startup state;
- exposure synchronization timing;
- generator trigger timing.

Classification boundary:

This is **not classified as Lag** based on the available record. It should be routed to a first-frame / initialization / synchronization Case or DecisionTree branch.

---

# 9. Associated Experience 03 — Exposure Synchronization Timing

Source:

- FAE Pre-sales Weekly Report

Observed pattern:

- communication normal;
- trigger received;
- first image abnormal or acquisition initially unstable;
- continuous acquisition later normal.

Recorded candidate conclusion:

- generator and detector exposure synchronization were not properly matched.

Classification boundary:

This is **not a Lag Case**. It belongs to exposure synchronization / first-frame acquisition diagnostics and should not be used to infer pixel temporal recovery behavior.

---

# 10. Diagnostic Lessons

- Lag and Ghost are different diagnostic phenomena.
- A gradually decaying residual pattern is stronger evidence for a Lag-like path than a fixed copy of one prior frame.
- First-frame-only gray-value abnormalities should not automatically be classified as Lag.
- Exposure synchronization problems can mimic temporal image abnormalities but require a separate trigger/acquisition diagnostic path.
- Do not recalibrate or replace hardware before classifying the temporal behavior and preserving evidence.

---

# 11. Knowledge Feedback Review

| Layer | Result | Action / Reason |
|---|---|---|
| FailureKnowledge | No direct update required | LagFailure remains the generic mechanism reference |
| DecisionTree | Follow-up required | First-frame and exposure-synchronization records need independent routing rather than Lag reuse |
| SOP | No direct update required | No new verified universal procedure extracted |
| Case | Reclassified | Primary Lag event retained; two non-Lag experiences explicitly separated |
| Tools | No direct update required | Current record does not establish a new tool requirement |

---

# 12. Required Follow-up

The following associated experiences should be considered for future extraction into independent records:

1. First-frame low gray value after initialization.
2. Exposure synchronization timing causing first-frame/acquisition abnormality.

Until independent evidence is available, they remain associated references only and must not be counted as Lag cases.

---

# 13. Evidence Gap for Promotion to Verified Lag Case

Missing evidence:

- detector identifier;
- exact SDK/firmware versions;
- exposure duration/dose or applicable exposure parameters;
- before/during/after image sequence;
- quantified recovery time;
- repeatability test;
- technical analysis confirming the underlying temporal response mechanism.

---

# 14. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Batch 5 admission audit: retained primary Lag event, explicitly separated two non-Lag experiences, added temporal evidence boundary and extraction follow-up |
| V1.0 | 2026-08 | Initial Lag Artifact field case |