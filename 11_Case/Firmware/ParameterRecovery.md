# ParameterRecovery

Version: V1.1

Case ID: CASE-FW-004

Module: 11_Case / Firmware

Status: Resolved

Case Classification: Recovery Record / Parameter Loss Mechanism Not Fully Confirmed

Evidence Level: Partial. The record documents a successful parameter restoration sequence, but the specific parameter-loss mechanism and exact parameter/version evidence are not preserved.

Promotion Rule: Upgrade to `Verified` only when before/after parameter sets, firmware/package scope, and controlled verification establish the mechanism that caused the configuration change.

Severity: ★★★★☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Pluto Series
- Wired Detector
- Wireless Detector

Related Documents:

- [FirmwareUpgrade Tool](../../17_Tools/SDKTool/FirmwareUpgrade.md)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [FirmwareUpgrade Workflow](../../06_Workflow/FirmwareUpgradeWorkflow.md)
- [ParameterRecovery FailureKnowledge](../../07_FailureKnowledge/FirmwareFailure/ParameterRecovery.md)
- [ParameterRecovery DecisionTree](../../09_DecisionTree/Firmware/ParameterRecovery.md)
- [Firmware Upgrade SOP](../../10_SOP/FirmwareUpgrade.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

The record supports that restoring a saved factory parameter set returned the detector to the intended operating state. However, the stored Case does not preserve the actual backup files, before/after parameter comparison, exact firmware/package scope, or evidence proving why the parameters changed.

The recovery outcome is sufficient for `Resolved`, but not for a fully verified universal mechanism.

---

# 2. Case Summary

Firmware upgrade was reported successful and the detector could connect, but configuration and/or calibration-related operating parameters no longer matched the expected pre-upgrade state. Restoring the saved parameter set and restarting the detector recovered normal operation.

---

# 3. Evidence Boundary

Recorded:

- product: Pluto1717
- firmware upgrade reported successful
- detector communication remained available
- parameters were observed as inconsistent with the expected state
- saved factory parameters were restored
- restart and functional verification completed

Missing:

- detector SN
- exact firmware/FPGA/package versions
- original parameter backup identity
- before/after parameter diff
- calibration artifact/version identity
- upgrade log demonstrating how or why parameters changed

---

# 4. Actual Diagnostic / Recovery Sequence

1. Confirmed the firmware upgrade had completed.
2. Reviewed detector configuration, network parameters, and calibration-related status.
3. Recorded that the observed configuration did not match the expected state.
4. Restored the saved factory parameter set.
5. Restored applicable network/configuration values and checked calibration-related status.
6. Restarted the detector and allowed initialization to complete.
7. Reconnected through the SDK and verified detector online state and image acquisition.

---

# 5. Current Conclusion

Root Cause: Not Fully Confirmed.

Supported operational conclusion: restoring the saved parameter set returned the detector to the expected configuration and functional state.

The statement that a firmware upgrade universally resets parameters to defaults is not established by the current evidence and must not be promoted as a general rule from this Case alone.

---

# 6. Corrective Action

- Preserve factory parameter backup before firmware upgrade.
- Preserve applicable calibration/configuration artifacts and version scope.
- After upgrade, compare the actual configuration against the required state.
- Restore only the approved parameter set for the specific detector/version scope.
- Restart and verify communication, configuration, calibration status, and image acquisition.

---

# 7. Verification

Recorded result:

- Detector connected normally.
- Required parameter state was restored.
- Calibration-related status was reported normal.
- Image acquisition recovered.
- Functional recovery was accepted.

Status: `Resolved`.

---

# 8. Knowledge Feedback Review

| Layer | Result | Reason |
|---|---|---|
| FailureKnowledge | No update required | Existing parameter-recovery knowledge remains the generic mechanism layer |
| DecisionTree | No update required | Existing parameter-recovery routing remains applicable |
| SOP | Update required | Backup identity, restore boundary, and post-restore functional verification are important procedural controls |
| Tools | No update required | Firmware upgrade and calibration tools are already linked |
| ErrorCode | No update required | No verified error/event mapping was established |
| Index | Update required | Status changed from Released to Resolved |

---

# 9. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Case admission audit: reclassified as Resolved and separated parameter recovery success from unverified loss mechanism |
| V1.0 | 2026-08 | Initial parameter recovery record |