# NetworkConfiguration

Version: V1.1

Module: 11_Case / Communication

Status: Reference Candidate

Case Classification: Mixed Field Experience / Diagnostic Reference

Evidence Level: Candidate Evidence — the file summarizes recurring configuration patterns but does not contain a single independently evidenced event sufficient for `Verified` status.

Promotion Rule: A specific network-configuration cause may be promoted only with product/version scope, actual before/after configuration, diagnostic evidence, and controlled verification.

Severity: ★★★★☆

Typical Frequency: ★★★★★（现场高频）

Applicable Products:

- Wired Detector
- Wireless Detector（AP Mode）
- Pluto Series
- Gigabit Ethernet Detector

Related Documents:

- [NetworkConfiguration SOP](../../10_SOP/NetworkConfiguration.md)
- [ConnectionWorkflow](../../06_Workflow/ConnectionWorkflow.md)
- [CommunicationFailure](../../07_FailureKnowledge/SystemFailure/CommunicationFailure.md)
- [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md)
- [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md)
- [Ping](../../17_Tools/Ping/README.md)
- [Wireshark](../../17_Tools/Wireshark/README.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

This file is a cross-symptom network configuration reference, not a single event-level Case. The original `Released` status is therefore replaced by `Reference Candidate`.

The content remains useful for search and diagnostic branching, but statements such as "IP error", "Jumbo Frame", or "Packet Size" are candidate causes until confirmed in a specific event.

---

# 2. Reference Summary

Network configuration inconsistency may contribute to:

- Detector Offline;
- Connection Failed;
- Ping instability;
- Image Loss;
- Timeout;
- calibration input interruption.

The same symptom can also originate outside network configuration. Use the DecisionTree before applying a configuration change.

---

# 3. Candidate Configuration Branches

## 3.1 Interface Selection

Verify that the PC interface actually connected to the detector is the interface being configured.

For AP Mode, the relevant wireless interface must be identified. Do not modify unrelated interfaces merely to test connectivity.

## 3.2 IP / Subnet / Address Conflict

Record the actual configuration before modification and verify product-specific addressing requirements.

## 3.3 Adapter Parameters

Where applicable, verify the released product configuration for:

- MTU / Jumbo Frame;
- packet or transport size;
- receive/transmit buffer;
- interrupt moderation;
- power-saving features.

This document does not define universal values.

## 3.4 Driver / Operating System Layer

Record adapter model and driver version. Use a validated driver/version boundary where one exists.

---

# 4. Reference Diagnostic Path

1. Identify the actual connection mode: wired or AP Mode.
2. Identify the active detector interface.
3. Preserve current IP/subnet and adapter configuration.
4. Run [Ping](../../17_Tools/Ping/README.md) and record reachability, loss, and repeatability.
5. Compare adapter parameters against the applicable product release/configuration source.
6. If image transfer is affected, capture logs and use [Wireshark](../../17_Tools/Wireshark/README.md) when packet evidence is required.
7. Enter the symptom-specific DecisionTree rather than assuming all failures are network configuration errors.
8. Change one documented variable at a time and perform a controlled retest.

---

# 5. Candidate Field Experiences

### Candidate A — Wrong Interface Modified

Pattern: connection remains abnormal after network changes because the configured interface was not the active detector interface.

Promotion evidence: before/after interface configuration and successful controlled reconnection.

### Candidate B — AP Mode Interface Mismatch

Pattern: wireless detector cannot communicate while the wired interface is being changed instead of the active AP interface.

Promotion evidence: connection mode, active adapter identity, before/after configuration, and reconnection result.

### Candidate C — Adapter Parameter Mismatch

Pattern: detector connection may succeed but image transfer or calibration input becomes unstable until the validated adapter configuration is restored.

Promotion evidence: exact product requirement, before/after parameters, logs, and continuous retest.

---

# 6. Verification Rule

A future Case may be closed only when the modified configuration is explicitly recorded and the original symptom is verified under the same relevant operating condition.

Ping success alone is insufficient proof of normal image acquisition, and successful acquisition alone is insufficient proof that a specific network parameter was the sole root cause without before/after evidence.

---

# 7. Knowledge Feedback Review

| Layer | Result | Reason |
|---|---|---|
| FailureKnowledge | No update required | Generic network configuration mechanisms already exist |
| DecisionTree | No update required | Existing connection/image-loss branches remain the correct primary routing |
| SOP | No update required | No new verified universal configuration step was established |
| Tools | No update required | Ping/Wireshark usage is already available |
| ErrorCode | No update required | No new verified error-code mapping |
| Index | Update required | Classification changed to Reference Candidate |

---

# 8. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.1 | 2026-08-10 | Case admission audit: reclassified as Reference Candidate and added evidence, promotion and feedback boundaries |
| V1.0 | 2026-08 | Initial network field-experience summary |