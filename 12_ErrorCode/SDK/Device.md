# SDK Error Code - Device

> Module: SDK
>
> Category: Device Error Codes

---

# Overview

This document describes errors returned while identifying, connecting, controlling, or operating the detector, including device identity, state, firmware compatibility, storage, detector-side command execution, and calibration-file availability.

A device error must be evaluated with detector state, model/SN, firmware version, working-directory configuration, and `Detector.log`.

---

# Related Commands

- `Cmd_Connect`
- `Cmd_Disconnect`
- `Cmd_Reset`
- `Cmd_ReadUserRAM`
- `Cmd_WriteUserRAM`
- `Cmd_WriteUserROM`
- `Cmd_ReadTemperature`
- `Cmd_ReadHumidity`

---

# Error Code → Diagnostic Entry

| Error | Primary Diagnostic Entry | Required Evidence |
|---|---|---|
| `Err_DetectorIdNotFound` | [DetectorNotFound](../../09_DecisionTree/Software/DetectorNotFound.md) | Configuration, detector identity |
| `Err_DetectorNotFound` | [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md) | Power, IP/SN, network state |
| `Err_ProdInfoMismatch` / `Err_DetectorSN_Mismatch` | [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md) or working-directory verification | Model/SN, SDK/FW, working directory |
| `Err_FPD_General_Detector_Error` | [SDKException](../../09_DecisionTree/Software/SDKException.md) | Exact operation, log, device state |
| `Err_FPD_Busy` / `Err_FPD_Occupied` | [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md) | Current task/client/session |
| `Err_FPD_CmdExecuteTimeout` | [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md) | Command, device state, network/log |
| `Err_FPD_NotSupportInCurrMode` | [ConfigurationWorkflow](../../06_Workflow/ConfigurationWorkflow.md) | Current mode/trigger/ROI configuration |
| `Err_FPD_NotImplemented` | [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md) | Firmware/model/API compatibility |
| `Err_FPD_NoEnoughStorageSpace` / `Err_FPD_FileNotExist` | Calibration/file-state verification | File list, operation, detector log |
| `Err_FPD_HWCaliFileError` | [Calibration](../../10_SOP/Calibration.md) | Template identity, generation/download result |

---

# Diagnostic Rules

## Identity and Configuration Errors

For `Err_DetectorIdNotFound`, `Err_DetectorNotFound`, `Err_ProdInfoMismatch`, and `Err_DetectorSN_Mismatch`:

1. Do not overwrite the working directory or calibration files first.
2. Record detector model, SN, SDK version, firmware version, and working-directory identity.
3. Confirm the connected detector before applying calibration or configuration files.
4. Use the linked DecisionTree before attempting recovery.

## State Errors

For `Err_FPD_Busy` and `Err_FPD_Occupied`:

1. Identify the current task or connected client.
2. Wait for task completion where supported.
3. Do not send duplicate commands as a recovery shortcut.
4. If the state does not clear, preserve logs and follow [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md).

## Firmware / Mode Errors

For `Err_FPD_NotSupportInCurrMode` and `Err_FPD_NotImplemented`:

1. Record the exact command and current mode.
2. Verify configuration through [ModeConfiguration](../../17_Tools/SDKTool/ModeConfiguration.md).
3. Verify firmware/model compatibility before upgrading or changing mode.

## Calibration File Errors

For `Err_FPD_NoEnoughStorageSpace`, `Err_FPD_FileNotExist`, and `Err_FPD_HWCaliFileError`:

1. Preserve current calibration and log evidence.
2. Verify file existence and selected index.
3. Verify template identity matches the detector and intended calibration type.
4. Follow [Calibration](../../10_SOP/Calibration.md).
5. Use [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md) or [DTDITool](../../17_Tools/SDKTool/DTDITool.md) only where applicable.

---

# Detector Object States

## Unknown

Detector object exists but is not connected. Hardware operations are unavailable.

## Ready

Detector is connected and ready for acquisition, calibration, configuration, and supported firmware operations.

## Busy

Detector is executing a task. Most device commands should not be retried until task completion or an explicit recovery path is reached.

---

# Evidence Package

Collect:

- Exact error code and timestamp
- Command/API that triggered the error
- Detector state (`Unknown` / `Ready` / `Busy`)
- Detector model and SN where permitted
- SDK version and firmware version
- Working-directory/configuration identity
- Relevant calibration/template information
- `Detector.log`
- Result after controlled reconnect or retry

For export, use [LogExport](../../17_Tools/SDKTool/LogExport.md).

---

# Related DecisionTree / SOP / Tool

- [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md)
- [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md)
- [SDKException](../../09_DecisionTree/Software/SDKException.md)
- [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md)
- [Calibration](../../10_SOP/Calibration.md)
- [ConfigurationWorkflow](../../06_Workflow/ConfigurationWorkflow.md)
- [ModeConfiguration](../../17_Tools/SDKTool/ModeConfiguration.md)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added error-to-decision mapping, evidence rules, and direct SOP/tool links |
| v1.0 | 2026-08-07 | Initial release |