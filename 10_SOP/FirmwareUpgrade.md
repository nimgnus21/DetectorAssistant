# Firmware Upgrade

> Module: Standard Operating Procedure
>
> SOP ID: SOP-004
>
> Category: Firmware Upgrade
>
> Version: v1.1

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

Software / Diagnostics

- [Firmware Upgrade Tool](../17_Tools/SDKTool/FirmwareUpgrade.md)
- [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)
- [Log Viewer](../17_Tools/LogViewer/)（升级失败、超时或回退分析时）

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

### Exception Handling

Resolve communication failures first through the [Connection DecisionTree](../09_DecisionTree/Connection/) and preserve logs with [Log Viewer](../17_Tools/LogViewer/) if the state is unstable.

---

## Step 2 – Verify Firmware Package

### Process

- Verify detector model.
- Verify firmware version.
- Verify firmware file integrity.
- Confirm firmware compatibility.

### Acceptance Criteria

Firmware package matches detector.

### Exception Handling

Do not continue when model, package or compatibility is uncertain. Record the package and version information before escalation.

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

Use the [Firmware Upgrade Tool](../17_Tools/SDKTool/FirmwareUpgrade.md) or applicable [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md) workflow to execute the upgrade.

Monitor:

- Progress
- Task status
- Error events

### Acceptance Criteria

Task completed successfully.

### Exception Handling

On failure, timeout or abnormal rollback, stop repeated retries, preserve `Detector.log` and inspect it with [Log Viewer](../17_Tools/LogViewer/) before escalation.

---

## Step 5 – Restart Detector

### Process

Power cycle detector.

Reconnect detector.

### Acceptance Criteria

Detector reconnects successfully.

### Exception Handling

If the detector cannot reconnect, enter the [Connection DecisionTree](../09_DecisionTree/Connection/) and retain the upgrade log.

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

### Exception Handling

- Connection abnormal → [Connection DecisionTree](../09_DecisionTree/Connection/)
- Image abnormal → [Image Troubleshooting SOP](ImageTroubleshooting.md)
- Calibration abnormal → [Calibration SOP](Calibration.md)

---

## Step 8 – Complete Upgrade

### Process

Save:

- Detector.log
- Upgrade Record
- Firmware Version
- Operator
- Date
- Verification result

---

# Acceptance Checklist

- Firmware upgraded successfully.
- Detector restarted successfully.
- Detector reconnects.
- Firmware version correct.
- Communication normal.
- Image acquisition successful.
- No abnormal SDK events.
- Verification evidence retained.

---

# Exception Matrix

| Symptom | Direction | Action |
|----------|-----------|--------|
| Upgrade failed | Package or internal upgrade failure | Preserve logs and stop repeated retries |
| Timeout | Communication interruption | Recover communication before retry |
| Detector cannot reconnect | Upgrade or connection state abnormal | Run Connection DecisionTree |
| Firmware fallback | Automatic rollback or package/application issue | Preserve all logs before retrying |
| Apply firmware failed | Upgrade execution failure | Inspect logs and escalate with package/version information |

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
- Firmware package identification
- Final verification result

---

# Notes

- Upgrade only firmware released for the specific detector model.
- Do not interrupt power or communication during the upgrade.
- If the SDK reports **Err_FirmwareUpdated**, power-cycle the detector before reconnecting.
- If **Err_FPD_FirmwareFallback** occurs, preserve all logs before retrying.
- After upgrade, verify detector communication and image acquisition before returning the detector to service.

---

# Related Documents

- [Firmware Upgrade Tool](../17_Tools/SDKTool/FirmwareUpgrade.md)
- [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)
- [Log Viewer](../17_Tools/LogViewer/)
- [Firmware Upgrade Software Guide](../04_Software/Upgrade/FirmwareUpgrade.md)
- [Connection DecisionTree](../09_DecisionTree/Connection/)
- [Firmware DecisionTree](../09_DecisionTree/Firmware/)
- [Firmware Cases](../11_Case/Firmware/)
- [Detector Installation SOP](DetectorInstallation.md)
- [Calibration SOP](Calibration.md)
- [Image Troubleshooting SOP](ImageTroubleshooting.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added direct tool links and post-upgrade recovery flow |
| v1.0 | 2026-08-07 | Initial release |