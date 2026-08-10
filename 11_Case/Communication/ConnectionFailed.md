# ConnectionFailed

Version: V1.1

Module: 11_Case / Communication

Status: Reference Candidate

Case Classification: Mixed Field Evidence + Diagnostic Reference

Evidence Level: Mixed — this file contains both generic diagnostic guidance and several more specific field-experience records. The file as a whole is not one event-level Case and must not be treated as a single `Verified` conclusion.

Promotion Rule: Each field experience must be evaluated independently. Only an individual event with sufficient environment, diagnostic evidence, corrective action, and objective verification may become a `Verified` Case.

Severity: ★★★★★

Typical Frequency: ★★★★★（现场高频）

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Wired Detector
- Wireless Detector（AP Mode）
- Pluto Series

Related Documents:

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

The original document mixed:

- generic connection-failure categories;
- a standard troubleshooting procedure;
- short anonymous field experiences;
- several more specific field records from FAE reporting.

These records do not all share the same evidence level. Therefore the document is retained as a `Reference Candidate` and its individual experiences must not inherit one global `Released` or `Verified` status.

---

# 2. Reference Symptom

Typical entries include:

- Detector Offline;
- Connect Failed;
- Device Not Found;
- Connection Timeout;
- Cannot Open Detector;
- SDK cannot discover the detector.

These are entry symptoms, not root causes.

---

# 3. Candidate Diagnostic Branches

Depending on the actual event, evaluate:

1. active network interface and addressing;
2. physical connection and link state;
3. detector startup/state;
4. SDK/runtime configuration and version consistency;
5. security or operating-system interference where evidence supports it.

Do not apply a candidate branch as the final root cause without event evidence.

---

# 4. Reference Diagnostic Path

1. Record model, version, connection mode, and exact symptom.
2. Confirm detector power/state and physical link.
3. Identify the active detector network interface.
4. Preserve current network configuration before modification.
5. Run [Ping](../../17_Tools/Ping/README.md) and record reachability/stability.
6. If discovery and connection succeed but acquisition fails, leave the generic connection path and enter the relevant acquisition/image path.
7. Preserve SDK/Detector logs and configuration files.
8. Change one documented variable and perform a controlled retest.

---

# 5. Field Evidence Candidates

## Candidate 01 — Mercu1616TE Jumbo Frame Configuration

Observed field pattern:

- detector discovery and SDK connection were normal;
- image acquisition could not start or timed out;
- network adapter Jumbo Frame configuration was identified as inconsistent with the applicable detector communication requirement;
- acquisition recovered after restoring the required configuration.

Evidence boundary:

The record is more specific than the generic sections but still requires preserved version/configuration evidence if promoted to a standalone `Verified` Case.

## Candidate 02 — Pluto Mode.ini Mismatch

Observed field pattern:

- detector communication was normal;
- acquisition initialization or selected modes failed after SDK/configuration change;
- customer Mode.ini differed from the corresponding released configuration;
- operation recovered after restoring the required configuration and restarting the application/SDK.

Promotion boundary:

A standalone Case should include the exact model, SDK/configuration version, changed parameters, and controlled verification.

## Candidate 03 — SDK DLL Runtime Mismatch

Observed field pattern:

- application initialization failed while detector hardware communication remained available;
- SDK DLL files were missing or mismatched with the application release;
- operation recovered after restoring the correct runtime package.

Diagnostic boundary:

This is primarily an SDK runtime/deployment path and should not be classified as detector communication hardware failure.

## Candidate 04 — FrameNo / Application Processing

Observed field pattern:

- detector communication and image output continued;
- abnormal FrameNo behavior was associated with application frame handling or synchronization logic.

Evidence boundary:

Requires callback/buffer/application evidence before concluding that detector hardware is normal.

## Candidate 05 — Acquisition Mode Configuration

Observed field pattern:

- standard acquisition worked while a specific configured mode behaved abnormally;
- network and firmware were reported normal;
- investigation focused on application/SDK mode configuration.

Promotion boundary:

The exact mode, product, parameter scope, and retest result are required.

---

# 6. Verification Rule

A future event may be closed only after:

- exact symptom and failed stage are identified;
- actual environment/version is recorded;
- diagnostic evidence supports the selected branch;
- corrective action is documented;
- controlled verification confirms the expected change.

Successful Ping or detector discovery alone does not prove normal acquisition.

---

# 7. Knowledge Feedback Review

| Layer | Result | Reason |
|---|---|---|
| FailureKnowledge | No update required | Generic communication mechanisms are already represented |
| DecisionTree | No update required | Existing connection/acquisition routing remains applicable |
| SOP | No update required | No new universally verified step was extracted from the mixed record |
| Tools | No update required | Existing Ping/Wireshark/log tools cover the evidence path |
| ErrorCode | No update required | No new verified error/event mapping established |
| Index | Update required | File classification changed; specific future verified events should receive independent entries |

---

# 8. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.1 | 2026-08-10 | Case admission audit: reclassified mixed content, separated field-evidence candidates, and added promotion boundaries |
| V1.0 | 2026-08 | Initial connection field-experience summary |