# Firmware Upgrade

> iDetector Software Module - Firmware Upgrade

---

# 1. Purpose

The **Firmware Upgrade** function is used to update detector firmware using the applicable released firmware package and upgrade workflow.

Firmware upgrades may be performed for version compatibility, approved defect correction, supported function changes, maintenance or project delivery requirements.

Firmware upgrades should only be performed using the correct package for the applicable detector model and supported software environment.

---

# 2. Scope

This document describes the standard firmware upgrade workflow used by the iDetector software environment.

It covers:

- Package selection
- Pre-upgrade verification
- Upgrade execution
- Interruption prevention
- Post-upgrade verification
- Failure evidence collection

---

# 3. Preconditions

Before upgrading, confirm:

- Detector model and SN
- Current firmware version
- Target firmware version
- Applicable SDK/software version
- Correct upgrade package
- Stable detector communication
- Stable power supply
- Sufficient battery for applicable wireless products
- Upgrade environment is ready

If any version or package compatibility is uncertain, stop and obtain the required technical confirmation before starting.

---

# 4. Standard Workflow

```text
Identify Detector
        ↓
Record Current Versions
        ↓
Verify Model / Package / SDK Compatibility
        ↓
Verify Power and Communication Stability
        ↓
Start Upgrade
        ↓
Do Not Interrupt Upgrade
        ↓
Upgrade Completion
        ↓
Restart / Reconnect as Required
        ↓
Verify Firmware Version
        ↓
Verify Communication
        ↓
Acquire Test Image
        ↓
Record Result
```

---

# 5. Execution Rules

## Before Upgrade

Record:

- Detector model
- Detector SN
- Current firmware version
- Target firmware version
- SDK version
- Upgrade package name

Confirm the detector is connected and communication is normal.

## During Upgrade

Do not:

- Disconnect the detector
- Power off the detector
- Close the upgrade software
- Interrupt the communication path

Preserve the displayed upgrade status if an abnormality occurs.

## After Upgrade

Verify:

- Firmware version
- Detector status
- Detector reconnection
- Communication stability
- Image acquisition

Perform additional functional verification required by the applicable product or project.

---

# 6. Failure Handling

If the upgrade fails, record the failure before repeated attempts whenever possible.

Collect:

- Detector.log
- Detector model and SN
- Current/target firmware version
- SDK and upgrade tool version
- Upgrade package name
- Error code/message
- Screenshot
- Failure stage
- Post-failure detector connection status

Do not describe an incomplete upgrade as successful solely because the software process ended.

---

# 7. Post-Upgrade Acceptance

The upgrade is accepted only after the required checks are complete:

- Firmware version matches the intended target
- Detector reconnects successfully
- Detector status is normal
- Image acquisition completes normally
- No new abnormal communication or image phenomenon is observed

When calibration data or product-specific configuration must be restored or verified after an upgrade, follow the applicable product procedure.

---

# 8. Common Failure Directions

| Symptom | Primary Check |
|---|---|
| Upgrade cannot start | Detector connection and package applicability |
| Package rejected | Model/version compatibility |
| Upgrade interrupted | Power and communication stability |
| Detector cannot reconnect | Upgrade state and recovery path |
| Version does not match target | Correct package and version verification |
| Image abnormal after upgrade | Product configuration and required functional verification |

---

# 9. Related Documents

- UpgradeWorkflow.md
- VersionVerification.md
- UpgradeFailure.md
- ../../04_Software/Log
- ../../05_Calibration
- ../../07_FailureKnowledge
- ../../10_SOP
- ../../12_ErrorCode
- ../../13_Template/Work/LogCollection.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added preconditions, failure evidence and acceptance criteria |
| v1.0 | 2026-08-07 | Initial Firmware Upgrade documentation |