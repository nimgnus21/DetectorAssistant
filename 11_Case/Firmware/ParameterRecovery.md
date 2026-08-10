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
- [Configuration Workflow](../../06_Workflow/ConfigurationWorkflow.md)
- [Failure Analysis Method](../../07_FailureKnowledge/FailureAnalysisMethod.md)
- [Firmware Upgrade SOP](../../10_SOP/FirmwareUpgrade.md)
- [Firmware Upgrade ErrorCode](../../12_ErrorCode/Firmware/Upgrade.md)
- [UpgradeFailed DecisionTree](../../09_DecisionTree/Firmware/UpgradeFailed.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

The record documents a concrete recovery outcome: saved factory parameters were restored after an abnormal firmware/parameter event and the detector returned to normal operation. The record does not preserve the before/after parameter sets, package/version scope, or a controlled mechanism proving why the parameters became invalid or unavailable.

Therefore the correct status is `Resolved`, not `Verified`.

---

# 2. Case Summary

After a firmware-related abnormal event, detector parameters required restoration from the previously saved parameter set. After the approved parameters were restored and the detector was revalidated, normal operation returned.

---

# 3. Evidence Boundary

Recorded:

- Product family: Pluto Series
- a firmware/parameter-related abnormal event occurred
- a saved parameter set was available
- the saved parameters were restored
- detector operation returned to normal after restoration

Missing:

- detector SN
- exact firmware/package version scope
- exact SDK version
- before/after parameter files or parameter diff
- exact parameter items affected
- event log identifying the parameter-loss mechanism
- controlled evidence proving that firmware upgrade alone caused the change

---

# 4. Actual Recovery Sequence

1. Preserved or identified the approved saved parameter set.
2. Confirmed the applicable detector/product configuration.
3. Restored the required parameters according to the approved procedure.
4. Restarted or reconnected the detector as required.
5. Verified detector communication and functional status.
6. Verified image acquisition.

---

# 5. Current Conclusion

Root Cause: Parameter-loss mechanism not fully confirmed.

Supported finding: restoring the approved parameter set returned the detector to normal operation.

Do not generalize this record into a universal statement that every firmware upgrade resets or corrupts detector parameters.

---

# 6. Corrective Action

- Back up approved parameters before firmware changes.
- Preserve parameter-set identity and applicable firmware/package versions.
- Restore parameters only through the approved product procedure.
- Record which parameter set was applied.
- Verify communication, configuration, and image acquisition after restoration.

---

# 7. Verification

Recorded result:

- Detector configuration returned to the required state.
- Detector communication was normal.
- Image acquisition was normal.

Status: `Resolved`.

---

# 8. Knowledge Feedback Review

| Layer | Result | Reason |
|---|---|---|
| FailureKnowledge | No update required | The record does not establish a new verified parameter-loss mechanism |
| DecisionTree | No update required | Existing firmware-upgrade failure routing remains the closest operational entry |
| SOP | Update required | Parameter backup and restoration evidence should remain explicit in the upgrade SOP |
| Tools | No update required | Firmware and calibration tools are the execution entries |
| ErrorCode | No update required | No verified parameter-specific error code is preserved |
| Index | Update required | Status remains Resolved |

---

# 9. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Related Documents link repair: removed obsolete ParameterRecovery DecisionTree dependency and aligned the case with existing configuration, firmware-upgrade, ErrorCode, and failure-analysis nodes |
| V1.0 | 2026-08 | Initial parameter recovery record |