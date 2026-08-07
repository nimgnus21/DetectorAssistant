# Firmware Upgrade

> Module: Template
>
> Category: Firmware Upgrade Template

---

# Overview

This document provides standardized templates for firmware upgrade preparation, execution, verification, and troubleshooting.

It is intended for Field Application Engineers (FAEs) performing detector firmware upgrades during production, installation, maintenance, or technical support.

This document standardizes the firmware upgrade workflow and information collection process.

---

# Applicable Scope

This template applies to:

- Detector Firmware Upgrade
- Firmware Downgrade
- Firmware Recovery
- Version Verification
- Upgrade Failure Analysis

---

# Before Upgrade

## Detector Information

Detector Model:

Detector SN:

Current Firmware Version:

Target Firmware Version:

SDK Version:

Upgrade Tool Version:

Upgrade Package:

---

## Environment Checklist

□ Detector connected successfully

□ Detector status is Ready

□ Stable power supply

□ Stable network connection

□ Detector.log enabled

□ Upgrade package verified

□ Correct firmware selected

□ Detector SN confirmed

---

## Backup Information

Before upgrading, back up the following if required:

□ Calibration Templates

□ Configuration Files

□ Detector Parameters

□ Detector.log

---

# Upgrade Execution

## Upgrade Information

Upgrade Date:

Operator:

Upgrade Tool:

Upgrade Package:

Upgrade Start Time:

Upgrade End Time:

---

## Execution Checklist

□ Detector connected

□ Upgrade command executed

□ Upgrade completed successfully

□ Detector restarted

□ Detector reconnected

□ Firmware version updated

---

# After Upgrade Verification

## Connection Verification

□ Detector connected successfully

□ Detector status Ready

□ Communication normal

---

## Function Verification

□ Image acquisition successful

□ Image saving successful

□ Exposure normal

□ Detector response normal

---

## Calibration Verification

□ Calibration templates available

□ Templates loaded successfully

□ Image quality verified

---

# Upgrade Failure

## Required Information

Please collect:

□ Detector.log

□ Upgrade package

□ Upgrade software version

□ Firmware version before upgrade

□ Error message

□ Error screenshot

□ Detector SN

---

## Common Failure Scenarios

### Upgrade Interrupted

Collect:

□ Detector.log

□ Upgrade progress screenshot

□ Power status

□ Network status

---

### Firmware Version Mismatch

Collect:

□ Detector SN

□ Current firmware version

□ Target firmware version

□ SDK version

---

### Detector Cannot Reconnect

Collect:

□ Detector.log

□ Detector interface screenshot

□ Ping result

□ Network configuration

---

# Recovery Checklist

□ Detector powered normally

□ Detector detected

□ Firmware version readable

□ Communication restored

□ Image acquisition verified

□ Calibration verified

---

# Related SDK Command

Firmware upgrade is typically performed using:

- Cmd_UpdateFirmware

---

# Related SDK Events

Monitor:

- Evt_TaskResult_Succeed

- Evt_TaskResult_Failed

- Evt_GeneralError

---

# Related Error Codes

Frequently encountered upgrade-related errors include:

- Err_ApplyFirmwareFailed

- Err_FirmwareUpdated

- Err_OpenFileFailed

- Err_FileNotExist

- Err_InvalidFileFormat

- Err_TaskTimeOut

- Err_DetectorRespTimeout

- Err_FPD_FirmwareUpgrade_Error

- Err_FPD_FirmwareFallback

---

# Information Required for Technical Support

Please provide:

□ Detector Model

□ Detector SN

□ SDK Version

□ Firmware Version (Before)

□ Firmware Version (After)

□ Upgrade Package

□ Upgrade Tool Version

□ Detector.log

□ Upgrade Screenshot

□ Error Screenshot

□ Reproduction Procedure

---

# Related Modules

- 03_Hardware
- 06_Workflow
- 09_DecisionTree
- 11_Case
- 12_ErrorCode
- LogCollection.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |