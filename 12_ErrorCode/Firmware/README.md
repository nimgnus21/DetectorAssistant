# Firmware Error Code

> Module: Firmware
>
> Category: Error Code Reference

---

# Overview

This module provides a categorized reference for firmware-related error codes defined in the SDK Programming Reference.

Firmware errors generally occur during detector startup, firmware upgrade, parameter storage, firmware execution, and detector internal management.

Unlike SDK errors, firmware errors are returned by the detector itself and are typically associated with detector hardware, firmware logic, or persistent storage.

---

# Scope

This module applies to:

- Detector firmware startup
- Firmware upgrade
- Firmware rollback
- Detector parameter storage
- UserRAM / UserROM operations
- Detector internal firmware execution

---

# Document Structure

```text
Firmware
├── README.md
├── Boot.md
├── EEPROM.md
└── Upgrade.md
```

---

# Category Description

## Boot

Firmware startup and detector initialization.

Typical topics include:

- Detector startup
- Firmware initialization
- Hardware self-test
- Detector Ready state
- Firmware rollback during startup

---

## EEPROM

Detector parameter storage.

Typical topics include:

- UserRAM
- UserROM
- Parameter persistence
- Detector configuration
- Parameter recovery

---

## Upgrade

Firmware update process.

Typical topics include:

- Firmware download
- Firmware verification
- Firmware activation
- Firmware rollback
- Version compatibility

---

# Firmware Lifecycle

```text
Power On

↓

BootLoader

↓

Firmware Initialization

↓

Hardware Self-Test

↓

Network Initialization

↓

Detector Ready

↓

Normal Operation

↓

Firmware Upgrade (Optional)

↓

Restart Detector

↓

Reconnect SDK
```

---

# Common Symptoms

| Symptom | Possible Module |
|----------|-----------------|
| Detector cannot start | Boot |
| Detector repeatedly reboots | Boot |
| Firmware rollback | Upgrade |
| Firmware update failed | Upgrade |
| Detector parameters lost | EEPROM |
| Detector configuration abnormal | EEPROM |
| Detector cannot save parameters | EEPROM |

---

# Recommended Troubleshooting Procedure

When firmware-related errors occur:

1. Verify detector model.
2. Verify detector firmware version.
3. Verify SDK version compatibility.
4. Verify detector startup status.
5. Check Detector.log.
6. Review the corresponding firmware error document.
7. Follow the related DecisionTree.
8. Restore firmware or parameters if necessary.
9. Escalate if the issue cannot be resolved.

---

# Related Modules

## DecisionTree

```text
09_DecisionTree/Firmware
```

---

## Workflow

```text
06_Workflow/FirmwareUpgradeWorkflow.md
06_Workflow/PowerOnWorkflow.md
```

---

## Case

```text
11_Case/Firmware
```

---

## Software

```text
04_Software
```

Firmware compatibility should always be considered together with the SDK version.

---

# Related Commands

The following SDK commands are commonly associated with firmware operations:

- Cmd_UpdateFirmware
- Cmd_Reset
- Cmd_ReadUserRAM
- Cmd_WriteUserRAM
- Cmd_ReadUserROM
- Cmd_WriteUserROM

---

# Related Events

Firmware-related errors are commonly returned through:

- Evt_GeneralError
- Evt_TaskResult_Failed
- Evt_TaskResult_Succeed

---

# Related Log

```
Detector.log
```

When escalating firmware-related issues, collect at least the following information:

- Detector.log
- Detector Model
- Detector Serial Number
- Firmware Version
- SDK Version
- Upgrade Package Version
- Reproduction Procedure

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |