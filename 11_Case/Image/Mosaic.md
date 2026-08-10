# Mosaic

Version: V1.1

Case ID: CASE-IMG-009

Module: 11_Case / Image

Status: Resolved

Case Classification: Field Case Record

Evidence Level: Resolved Event Evidence — the recorded event shows random-position Mosaic artifacts, intermittent Image Loss, high-frame-rate sensitivity, incomplete network configuration, improvement after network configuration changes, and final recovery after network driver update. The exact packet-loss mechanism was not preserved through packet capture or quantitative network counters.

Promotion Rule: Promote the root cause to `Verified` only when packet loss, fragmentation, retransmission, receiver drop, or another specific transport failure is directly demonstrated and correlated with the affected acquisition.

Severity: ★★★★★

Typical Frequency: ★★★☆☆

Applicable Products:

- Pluto Series
- Wired Dynamic Detector
- Wired Static Detector

Related Documents:

- [MosaicArtifact](../../08_ImageDiagnosis/MosaicArtifact/)
- [MosaicFailure](../../07_FailureKnowledge/ImageFailure/MosaicFailure.md)
- [Mosaic DecisionTree](../../09_DecisionTree/Image/Mosaic.md)
- [NetworkConfiguration SOP](../../10_SOP/NetworkConfiguration.md)
- [CommunicationWorkflow](../../06_Workflow/CommunicationWorkflow.md)
- [Ping](../../17_Tools/Ping/)
- [Wireshark](../../17_Tools/Wireshark/)
- [Log Viewer](../../17_Tools/Log%20Viewer/)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

This record contains a concrete field event with product, communication mode, repeatable symptom characteristics, a documented diagnostic sequence, configuration changes, and successful post-change verification. It therefore remains a Case.

However, the original title and root-cause statement directly asserted that Ethernet packet loss caused the Mosaic image. The preserved record does not include a Wireshark capture, NIC error counter, packet-loss measurement, or another direct transport-layer proof.

The Case therefore supports:

- Mosaic artifact occurred during acquisition;
- artifact position was random/intermittent;
- high frame rate increased occurrence;
- `Image Loss` appeared intermittently;
- network configuration was incomplete relative to the recorded detector requirement;
- corrective network changes reduced the symptom;
- NIC driver update was followed by full recovery.

It does not independently prove one specific packet-loss mechanism.

---

# 2. Case Summary

## Case Name

Intermittent Random Mosaic Artifact During Continuous Ethernet Acquisition

## Case Boundary

This Case applies to Mosaic-like image corruption with changing block position, intermittent occurrence, and evidence of acquisition/transfer abnormality.

It does not establish that all Mosaic artifacts are network failures. Other branches may include:

- image packet reassembly/reconstruction;
- host receiver performance;
- SDK/application processing;
- storage/memory corruption;
- detector-side data generation;
- product-specific transport or firmware behavior.

Primary routing: [Mosaic DecisionTree](../../09_DecisionTree/Image/Mosaic.md).

---

# 3. Customer Environment

Customer Type:

- OEM Customer

Product:

- Pluto0900X

Communication:

- Gigabit Ethernet

Working Mode:

- Continuous Acquisition

Evidence limitations:

- detector SN not preserved;
- firmware version not preserved;
- NIC model not preserved;
- original MTU/Jumbo configuration snapshot not attached;
- driver version before/after not preserved;
- no packet capture or NIC statistics attached.

---

# 4. Fault Description

Customer reported obvious Mosaic artifacts during dynamic image acquisition.

Observed characteristics:

- image blocks appeared displaced or corrupted;
- Mosaic position changed between occurrences;
- symptom was intermittent;
- high frame rate increased occurrence;
- static acquisition could occasionally be normal.

Customer initially suspected detector FPGA damage.

FAE initial diagnostic direction:

- prioritize acquisition/data-integrity evidence before concluding fixed detector hardware failure.

---

# 5. Evidence Classification

| Evidence | Observation | Supported Finding |
|---|---|---|
| Consecutive acquisition | Mosaic position changed | Random/intermittent corruption pattern supported |
| High frame rate | Symptom more likely | Load/sustained-throughput sensitivity supported |
| Static acquisition | Occasionally normal | Symptom was not universally fixed across all operating conditions |
| SDK | Intermittent `Image Loss` | Acquisition/data-completeness abnormality supported |
| Jumbo Frame | Not enabled | Host network configuration did not match the recorded required setting |
| MTU | Host default 1500 bytes; recorded detector requirement 9000 bytes | Configuration mismatch supported |
| After MTU/Jumbo change | Symptom significantly reduced | Network configuration was causally relevant to the recovery path |
| NIC driver | Recorded as outdated | Driver candidate identified |
| After driver update | Image returned to normal | Final corrective path effective |
| Wireshark/NIC counters | Not attached | Specific packet-loss mechanism not verified |

Important boundary:

`Image Loss + Mosaic` is strong routing evidence for an acquisition/transfer path, but it does not by itself prove whether the loss originated from packet loss, fragmentation, receiver drop, SDK handling, or another layer.

---

# 6. Troubleshooting Timeline

## Step 1 — Reproduce Under Continuous Acquisition

Result:

- Mosaic positions changed between occurrences;
- symptom was intermittent;
- high-frame-rate operation increased occurrence.

Finding:

The observed pattern was inconsistent with a simple fixed detector-coordinate defect.

---

## Step 2 — Check SDK/Acquisition Evidence

Observed:

- intermittent `Image Loss` events.

Finding:

The Case entered the acquisition/data-integrity branch.

Required future evidence:

- exact error/log timestamp;
- affected frame index;
- image sequence;
- correlation between `Image Loss` and Mosaic occurrence.

