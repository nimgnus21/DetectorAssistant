# Firmware

> Module: Glossary
>
> Category: Firmware Terminology

---

# Overview

This document defines the standard terminology related to detector firmware.

Firmware is the embedded software running inside the detector and is responsible for hardware control, communication, image acquisition, calibration management, and system operation.

The terminology defined here is referenced throughout the DetectorAssistant knowledge base, including firmware upgrades, troubleshooting, SDK documentation, workflows, and error code references.

---

# Firmware

## Definition

Embedded software running inside the detector hardware.

Firmware directly controls detector operation and provides services required by the SDK.

## Responsibilities

- Detector initialization
- Hardware control
- Communication management
- Image acquisition
- Calibration management
- Status monitoring

---

# Firmware Version

## Definition

The software version currently installed in the detector.

## Purpose

Used for:

- Compatibility verification
- Upgrade management
- Technical support
- Problem analysis

---

# Firmware Package

## Definition

A firmware image file used to install or update detector firmware.

## Typical Usage

- Firmware Upgrade
- Firmware Recovery

---

# Firmware Upgrade

## Definition

The process of replacing the detector's current firmware with a newer version.

## Purpose

- Add new features
- Fix software defects
- Improve stability
- Improve compatibility

## Related SDK Command

- Cmd_UpdateFirmware

---

# Firmware Downgrade

## Definition

The process of installing an earlier firmware version.

## Typical Usage

- Compatibility testing
- Issue rollback
- Engineering verification

---

# Firmware Update

## Definition

The complete process of transferring, validating, and activating a firmware package.

---

# Firmware Compatibility

## Definition

The compatibility relationship between detector firmware and SDK versions.

## Notes

Firmware and SDK versions should always be verified before deployment.

---

# Firmware Activation

## Definition

The process of enabling newly installed firmware after successful download.

---

# Firmware Rollback

## Definition

The process of restoring a previous firmware version after an unsuccessful upgrade.

---

# Firmware Recovery

## Definition

The procedure used to restore detector operation after firmware corruption or upgrade failure.

---

# Firmware Fallback

## Definition

The detector automatically returns to a previous firmware version after an unsuccessful upgrade.

## Related Error Code

- Err_FPD_FirmwareFallback

---

# Firmware Verification

## Definition

The process of confirming that the installed firmware version matches the expected version and operates correctly.

---

# Firmware Validation

## Definition

The process of checking firmware integrity before installation.

---

# Firmware Image

## Definition

The binary file containing executable firmware code.

---

# Bootloader

## Definition

A small program executed immediately after power-on.

## Purpose

- Initialize hardware
- Load firmware
- Support firmware upgrades and recovery

---

# Flash Memory

## Definition

Non-volatile memory used to store detector firmware.

---

# ROM

## Definition

Read-Only Memory used to permanently store firmware or factory configuration data.

---

# RAM

## Definition

Volatile memory used during detector operation.

Contents are lost after power-off.

---

# User ROM

## Definition

Persistent storage area used for user configuration parameters.

## Related SDK Commands

- Cmd_WriteUserROM
- Cmd_ReadUserROM

---

# User RAM

## Definition

Temporary storage area used for detector configuration during runtime.

## Related SDK Commands

- Cmd_WriteUserRAM
- Cmd_ReadUserRAM

---

# Power Cycle

## Definition

Turning detector power off and on again.

## Typical Usage

Required after certain firmware updates before reconnecting the detector.

---

# Cold Boot

## Definition

Detector startup performed after complete power removal.

---

# Warm Restart

## Definition

Detector restart without complete power removal.

---

# Firmware Integrity

## Definition

The correctness and completeness of a firmware image.

---

# Firmware Integrity Check

## Definition

Verification performed before or during firmware installation to ensure the firmware image has not been corrupted.

---

# Firmware Upgrade Failure

## Definition

A firmware installation process that does not complete successfully.

## Typical Causes

- Power interruption
- Communication failure
- Invalid firmware package
- Hardware fault

---

# Firmware Recovery Mode

## Definition

A special operating mode used to recover detector firmware after a failed upgrade.

---

# Firmware Configuration

## Definition

Firmware parameters controlling detector behavior.

## Examples

- Detector mode
- Network configuration
- Hardware parameters

---

# Firmware Release

## Definition

An officially published firmware version for production or maintenance use.

---

# Firmware Revision

## Definition

A unique revision identifier associated with a firmware release.

---

# Related SDK Commands

- Cmd_UpdateFirmware
- Cmd_Reset
- Cmd_ReadUserROM
- Cmd_WriteUserROM
- Cmd_ReadUserRAM
- Cmd_WriteUserRAM

---

# Related SDK Events

- Evt_TaskResult_Succeed
- Evt_TaskResult_Failed
- Evt_GeneralError

---

# Related Error Codes

- Err_ApplyFirmwareFailed
- Err_FirmwareUpdated
- Err_FPD_FirmwareUpgrade_Error
- Err_FPD_FirmwareFallback
- Err_OpenFileFailed
- Err_FileNotExist
- Err_InvalidFileFormat
- Err_TaskTimeOut

---

# Related Modules

- 02_SDK
- 03_Hardware
- 06_Workflow
- 09_DecisionTree
- 11_Case
- 12_ErrorCode
- 13_Template

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |