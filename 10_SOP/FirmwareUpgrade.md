# Firmware Upgrade

> Module: Standard Operating Procedure
>
> SOP ID: SOP-004
>
> Category: Firmware Upgrade

---

# Scope

This SOP describes the standard procedure for upgrading detector firmware.

This procedure applies to:

- Firmware updates
- Firmware rollback
- Firmware recovery
- Detector maintenance
- Factory firmware programming

---

# Objective

Safely upgrade detector firmware while preserving detector configuration and ensuring compatibility with the installed SDK.

---

# Responsibility

| Role | Responsibility |
|------|----------------|
| FAE | Execute firmware upgrade |
| Technical Support Engineer | Remote upgrade support |
| Production Engineer | Factory firmware programming |
| R&D Engineer | Resolve abnormal upgrade failures |

---

# Preconditions

Before upgrading firmware, confirm:

- Detector status is Ready.
- Detector communication is stable.
- Correct firmware package has been obtained.
- Firmware version is verified.
- SDK version supports the firmware.
- Detector battery is sufficient (wireless models).
- Stable power supply is available.
- Original configuration has been backed up.

---

# Required Tools

Hardware

- Detector
- Host Computer
- Stable Power Supply

Software

- SDK Tool
- Firmware Upgrade Tool

---

# Required Files

- Firmware Package
- Detector.log
- Detector Configuration
- Calibration Templates (backup if required)

---

# Safety Precautions

Before upgrading:

- Never disconnect power during upgrade.
- Never disconnect the communication cable.
- Verify firmware compatibility.
- Close unnecessary applications.
- Backup detector configuration before upgrading.

---

# Upgrade Workflow

```text
Verify Environment

↓

Verify Firmware

↓

Backup Information

↓

Execute Upgrade

↓

Wait for Completion

↓

Restart Detector

↓

Reconnect Detector

↓

Verify Firmware Version

↓

Verify Image Acquisition

↓

Complete Upgrade
```

---

# Procedure

## Step 1 – Verify Environment

### Process

- Verify detector communication.
- Verify detector status.
- Verify firmware version.
- Verify SDK version.

### Acceptance Criteria

Detector status is Ready.

---

## Step 2 – Verify Firmware Package

### Process

- Verify detector model.
- Verify firmware version.
- Verify firmware file integrity.
- Confirm firmware compatibility.

### Acceptance Criteria

Firmware package matches detector.

---

## Step 3 – Backup Information

### Process

Record:

- Detector Serial Number
- Firmware Version
- SDK Version
- Detector Configuration

Archive:

- Detector.log
- Calibration Templates (if required)

### Acceptance Criteria

Backup completed.

---

## Step 4 – Execute Firmware Upgrade

### Process

Execute:

Cmd_UpdateFirmware

Monitor:

- Progress
- Task status
- Error events

### Acceptance Criteria

Task completed successfully.

---

## Step 5 – Restart Detector

### Process

Power cycle detector.

Reconnect detector.

### Acceptance Criteria

Detector reconnects successfully.

---

## Step 6 – Verify Firmware

### Process

Read:

- Firmware Version
- Detector Information

Compare with expected version.

### Acceptance Criteria

Firmware version updated correctly.

---

## Step 7 – Verify Detector Functions

### Process

- Connect detector.
- Acquire test image.
- Verify communication.
- Verify calibration availability.

### Acceptance Criteria

Detector operates normally.

---

## Step 8 – Complete Upgrade

### Process

Save:

- Detector.log
- Upgrade Record
- Firmware Version
- Operator
- Date

---

# Acceptance Checklist

- Firmware upgraded successfully.
- Detector restarted successfully.
- Detector reconnects.
- Firmware version correct.
- Communication normal.
- Image acquisition successful.
- No abnormal SDK events.

---

# Exception Matrix

| Symptom | Possible Cause | Action |
|----------|----------------|--------|
| Upgrade failed | Wrong firmware | Verify firmware package |
| Timeout | Communication unstable | Retry after communication recovery |
| Detector cannot reconnect | Firmware abnormal | Perform recovery procedure |
| Firmware fallback | Automatic rollback | Verify firmware and retry |
| Apply firmware failed | Internal upgrade failure | Preserve logs and escalate |

---

# Records

Record:

- Customer
- Detector Model
- Detector SN
- Original Firmware Version
- New Firmware Version
- SDK Version
- Upgrade Date
- Operator
- Detector.log

---

# Notes

- Upgrade only firmware released for the specific detector model.
- Do not interrupt power or communication during the upgrade.
- If the SDK reports **Err_FirmwareUpdated**, power-cycle the detector before reconnecting.
- If **Err_FPD_FirmwareFallback** occurs, preserve all logs before retrying.
- After upgrade, verify detector communication and image acquisition before returning the detector to service.

---

# Related Documents

- 02_SDK
- 03_Hardware
- 06_Workflow/FirmwareUpgrade
- 09_DecisionTree/Firmware
- 11_Case/Firmware
- 12_ErrorCode/Firmware
- 14_Glossary/Firmware
- SOP/DetectorInstallation
- SOP/Calibration

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |