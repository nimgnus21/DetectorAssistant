# Upgrade Workflow

> iDetector Software Module - Firmware Upgrade Workflow

---

# 1. Purpose

The **Upgrade Workflow** defines the standard operating procedure for detector firmware upgrades using the iDetector software.

A standardized workflow minimizes upgrade risks, ensures firmware compatibility, and improves upgrade success rates.

This document should be followed by Field Application Engineers (FAEs), Production Engineers, and Technical Support Engineers whenever detector firmware is upgraded.

---

# 2. Scope

This workflow applies to:

- Factory firmware programming
- Customer firmware upgrades
- Detector maintenance
- Firmware rollback
- Detector replacement
- Engineering verification

---

# 3. Upgrade Workflow

```text
Receive Upgrade Requirement

↓

Confirm Detector Model

↓

Read Detector Information

↓

Record Current Firmware Version

↓

Confirm Target Firmware Version

↓

Verify SDK Compatibility

↓

Verify Battery / Power Status

↓

Connect Detector

↓

Start Firmware Upgrade

↓

Wait Until Upgrade Completes

↓

Restart Detector

↓

Reconnect Detector

↓

Verify Firmware Version

↓

Perform Functional Test

↓

Complete Upgrade
```

---

# 4. Workflow Details

## Step 1 – Confirm Upgrade Requirement

Determine why the firmware upgrade is required.

Typical reasons include:

- Firmware bug fix
- Feature enhancement
- Compatibility update
- Customer requirement
- Factory production

---

## Step 2 – Identify Detector

Record the following information:

- Detector Model
- Detector Serial Number
- Detector Type
- Communication Mode

---

## Step 3 – Read Current Firmware

Record:

- Firmware Version
- FPGA Version (if applicable)
- SDK Version

These records provide a rollback reference if problems occur.

---

## Step 4 – Verify Firmware Package

Before upgrading, verify:

- Correct detector model
- Correct firmware package
- Firmware version
- Release source
- Compatibility

Never use firmware intended for another detector model.

---

## Step 5 – Verify Detector Status

Before upgrading, confirm:

- Detector connected successfully
- Communication stable
- Detector Ready
- Battery sufficient (Wireless detector)
- Power supply stable

---

## Step 6 – Start Upgrade

Open:

Upgrade

↓

Firmware Upgrade

↓

Select Firmware Package

↓

Start Upgrade

Do not interrupt the upgrade process.

---

## Step 7 – Wait for Completion

During firmware programming:

Do NOT

- Disconnect detector
- Close iDetector
- Restart computer
- Disconnect Ethernet
- Power off detector

Wait until the software reports upgrade completion.

---

## Step 8 – Restart Detector

Restart detector if required.

Reconnect detector.

Verify communication has recovered.

---

## Step 9 – Version Verification

Verify:

- Firmware Version
- Detector Information
- Detector Status

Ensure the displayed firmware version matches the target version.

---

## Step 10 – Functional Verification

Perform the following tests:

- Detector Connection
- Image Acquisition
- Image Display
- Communication Stability
- Calibration Function
- Image Saving

---

## Step 11 – Engineering Verification

Acquire multiple images.

Confirm:

- Image quality normal
- No communication error
- Detector stable
- Firmware operates correctly

---

# 5. Engineering Checklist

Before Upgrade

| Item | Status |
|-------|--------|
| Detector Connected | □ |
| Firmware Verified | □ |
| SDK Compatible | □ |
| Battery / Power Normal | □ |
| Network Stable | □ |

---

After Upgrade

| Item | Status |
|-------|--------|
| Firmware Updated | □ |
| Detector Connected | □ |
| Version Correct | □ |
| Image Acquisition Normal | □ |
| Communication Stable | □ |
| Functional Test Passed | □ |

---

# 6. Upgrade Risks

Possible risks include:

- Wrong firmware package
- Communication interruption
- Power failure
- Firmware corruption
- Detector not responding
- Version mismatch

All upgrade operations should be performed in a stable environment.

---

# 7. Best Practices

- Upgrade one detector at a time.
- Archive firmware packages.
- Record upgrade history.
- Verify functionality immediately after upgrade.
- Save upgrade logs.
- Keep previous firmware version information.

---

# 8. Related Documents

## Upgrade Module

- README.md
- FirmwareUpgrade.md
- VersionVerification.md
- UpgradeFailure.md
- FAQ.md

## Knowledge Base

- ../../03_Hardware/Firmware.md
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case
- ../../17_Tools/FirmwareUpgrade.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Upgrade Workflow documentation |