---

## Step 3 — Review Host Network Configuration

Recorded findings:

- Jumbo Frame not enabled;
- MTU remained at 1500 bytes;
- recorded detector configuration requirement was 9000 bytes.

Finding:

A host-to-detector network configuration mismatch was present.

Boundary:

The Case records a 9000-byte requirement for this event. Do not generalize this value to every detector without checking the applicable product configuration.

---

## Step 4 — Correct Network Configuration

Actions:

- enable the required Jumbo Frame setting;
- configure MTU according to the applicable detector requirement;
- restart/reinitialize the network interface and detector connection according to the approved procedure;
- repeat continuous acquisition.

Result:

- Mosaic occurrence was significantly reduced.

Finding:

Network configuration was relevant but was not the complete corrective path in the recorded event.

---

## Step 5 — Review and Update NIC Driver

Recorded finding:

- NIC driver was outdated.

Action:

- update the NIC driver to the approved/recommended version;
- repeat continuous acquisition under the affected operating condition.

Result:

- image returned to normal;
- no further Mosaic recorded during verification.

---

# 7. Current Conclusion

## Verified Findings

- intermittent random-position Mosaic occurred during continuous acquisition;
- high frame rate increased occurrence;
- intermittent `Image Loss` was recorded;
- Jumbo/MTU configuration did not match the recorded detector requirement;
- configuration correction significantly reduced the symptom;
- NIC driver update was followed by normal acquisition;
- long-run verification was recorded as stable.

## Root Cause

Not Fully Confirmed.

## Supported Failure Path

Host-side network/acquisition configuration and NIC driver state contributed to an image-data integrity failure path associated with Mosaic artifacts.

## Suspected Mechanism

Network transport or host receive instability caused incomplete or improperly handled image data, resulting in intermittent Mosaic corruption.

The exact lower-level mechanism is not verified because packet capture and transport statistics were not preserved.

---

# 8. Corrective Action

Recorded corrective sequence:

1. verify the product-required network configuration;
2. enable/configure Jumbo Frame only where required;
3. set MTU according to the applicable product requirement;
4. reinitialize the network connection after configuration change;
5. update the NIC driver to an approved/recommended version;
6. disable NIC power-saving features where they are incompatible with continuous acquisition;
7. reduce frame rate temporarily as a diagnostic load test when required;
8. use Wireshark, NIC statistics, and SDK logs to collect evidence before and after correction.

Do not apply every network setting blindly to every product or host adapter.

---

# 9. Verification

Recorded result:

- continuous acquisition normal;
- no Mosaic observed;
- no `Image Loss` recorded during verification;
- long-duration operation reported stable;
- customer confirmed recovery.

For future Cases, record:

- test duration;
- frame rate;
- frame count;
- MTU/Jumbo configuration;
- NIC model and driver version;
- SDK/Detector log;
- packet capture or NIC error statistics.

---

# 10. Diagnostic Lessons

- Mosaic is a phenomenon, not a root cause.
- Random/intermittent block corruption should be distinguished from fixed detector-coordinate defects.
- `Image Loss` is a routing signal toward acquisition/data integrity, not direct proof of Ethernet packet loss.
- High-frame-rate sensitivity is useful evidence for throughput/load investigation.
- Partial improvement after one change may indicate multiple contributing factors; do not stop the investigation too early.
- Do not recalibrate first when the symptom and logs indicate a data-integrity branch.
- Preserve network configuration and transport evidence before making broad changes.

---

# 11. Knowledge Feedback Review

| Layer | Result | Action / Reason |
|---|---|---|
| FailureKnowledge | No direct update required | [MosaicFailure](../../07_FailureKnowledge/ImageFailure/MosaicFailure.md) remains the generic mechanism layer |
| DecisionTree | No direct update required | Existing Mosaic DecisionTree remains the primary routing entry |
| SOP | No direct update required | NetworkConfiguration and communication workflow already cover the execution path |
| Tools | No direct update required | Ping, Wireshark, and Log Viewer are the correct evidence tools |
| Case | Updated | Changed direct packet-loss assertion into evidence-bounded acquisition/data-integrity path |
| ErrorCode | Follow existing branch | If Image Loss/error events are captured, route them through the applicable ErrorCode knowledge |

---

# 12. Evidence Gap for Promotion to Verified

Missing evidence:

- detector SN;
- firmware/software/SDK versions;
- NIC model;
- NIC driver version before/after;
- original network configuration export;
- affected RAW/image sequence;
- SDK/Detector logs with frame/time correlation;
- Wireshark packet capture;
- NIC error/drop counters;
- controlled test isolating configuration versus driver contribution.

Without this evidence, the Case remains `Resolved` rather than `Verified`.

---

# 13. Related Documents

- [MosaicArtifact](../../08_ImageDiagnosis/MosaicArtifact/)
- [MosaicFailure](../../07_FailureKnowledge/ImageFailure/MosaicFailure.md)
- [Mosaic DecisionTree](../../09_DecisionTree/Image/Mosaic.md)
- [NetworkConfiguration SOP](../../10_SOP/NetworkConfiguration.md)
- [CommunicationWorkflow](../../06_Workflow/CommunicationWorkflow.md)
- [Ping](../../17_Tools/Ping/)
- [Wireshark](../../17_Tools/Wireshark/)
- [Log Viewer](../../17_Tools/Log%20Viewer/)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 14. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Batch 5 admission audit: retained event as Resolved, replaced direct packet-loss assertion with evidence-bounded acquisition/data-integrity path, added network/driver contribution boundaries |
| V1.0 | 2026-08 | Initial Mosaic image field case |