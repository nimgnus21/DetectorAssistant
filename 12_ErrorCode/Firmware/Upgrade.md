# Firmware Error Code - Upgrade

> Module: Firmware
>
> Category: Firmware Upgrade Error Codes

---

# Overview

This document describes firmware upgrade-related error codes.

These errors occur during firmware download, firmware verification, firmware activation, or detector reboot after a firmware update.

---

# Related Commands

- Cmd_UpdateFirmware
- Cmd_Reset
- Cmd_Connect

---

# Related Events

- Evt_TaskResult_Failed
- Evt_TaskResult_Succeed
- Evt_GeneralError

---

# Error Codes

---

## Err_ApplyFirmwareFailed

### Description

The firmware file was successfully downloaded to the detector, but the detector failed to activate the new firmware.

### Possible Causes

- Firmware file is corrupted.
- Firmware version is incompatible.
- Firmware verification failed.
- Detector flash write failed.
- Detector reboot failed after upgrade.

### Recommended Actions

1. Verify the firmware package.
2. Confirm firmware matches the detector model.
3. Perform the upgrade again.
4. Restart the detector.
5. If the issue persists, recover the previous firmware.

---

## Err_FirmwareUpdated

### Description

Firmware update completed successfully.

The detector must be powered off, restarted, and reconnected before the new firmware becomes effective.

### Possible Causes

This is an informational status rather than a failure.

### Recommended Actions

1. Power off the detector.
2. Wait several seconds.
3. Power on the detector.
4. Execute Cmd_Connect again.
5. Verify the firmware version.

---

## Err_FPD_FirmwareFallback

### Description

The detector has automatically rolled back to the previous firmware version.

The SDK reports this condition during the first connection through **Evt_GeneralError**.

### Possible Causes

- Firmware verification failed.
- Firmware startup failed.
- Firmware compatibility issue.
- Upgrade interrupted.

### Recommended Actions

1. Verify detector firmware version.
2. Check Detector.log.
3. Perform the firmware upgrade again.
4. Use the correct firmware package.
5. Contact technical support if rollback occurs repeatedly.

---

## Err_FPD_General_FirmwareUpgrade_Error

### Description

General firmware upgrade failure reported by the detector.

### Possible Causes

- Firmware transmission failed.
- Flash programming failed.
- Firmware verification failed.
- Internal firmware exception.

### Recommended Actions

1. Verify firmware package integrity.
2. Verify detector communication.
3. Upgrade again using a stable network.
4. Restart detector after failure.
5. Collect Detector.log before escalation.

---

# Firmware Upgrade Recommendations

Before upgrading firmware:

- Verify detector model.
- Verify firmware version.
- Verify SDK compatibility.
- Ensure stable power supply.
- Ensure stable Ethernet connection.
- Close all acquisition tasks.
- Do not interrupt the upgrade process.

---

# Diagnostic Checklist

When firmware upgrade errors occur, verify the following:

- Firmware package is correct.
- Firmware package is not corrupted.
- Detector model matches the firmware.
- Detector communication is stable.
- Detector power is stable.
- Detector reboot completed successfully.
- Detector.log contains no firmware exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Firmware/FirmwareUpgradeFailed.md
- 09_DecisionTree/Firmware/VersionMismatch.md

---

# Related Case

- 11_Case/Firmware/VersionMismatch.md
- 11_Case/Firmware/ParameterRecovery.md

---

# Related Workflow

- 06_Workflow/FirmwareUpgradeWorkflow.md

---

# Related Log

```
Detector.log
```

Firmware upgrade failures should always be analyzed together with Detector.log, firmware package information, detector model, firmware version, and SDK version.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |