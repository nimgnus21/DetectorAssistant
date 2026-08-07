# SDK Error Code - Device

> Module: SDK
>
> Category: Device Error Codes

---

# Overview

This document describes SDK device-related error codes.

These errors occur when communicating with the detector hardware, including detector identification, device status, firmware compatibility, storage resources, and detector-side command execution.

---

# Related Commands

- Cmd_Connect
- Cmd_Disconnect
- Cmd_Reset
- Cmd_ReadUserRAM
- Cmd_WriteUserRAM
- Cmd_WriteUserROM
- Cmd_ReadTemperature
- Cmd_ReadHumidity

---

# Related Events

- Evt_GeneralError
- Evt_TaskResult_Failed
- Evt_ConnectProcess
- Evt_TransactionAborted

---

# Error Codes

---

## Err_DetectorIdNotFound

### Description

Detector ID could not be found.

### Possible Causes

- Detector configuration is incorrect.
- Detector ID does not exist.
- Configuration file is damaged.

### Recommended Actions

- Verify detector configuration.
- Check detector information.
- Reload detector configuration.

---

## Err_DetectorNotFound

### Description

The detector with the specified serial number could not be found.

### Possible Causes

- Detector is powered off.
- Detector is disconnected.
- Incorrect detector SN.
- Detector is on another subnet.

### Recommended Actions

- Verify detector power.
- Verify Ethernet connection.
- Verify detector serial number.
- Reconnect the detector.

---

## Err_ProdInfoMismatch

### Description

Detector product information or protocol version does not match the working directory configuration.

### Possible Causes

- Incorrect detector configuration.
- SDK version incompatible.
- Firmware version incompatible.
- Wrong product directory selected.

### Recommended Actions

- Verify detector model.
- Verify SDK version.
- Verify firmware version.
- Confirm correct working directory.

---

## Err_DetectorSN_Mismatch

### Description

The connected detector serial number does not match the serial number stored in the working directory.

Using existing calibration files may result in incorrect image correction.

### Possible Causes

- Different detector connected.
- Detector replaced.
- Working directory copied from another detector.

### Recommended Actions

- Verify detector serial number.
- Use the correct working directory.
- Recreate calibration templates if necessary.

---

## Err_FPD_General_Detector_Error

### Description

General detector error returned by the detector.

### Possible Causes

- Internal detector exception.
- Detector firmware error.
- Detector hardware fault.

### Recommended Actions

- Restart detector.
- Reconnect detector.
- Check Detector.log.
- Contact technical support if the issue persists.

---

## Err_FPD_Busy

### Description

Detector is busy executing another task.

### Possible Causes

- Image acquisition in progress.
- Calibration in progress.
- Firmware update in progress.
- Previous command has not completed.

### Recommended Actions

- Wait for the current task to finish.
- Wait for Evt_TaskResult_Succeed.
- Do not send duplicate commands.

---

## Err_FPD_Occupied

### Description

Detector is occupied by another operation or client.

### Possible Causes

- Another SDK instance is connected.
- Another application is controlling the detector.
- Previous connection was not released.

### Recommended Actions

- Close other detector software.
- Disconnect previous session.
- Restart detector if necessary.

---

## Err_FPD_CmdExecuteTimeout

### Description

Detector command execution timed out.

### Possible Causes

- Detector firmware response delayed.
- Detector busy.
- Communication interrupted.

### Recommended Actions

- Retry the command.
- Verify detector communication.
- Restart detector if necessary.

---

## Err_FPD_NotSupportInCurrMode

### Description

The requested operation is not supported in the current detector mode.

### Possible Causes

- Incorrect acquisition mode.
- Incorrect trigger mode.
- Current application mode does not support the command.

### Recommended Actions

- Verify detector operating mode.
- Change to the appropriate mode.
- Retry the operation.

---

## Err_FPD_NotImplemented

### Description

Detector received the command successfully, but the command is not implemented in the current firmware.

### Possible Causes

- Firmware version does not support the command.
- Unsupported detector model.

### Recommended Actions

- Verify firmware version.
- Upgrade firmware if applicable.
- Use supported SDK commands.

---

## Err_FPD_NoEnoughStorageSpace

### Description

Detector internal storage space is insufficient.

### Possible Causes

- Calibration storage full.
- Temporary files occupy storage.
- Internal flash memory capacity exceeded.

### Recommended Actions

- Remove unused calibration files.
- Check detector storage usage.
- Restart detector if necessary.

---

## Err_FPD_FileNotExist

### Description

The specified file does not exist inside the detector.

### Possible Causes

- Calibration file missing.
- Incorrect file index.
- File deleted accidentally.

### Recommended Actions

- Verify calibration file exists.
- Upload the required file again.
- Check selected file index.

---

## Err_FPD_HWCaliFileError

### Description

Hardware calibration file is unavailable or invalid.

The detector cannot perform hardware calibration because the required calibration template has not been prepared.

### Possible Causes

- Hardware Gain template not downloaded.
- Hardware Defect template not downloaded.
- Calibration template corrupted.
- Incorrect calibration file selected.

### Recommended Actions

- Verify calibration templates.
- Download calibration files again.
- Select the correct hardware calibration template.
- Confirm template download completed successfully.

---

# Detector Object States

## Unknown

Detector object has been created but is not connected.

Available operations include:

- Read/write configuration.
- Scan online detectors.
- Open local image files.

Hardware-related operations are unavailable.

---

## Ready

Detector is connected and ready for operation.

Available operations include:

- Image acquisition.
- Calibration.
- Detector parameter configuration.
- Firmware management.

---

## Busy

Detector is executing a task.

Most device commands will be rejected until the current task is completed.

---

# Diagnostic Checklist

Verify the following items:

- Detector power is normal.
- Detector serial number is correct.
- Detector firmware version is compatible.
- Detector state is Ready.
- Required calibration files exist.
- Detector internal storage is sufficient.
- Detector.log contains no device exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Connection/DetectorOffline.md
- 09_DecisionTree/Software/DetectorBusy.md
- 09_DecisionTree/Firmware/VersionMismatch.md
- 09_DecisionTree/Calibration/GainFailure.md
- 09_DecisionTree/Calibration/OffsetFailure.md
- 09_DecisionTree/Calibration/DefectFailure.md

---

# Related Case

- 11_Case/Communication/ConnectionFailed.md
- 11_Case/Firmware/VersionMismatch.md
- 11_Case/Calibration/GainGenerationFailed.md
- 11_Case/Calibration/OffsetGenerationFailed.md
- 11_Case/Calibration/DefectGenerationFailed.md

---

# Related Log

```
Detector.log
```

Device-related problems should always be analyzed together with Detector.log, detector status, firmware version, and calibration file status.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |