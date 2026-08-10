# BootFailed

Version: V1.1

Case ID: CASE-FW-003

Module: 11_Case / Firmware

Status: Resolved

Case Classification: Recovery Record / Root Cause Not Fully Confirmed

Evidence Level: Partial event evidence. Recovery and functional verification are recorded, but the stored record does not contain sufficient upgrade-log analysis to identify the firmware/boot failure mechanism.

Promotion Rule: Upgrade to `Verified` only when the specific failure mechanism is supported by preserved upgrade/boot evidence or reproducible controlled verification.

Severity: ★★★★★

Typical Frequency: ★★☆☆☆

Applicable Products:

- Pluto Series
- Wired Detector
- Wireless Detector

Related Documents:

- [FirmwareUpgrade Tool](../../17_Tools/SDKTool/FirmwareUpgrade.md)
- [Initialization Workflow](../../06_Workflow/InitializationWorkflow.md)
- [Configuration Workflow](../../06_Workflow/ConfigurationWorkflow.md)
- [Failure Analysis Method](../../07_FailureKnowledge/FailureAnalysisMethod.md)
- [BootFailure DecisionTree](../../09_DecisionTree/Firmware/BootFailure.md)
- [Firmware Upgrade SOP](../../10_SOP/FirmwareUpgrade.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

This record describes a specific upgrade-related recovery sequence, but its event evidence is incomplete: SN, upgrade package identity, before/after firmware version, SDK version, and upgrade log analysis are not preserved in the record.

The documented outcome supports `Resolved`: the detector recovered and passed functional checks. It does not support a verified statement about why the boot process failed.

---

# 2. Case Summary

Detector failed to boot or reconnect after a firmware upgrade. After power-state checks, controlled restart, package/version review, network verification, log export, and R&D-guided firmware recovery, the detector returned to normal operation.

---

# 3. Event Evidence Boundary

Known from the record:

- Product: Pluto1717
- Operation: Firmware upgrade
- Pre-upgrade operation: reported normal
- Post-upgrade symptom: offline / SDK not discoverable / Ping unavailable / acquisition unavailable
- Recovery: firmware recovery performed according to R&D analysis
- Verification: boot, SDK connection, firmware version, and image acquisition returned to normal

Missing or not preserved:

- Detector SN
- exact pre/post firmware versions
- upgrade package identity
- SDK version
- upgrade log content
- R&D failure-mechanism conclusion

---

# 4. Actual Diagnostic Sequence

1. Confirmed detector power, indicators, and network-link condition; recorded as normal.
2. Performed complete power-off and restart; connection did not recover.
3. Reviewed firmware package/release and SDK version consistency; recorded as consistent.
4. Checked network configuration; recorded as normal.
5. Exported upgrade information/logs and submitted the event for R&D analysis.
6. Performed firmware recovery according to the resulting guidance.
7. Retested boot, SDK connection, firmware version, and image acquisition.

---

# 5. Current Conclusion

Root Cause: Not Fully Confirmed.

Supported conclusion: an upgrade-related boot/initialization failure occurred and the detector recovered after the R&D-guided firmware recovery path.

The statement "firmware upgrade completed but boot initialization was abnormal" is an event description, not a verified failure mechanism.

---

# 6. Corrective Action

- Preserve upgrade and version information.
- Do not repeatedly re-upgrade without identifying the failed stage.
- Export upgrade/SDK/detector logs.
- Follow the approved recovery path for the applicable product and package.
- Perform complete functional verification after recovery.

---

# 7. Verification

Recorded result:

- Detector booted normally.
- SDK connection succeeded.
- Firmware version was reported correct.
- Image acquisition returned to normal.

Status: `Resolved`, not `Verified`, because the recovery result is documented but the failure mechanism is not independently established.

---

# 8. Preventive Action

- Use the approved release package.
- Preserve pre/post upgrade versions and package identity.
- Prevent power interruption during upgrade.
- Save upgrade logs.
- Verify boot, communication, and acquisition after upgrade rather than relying only on a success indication.

---

# 9. Knowledge Feedback Review

| Layer | Result | Reason |
|---|---|---|
| FailureKnowledge | No update required | Existing boot-failure knowledge already covers the generic mechanism layer; this record adds no verified new mechanism |
| DecisionTree | No update required | Existing boot-failure routing remains applicable |
| SOP | Update required | Post-upgrade functional verification and evidence preservation should remain explicit in the firmware upgrade SOP |
| Tools | No update required | Firmware upgrade tooling and log handling are already the operational entry |
| ErrorCode | No update required | No specific verified error/event code is preserved |
| Index | Update required | Status changed from Released to Resolved |

---

# 10. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Case admission audit: downgraded to Resolved, separated recovery result from unverified failure mechanism, and added evidence/feedback boundaries |
| V1.0 | 2026-08 | Initial firmware boot failure record |