# ImageLoss

Version: V1.1

Module: 11_Case / Communication

Status: Reference Candidate

Case Classification: Mixed Field Experience / Diagnostic Reference

Evidence Level: Candidate Evidence — this file does not currently contain a single event-level evidence package sufficient for `Verified` Case status.

Promotion Rule: Promote an individual scenario to `Verified` only after model/version/environment, actual diagnostic sequence, preserved evidence, corrective action, and objective retest result are recorded.

Severity: ★★★★★

Typical Frequency: ★★★★★（现场高频）

Applicable Products:

- Dynamic Flat Panel Detector
- Static Flat Panel Detector（GigE）
- Pluto Series
- Gigabit Ethernet Detector

Related Documents:

- [ImageGenerationWorkflow](../../06_Workflow/ImageGenerationWorkflow.md)
- [CommunicationFailure](../../07_FailureKnowledge/SystemFailure/CommunicationFailure.md)
- [ImageLoss DecisionTree](../../09_DecisionTree/Image/ImageLoss.md)
- [Ping](../../17_Tools/Ping/README.md)
- [Wireshark](../../17_Tools/Wireshark/README.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

This file contains general diagnostic knowledge and several typical field-experience summaries. It does not currently identify one specific customer/field/laboratory event with a complete event-level evidence package.

Therefore:

- it remains in `11_Case` as a search and reference node;
- its status is `Reference Candidate`, not `Verified` or equivalent;
- the listed causes are diagnostic candidates, not universally confirmed root causes;
- future real events may be linked here or promoted into independent Case records.

---

# 2. Reference Summary

## Reference Name

Image Loss

## Description

探测器能够正常连接，但图像采集过程中发生图像丢失。

SDK 或采集软件可能提示：

- Image Loss
- Lost Frame
- Frame Missing
- Acquisition Failed
- Offset Generation Failed（当丢帧影响校准输入时）

---

# 3. Diagnostic Candidates

The following are candidate branches that must be verified against the actual event:

- Jumbo Frame / MTU configuration mismatch where applicable;
- Packet Size or adapter receive configuration mismatch;
- network adapter driver or compatibility issue;
- acquisition rate exceeding validated PC/network capacity;
- adapter or PCIe power-saving features;
- cable, connector, or switch-path instability.

Do not mark any candidate as the root cause without event evidence.

---

# 4. Reference Diagnostic Path

1. Confirm whether the symptom is reproducible and record the acquisition condition.
2. Preserve affected image/RAW, SDK event, and timestamp.
3. Verify the product-specific network configuration rather than assuming one universal Jumbo Frame or Packet Size value.
4. Record adapter driver and power-saving configuration.
5. Compare the symptom under the intended acquisition rate.
6. Use [Ping](../../17_Tools/Ping/README.md) for reachability/stability and [Wireshark](../../17_Tools/Wireshark/README.md) when packet-level evidence is required.
7. Enter [ImageLoss DecisionTree](../../09_DecisionTree/Image/ImageLoss.md).
8. Preserve `Detector.log` and perform a controlled retest after one documented change.

---

# 5. Candidate Field Experiences

## Candidate A — Jumbo Frame / Adapter Configuration

Observed pattern:

- image loss or incomplete frame transfer;
- symptom improves after restoring the validated network-adapter configuration.

Evidence required for promotion:

- product/model and software scope;
- before/after adapter parameters;
- affected acquisition condition;
- logs or network evidence;
- controlled continuous-acquisition retest.

## Candidate B — Image Loss Affecting Calibration

Observed pattern:

- image acquisition interruption;
- calibration generation fails because the required input image set is incomplete.

Diagnostic boundary:

The calibration error is not by itself proof that network loss is the root cause. Preserve image count/selection state and use the applicable calibration DecisionTree.

## Candidate C — Acquisition Rate / System Capacity

Observed pattern:

- continuous acquisition loses frames under a higher rate;
- symptom changes after returning to a validated acquisition rate.

Evidence required:

- configured rate;
- PC/network configuration;
- repeatability;
- before/after controlled test.

---

# 6. Verification Rule

A future event may be closed only when:

- the exact symptom is identified;
- the failed stage is distinguished from detector connection, acquisition timeout, and image corruption;
- the corrective action is documented;
- the original symptom is absent or changes as predicted during a controlled retest;
- evidence is preserved or explicitly unavailable.

---

# 7. Knowledge Feedback Review

Current audit decision:

| Layer | Result | Reason |
|---|---|---|
| FailureKnowledge | No update required | Existing communication/image-loss knowledge already provides the generic diagnostic layer |
| DecisionTree | No update required | Existing ImageLoss routing is the primary diagnostic entry |
| SOP | No update required | No new verified procedural step was extracted from this mixed evidence |
| Tools | No update required | Ping/Wireshark are already linked as evidence tools |
| ErrorCode | No update required | No new verified error/event mapping was established |
| Index | Update required | This file remains a Reference Candidate rather than a Verified Case |

---

# 8. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.1 | 2026-08-10 | Case admission audit: reclassified as Reference Candidate, separated candidate causes from verified conclusions, added promotion and feedback rules |
| V1.0 | 2026-08 | Initial field-experience summary |