# VersionMismatch

Version: V1.1

Case ID: CASE-FW-001

Module: 11_Case / Firmware

Status: Resolved

Case Classification: Project / OQC Version-Control Record

Evidence Level: Partial. The record describes a concrete version-control decision and successful remediation, but exact version values, project requirement evidence, and R&D review output are not preserved.

Promotion Rule: A version mismatch may be promoted to `Verified` only when the required version boundary, actual version set, compatibility decision, and post-change verification are preserved for the specific product/project scope.

Severity: ★★★☆☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Pluto Series
- Wired Detector
- Wireless Detector

Related Documents:

- [FirmwareUpgrade Tool](../../17_Tools/SDKTool/FirmwareUpgrade.md)
- [FirmwareUpgrade Workflow](../../06_Workflow/FirmwareUpgradeWorkflow.md)
- [VersionMismatch FailureKnowledge](../../07_FailureKnowledge/FirmwareFailure/VersionMismatch.md)
- [VersionMismatch DecisionTree](../../09_DecisionTree/Firmware/VersionMismatch.md)
- [Firmware Upgrade SOP](../../10_SOP/FirmwareUpgrade.md)
- [OQC / Sample Evidence Requirements](../../11_Case/Customer/OQC.md)
- [Case Admission Checklist](../CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../KnowledgeFeedbackRecord.md)

---

# 1. Admission Audit Result

This record is closer to a real project/OQC event than the generic upgrade-failure summaries, but the exact firmware, SDK, release-package values and the R&D compatibility decision are absent.

It supports a resolved version-management outcome, not a universal conclusion that any mismatch is defective or requires upgrade.

---

# 2. Case Summary

During OQC/sample preparation, the detector could connect and acquire images, but its installed firmware did not match the project-required version. After compatibility review and upgrade to the required version, functional verification and delivery approval were completed.

---

# 3. Evidence Boundary

Recorded:

- product: Pluto1717
- stage: OQC / sample delivery
- detector communication and acquisition were initially available
- version mismatch against the project requirement was identified
- R&D review was requested
- required firmware was installed
- communication and image acquisition were revalidated
- OQC approval and delivery proceeded

Missing:

- detector SN
- actual installed firmware version
- exact required firmware version
- SDK and release-package versions
- customer/project requirement record
- R&D review conclusion

---

# 4. Actual Investigation / Resolution Sequence

1. Identified the installed firmware version during OQC.
2. Compared the installed version with the project/sample requirement.
3. Reviewed the firmware, SDK, and release-package scope.
4. Requested R&D compatibility confirmation.
5. Determined that the current version did not meet the project requirement.
6. Upgraded to the required firmware.
7. Revalidated firmware version, SDK communication, and image acquisition before delivery.

---

# 5. Current Conclusion

Root Cause: Project version-control mismatch.

Scope limitation: this conclusion applies to the recorded project requirement. A version mismatch is not automatically a detector hardware fault, and it is not automatically proof that the detector cannot operate.

The need for upgrade must be determined against the applicable project/release requirement.

---

# 6. Corrective Action

- Record actual detector firmware and SDK/release versions during OQC.
- Compare against the approved project requirement.
- Obtain the required compatibility/release decision when versions differ.
- Upgrade only to the approved version.
- Revalidate communication and image acquisition after change.
- Update the OQC/sample record.

---

# 7. Verification

Recorded result:

- Firmware version matched the project requirement.
- SDK communication was normal.
- Image acquisition was normal.
- OQC review passed and the sample proceeded to delivery.

Status: `Resolved`.

---

# 8. Knowledge Feedback Review

| Layer | Result | Reason |
|---|---|---|
| FailureKnowledge | No update required | Existing version-mismatch knowledge already covers the general distinction from hardware failure |
| DecisionTree | No update required | Existing version-mismatch routing remains applicable |
| SOP | Update required | OQC version evidence and compatibility-review gate are procedural controls |
| Tools | No update required | Firmware tool remains the execution entry |
| ErrorCode | No update required | No error/event code is involved |
| Index | Update required | Status changed from Released to Resolved |

---

# 9. Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Case admission audit: reclassified as Resolved and bounded the conclusion to project-specific version control |
| V1.0 | 2026-08 | Initial firmware version mismatch record |