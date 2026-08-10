# Firmware Error Code - Upgrade

> Module: Firmware
>
> Category: Firmware Upgrade Error Codes

---

# Overview

This document describes firmware upgrade-related errors during download, verification, activation, reboot, and rollback.

Firmware errors must be interpreted with detector model, current/target firmware version, SDK version, package identity, power/communication state, and `Detector.log`.

---

# Related Commands

- `Cmd_UpdateFirmware`
- `Cmd_Reset`
- `Cmd_Connect`

# Related Events

- `Evt_TaskResult_Failed`
- `Evt_TaskResult_Succeed`
- `Evt_GeneralError`

---

# Error Code → Diagnostic Entry

| Error | Primary Entry | Tool / Evidence |
|---|---|---|
| `Err_ApplyFirmwareFailed` | [UpgradeFailed](../../09_DecisionTree/Firmware/UpgradeFailed.md) | Package identity, `Detector.log`, upgrade record |
| `Err_FirmwareUpdated` | [FirmwareUpgrade](../../10_SOP/FirmwareUpgrade.md) post-upgrade verification | Reboot/reconnect/version/acquisition evidence |
| `Err_FPD_FirmwareFallback` | [UpgradeFailed](../../09_DecisionTree/Firmware/UpgradeFailed.md) + [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md) | Rollback evidence, version comparison, log |
| `Err_FPD_General_FirmwareUpgrade_Error` | [UpgradeFailed](../../09_DecisionTree/Firmware/UpgradeFailed.md) | Communication/power/package/log evidence |

---

# Error Codes

## Err_ApplyFirmwareFailed

The firmware package was downloaded, but the detector failed to apply or activate it.

### Diagnostic Path

1. Stop repeated upgrade attempts and preserve the failure evidence.
2. Record detector model, current firmware, target firmware, SDK version, and package identity.
3. Enter [UpgradeFailed](../../09_DecisionTree/Firmware/UpgradeFailed.md).
4. Verify package/model/version compatibility through [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md).
5. Review the upgrade procedure in [FirmwareUpgrade](../../10_SOP/FirmwareUpgrade.md).
6. Export logs with [LogExport](../../17_Tools/SDKTool/LogExport.md).
7. Retry only after the failure branch has been identified and corrected.

---

## Err_FirmwareUpdated

Firmware update completed successfully. This is an informational status, not a failure.

### Required Verification

1. Complete the required detector power-cycle/reboot procedure.
2. Reconnect using `Cmd_Connect`.
3. Verify the reported firmware version.
4. Verify the detector state is normal.
5. Perform a controlled acquisition test.
6. If dynamic-product calibration state is affected by reset, follow the applicable calibration/configuration requirement before declaring release.

Use [FirmwareUpgrade](../../10_SOP/FirmwareUpgrade.md) as the verification path.

---

## Err_FPD_FirmwareFallback

The detector automatically rolled back to the previous firmware version, reported during the first connection through `Evt_GeneralError`.

### Diagnostic Path

1. Preserve the rollback event and log before another upgrade.
2. Record the current version and attempted target version.
3. Follow [UpgradeFailed](../../09_DecisionTree/Firmware/UpgradeFailed.md).
4. Compare compatibility through [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md).
5. Do not repeatedly force the same package until package/version compatibility and failure evidence are reviewed.

---

## Err_FPD_General_FirmwareUpgrade_Error

General detector-side firmware upgrade failure.

### Diagnostic Path

1. Preserve the exact error, command result, and timestamp.
2. Verify stable power and communication.
3. Verify package identity and detector model before retry.
4. Follow [UpgradeFailed](../../09_DecisionTree/Firmware/UpgradeFailed.md).
5. If communication evidence is abnormal, enter [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md).
6. Export `Detector.log` and upgrade evidence with [LogExport](../../17_Tools/SDKTool/LogExport.md).

---

# Pre-Upgrade Control

Before upgrading:

- Verify detector model.
- Record current firmware version.
- Verify target firmware applicability.
- Verify SDK compatibility where required.
- Ensure stable power.
- Ensure stable Ethernet communication.
- Close acquisition tasks.
- Preserve existing version/configuration evidence.
- Do not interrupt the upgrade.

---

# Evidence Package

Collect:

- Exact error/event and timestamp
- Detector model and applicable identity
- Current firmware version
- Target firmware version
- SDK version
- Firmware package identity/check information
- Upgrade step where failure occurred
- Detector power/reboot result
- Network/communication state when applicable
- `Detector.log`
- Result after controlled retry or rollback

---

# Related DecisionTree / SOP / Tool / Case

- [UpgradeFailed](../../09_DecisionTree/Firmware/UpgradeFailed.md)
- [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md)
- [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md)
- [FirmwareUpgrade](../../10_SOP/FirmwareUpgrade.md)
- [Firmware Upgrade Tool](../../17_Tools/SDKTool/FirmwareUpgrade.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)
- [FirmwareUpgradeFailed Case](../../11_Case/Firmware/FirmwareUpgradeFailed.md)
- [VersionMismatch Case](../../11_Case/Firmware/VersionMismatch.md)
- [ParameterRecovery Case](../../11_Case/Firmware/ParameterRecovery.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.2 | 2026-08-10 | Repaired Firmware DecisionTree references and aligned the Case/DecisionTree naming boundary |
| v1.1 | 2026-08-10 | Added direct upgrade failure mapping, evidence package, and post-upgrade verification chain |
| v1.0 | 2026-08-07 | Initial release |