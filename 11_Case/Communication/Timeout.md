# Timeout

Version: V1.1

Module: 11_Case / Communication

Status: Reference Candidate

Case Classification: Mixed Diagnostic Reference

Evidence Level: Candidate Evidence — multiple timeout mechanisms are summarized, but the file does not represent one complete event-level Case.

Promotion Rule: A timeout scenario may be promoted only after the timeout stage, model/version, actual evidence, corrective action, and controlled verification are recorded.

Severity: ★★★★☆

Typical Frequency: ★★★★☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Wired Detector
- Wireless Detector
- Pluto Series

Related Documents:

- [ConnectionWorkflow](../../06_Workflow/ConnectionWorkflow.md)
- [CommunicationFailure](../../07_FailureKnowledge/SystemFailure/CommunicationFailure.md)
- [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md)
- [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md)
- [Ping](../../17_Tools/Ping/README.md)
- [Wireshark](../../17_Tools/Wireshark/README.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

The previous document grouped Connection Timeout, Acquisition Timeout, response timeout, and missing-image symptoms into one generic Case. These stages have different diagnostic boundaries and cannot share one automatically confirmed root cause.

The file is retained as a `Reference Candidate` for search and routing, not as a released event-level Case.

---

# 2. Stage Classification

Before troubleshooting, identify the timeout stage:

| Stage | Primary Meaning | Diagnostic Entry |
|---|---|---|
| Connection | Detector/SDK communication did not complete | [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md) |
| Acquisition | Acquisition started but expected response/image did not arrive | [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md) |
| Image Transfer | Exposure/acquisition evidence exists but image delivery is incomplete | [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md) |
| Device State | Detector remains Busy/abnormal or cannot progress | Relevant device-state DecisionTree / log review |

A timeout event does not by itself prove detector hardware, generator, network, SDK, or PC failure.

---

# 3. Candidate Diagnostic Branches

Depending on the identified stage, candidates may include:

- network interruption, loss, or configuration mismatch;
- detector state, initialization, or firmware abnormality;
- SDK/application timeout or configuration boundary;
- trigger/exposure sequence mismatch;
- acquisition rate or host resource limitation.

Each branch requires event evidence before being recorded as the root cause.

---

# 4. Reference Diagnostic Path

1. Preserve the exact error/event and timestamp.
2. Record detector state and acquisition/application mode.
3. Identify the timeout stage.
4. Run [Ping](../../17_Tools/Ping/README.md) only as a network reachability check; do not treat a successful Ping as proof that acquisition is normal.
5. Export and correlate `Detector.log` using [LogExport](../../17_Tools/SDKTool/LogExport.md).
6. Verify product-specific network, SDK, firmware, trigger, and operating conditions according to the identified branch.
7. Use [Wireshark](../../17_Tools/Wireshark/README.md) when packet-level evidence is needed.
8. Change one controlled variable and retest.

---

# 5. Candidate Field Experiences

### Candidate A — Address/Network Configuration

Pattern: connection timeout changes after correcting the active network interface configuration.

Required evidence: before/after configuration and repeatable reconnection.

### Candidate B — Detector State

Pattern: acquisition timeout occurs while the detector remains in an abnormal or Busy state; recovery follows the applicable state reset/reinitialization path.

Required evidence: state/log before and after recovery.

### Candidate C — Acquisition Rate / Host Capacity

Pattern: timeout occurs at a specific acquisition load and changes after returning to a validated operating condition.

Required evidence: rate, system environment, repeatability, and controlled before/after result.

---

# 6. Verification Rule

Closure of a future Case requires:

- timeout stage identified;
- suspected condition recorded before change;
- one corrective action or controlled change documented;
- retest under the relevant original condition;
- objective evidence that the timeout no longer occurs or changes as predicted.

---

# 7. Knowledge Feedback Review

| Layer | Result | Reason |
|---|---|---|
| FailureKnowledge | No update required | Existing timeout/communication mechanisms remain broader than this mixed record |
| DecisionTree | No update required | Stage-specific routing already exists |
| SOP | No update required | No new verified universal procedure was extracted |
| Tools | No update required | Ping, Wireshark and LogExport are existing evidence tools |
| ErrorCode | No update required | No new verified timeout mapping |
| Index | Update required | Classification changed to Reference Candidate |

---

# 8. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.1 | 2026-08-10 | Case admission audit: separated timeout stages and reclassified as Reference Candidate |
| V1.0 | 2026-08 | Initial timeout field-experience summary |