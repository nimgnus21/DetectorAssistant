# FirmwareUpgradeFailed

Version: V1.1

Case ID: CASE-FW-002

Module: 11_Case / Firmware

Status: Resolved

Case Classification: Recovery Record / Root Cause Not Fully Confirmed

Evidence Level: Partial. The record documents successful recovery after repeating the upgrade and performing the required restart, but it does not preserve the failed upgrade log or sufficient evidence to prove that the missing restart was the sole failure mechanism.

Promotion Rule: Upgrade to `Verified` only with the exact failed stage, package/version scope, relevant logs, and controlled evidence showing that the identified condition explains the failure.

Severity: ★★★★☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Pluto Series
- Wired Detector
- Wireless Detector

Related Documents:

- [FirmwareUpgrade Tool](../../17_Tools/SDKTool/FirmwareUpgrade.md)
- [FirmwareUpgrade Workflow](../../06_Workflow/FirmwareUpgradeWorkflow.md)
- [FirmwareUpgradeFailed FailureKnowledge](../../07_FailureKnowledge/FirmwareFailure/FirmwareUpgradeFailed.md)
- [FirmwareUpgradeFailed DecisionTree](../../09_DecisionTree/Firmware/FirmwareUpgradeFailed.md)
- [Firmware Upgrade SOP](../../10_SOP/FirmwareUpgrade.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

The record contains a concrete recovery sequence, but detector identity, package version, SDK version, and failed upgrade-log evidence are not preserved.

The original statement that failure was caused by an incomplete shutdown/restart procedure is plausible and operationally useful, but the current record does not prove it as the unique root cause.

Therefore the correct status is `Resolved` rather than `Verified`.

---

# 2. Case Summary

During firmware upgrade, the upgrade was reported as failed or incomplete and the detector could not be reliably returned to normal operation until the approved upgrade/restart sequence was repeated.

---

# 3. Evidence Boundary

Recorded:

- Product family: Pluto1717
- operation: firmware upgrade
- approved release package was reportedly used
- factory parameters were backed up
- upgrade was repeated
- detector was powered off for the required interval and restarted
- firmware version, communication, and image acquisition recovered

Missing:

- detector SN
- exact package/version identity
- exact SDK version
- failed upgrade log
- precise failure stage
- controlled comparison isolating restart as the only causal variable

---

# 4. Actual Diagnostic / Recovery Sequence

1. Confirmed upgrade package source.
2. Confirmed parameter backup was completed.
3. Re-executed the firmware upgrade.
4. Performed the required power-off interval and restart.
5. Reconnected the detector.
6. Verified firmware version, SDK communication, and image acquisition.

---

# 5. Current Conclusion

Root Cause: Not Fully Confirmed.

Operationally supported finding: recovery succeeded after the approved upgrade sequence, including the required restart, was completed.

Do not generalize this record into a universal statement that every firmware upgrade failure is caused by missing power cycling.

---

# 6. Corrective Action

- Back up required parameters before upgrade.
- Use the approved release package.
- Preserve the exact package/version identity.
- Follow the product-specific power-cycle/restart requirement.
- Preserve failed and successful upgrade logs.
- Verify firmware version, communication, and image acquisition after upgrade.

---

# 7. Verification

Recorded result:

- Firmware version updated successfully.
- Detector communication recovered.
- SDK communication was normal.
- Image acquisition was normal.

Status: `Resolved`.

---

# 8. Knowledge Feedback Review

| Layer | Result | Reason |
|---|---|---|
| FailureKnowledge | No update required | Existing upgrade-failure knowledge remains the formal diagnostic layer |
| DecisionTree | No update required | Existing upgrade-failure routing already covers failed-stage investigation |
| SOP | Update required | Evidence preservation and explicit post-upgrade restart verification are operationally relevant |
| Tools | No update required | Firmware upgrade tool is already the execution entry |
| ErrorCode | No update required | No verified error code/event is preserved in this record |
| Index | Update required | Status changed from Released to Resolved |

---

# 9. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Case admission audit: reclassified as Resolved and separated recovery success from unverified root cause |
| V1.0 | 2026-08 | Initial firmware upgrade failure record |