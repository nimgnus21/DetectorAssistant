# Firmware Error Code - EEPROM

> Module: Firmware
>
> Category: EEPROM / UserROM Error Codes

---

# Overview

This document describes errors related to detector parameter storage.

The SDK uses **UserRAM** and **UserROM** to store detector configuration parameters.

- UserRAM stores runtime parameters.
- UserROM stores persistent parameters that remain after power-off.

Improper read/write operations may result in configuration loss or parameter inconsistency.

---

# Related Commands

- Cmd_ReadUserRAM
- Cmd_WriteUserRAM
- Cmd_ReadUserROM
- Cmd_WriteUserROM

---

# Related Events

- Evt_TaskResult_Succeed
- Evt_TaskResult_Failed
- Evt_GeneralError

---

# Error Codes

---

## Err_OpenFileFailed

### Description

Failed to access the parameter storage file.

### Possible Causes

- File cannot be opened.
- Access denied.
- Storage unavailable.

### Recommended Actions

1. Verify storage access.
2. Verify file permissions.
3. Retry the operation.

---

## Err_FileNotExist

### Description

The required parameter file does not exist.

### Possible Causes

- Configuration file deleted.
- Incorrect storage location.
- File damaged.

### Recommended Actions

1. Verify configuration files.
2. Restore missing files.
3. Reload detector configuration.

---

## Err_InvalidFileFormat

### Description

The parameter file format is invalid.

### Possible Causes

- Corrupted parameter file.
- Incorrect firmware version.
- Unsupported configuration format.

### Recommended Actions

1. Restore the correct configuration.
2. Regenerate configuration if necessary.
3. Verify firmware compatibility.

---

## Err_AccessDenied

### Description

Parameter write operation was denied.

### Possible Causes

- Detector busy.
- Write protection enabled.
- Permission insufficient.

### Recommended Actions

1. Wait until detector is Ready.
2. Retry the operation.
3. Verify detector status.

---

## Err_PreCondition

### Description

The required conditions for reading or writing detector parameters were not satisfied.

### Possible Causes

- Detector not connected.
- Detector not initialized.
- Previous task not completed.

### Recommended Actions

1. Connect the detector.
2. Verify detector status is Ready.
3. Retry the operation.

---

# UserRAM vs UserROM

| Item | UserRAM | UserROM |
|------|---------|----------|
| Storage | RAM | Flash / EEPROM |
| Power Loss | Lost | Retained |
| Write Command | Cmd_WriteUserRAM | Cmd_WriteUserROM |
| Read Command | Cmd_ReadUserRAM | Cmd_ReadUserROM |
| Typical Use | Temporary parameters | Permanent detector configuration |

---

# Important Notes

- `Cmd_ReadUserROM` returns the same data as `Cmd_ReadUserRAM`, because UserROM is copied into RAM during detector startup.
- `Cmd_WriteUserROM` updates both ROM and RAM.
- After `Cmd_WriteUserROM`, the SDK automatically performs `Cmd_ReadUserRAM`.
- Therefore, two task events are normally generated:
  1. Cmd_WriteUserROM
  2. Cmd_ReadUserRAM

---

# Diagnostic Checklist

Verify the following items:

- Detector is connected.
- Detector status is Ready.
- Parameter files are valid.
- Detector configuration is correct.
- Detector.log contains no storage exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Firmware/ParameterRecovery.md
- 09_DecisionTree/Software/APIError.md

---

# Related Case

- 11_Case/Firmware/ParameterRecovery.md

---

# Related Log

```
Detector.log
```

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |