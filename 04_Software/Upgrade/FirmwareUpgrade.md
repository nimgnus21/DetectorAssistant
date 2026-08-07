# Firmware Upgrade

> iDetector Software Module - Firmware Upgrade

---

# 1. Purpose

The **Firmware Upgrade** function is used to update the detector firmware stored inside the Flat Panel Detector (FPD).

Firmware upgrades are performed to:

- Fix known software defects
- Improve detector stability
- Support new detector functions
- Improve communication compatibility
- Match SDK and detector versions
- Meet project delivery requirements

Firmware upgrades should only be performed using officially released firmware packages.

---

# 2. Scope

This document describes the firmware upgrade function provided by the **Upgrade** module of iDetector.

It includes:

- Firmware selection
- Upgrade process
- Version verification
- Upgrade precautions
- Recovery recommendations

---

# 3. Applicable Scenarios

Firmware Upgrade is typically performed during:

- Factory production
- Detector maintenance
- Customer deployment
- Firmware bug fixing
- Detector replacement
- Version compatibility adjustment
- R&D verification

Firmware should **not** be upgraded during normal image acquisition.

---

# 4. Upgrade Prerequisites

Before upgrading firmware, verify the following items.

## Detector Status

- Detector connected successfully
- Detector communication normal
- Detector power supply stable
- Detector battery sufficient (Wireless Detector)
- Detector status is Ready

---

## Software Environment

- Correct firmware package
- Compatible SDK version
- Compatible detector model
- Stable network connection (Ethernet detector)

---

## Engineering Preparation

Record:

- Detector Model
- Detector Serial Number
- Current Firmware Version
- Target Firmware Version
- SDK Version

Backup detector configuration if required.

---

# 5. Typical Upgrade Workflow

```text
Connect Detector

↓

Read Detector Information

↓

Verify Current Firmware Version

↓

Select Firmware Package

↓

Start Upgrade

↓

Firmware Download

↓

Firmware Programming

↓

Upgrade Completed

↓

Restart Detector

↓

Verify Firmware Version

↓

Functional Verification
```

---

# 6. Operating Procedure

## Step 1

Connect the detector.

Verify:

- Communication normal
- Detector Ready

---

## Step 2

Open

Upgrade

↓

Firmware Upgrade

---

## Step 3

Select the correct firmware package.

Verify:

- Detector model
- Firmware version
- Firmware compatibility

---

## Step 4

Start firmware upgrade.

The software downloads the firmware to the detector.

---

## Step 5

Wait until programming finishes.

**Do NOT**

- Disconnect detector
- Close iDetector
- Power off detector
- Disconnect network cable

---

## Step 6

Upgrade completed.

Restart detector if required.

---

## Step 7

Reconnect detector.

Verify:

- Firmware Version
- Detector Status
- Image Acquisition
- Detector Communication

---

# 7. Upgrade Verification

After firmware upgrade, verify:

## Basic Verification

- Detector can connect.
- Detector status is normal.
- Detector firmware version is correct.
- Detector information is readable.

---

## Functional Verification

Verify:

- Image acquisition
- Image transfer
- Offset Calibration
- Gain Calibration
- Defect Correction
- Image display

---

## Engineering Verification

Acquire several images.

Confirm:

- Communication stable
- No abnormal artifacts
- Image quality normal
- Detector operates normally

---

# 8. Engineering Recommendations

Before upgrade:

- Verify firmware package.
- Record original firmware version.
- Ensure stable power supply.
- Close unnecessary software.

During upgrade:

- Do not disconnect detector.
- Do not restart computer.
- Do not interrupt network communication.
- Wait until upgrade completes.

After upgrade:

- Verify firmware version.
- Verify detector communication.
- Perform functional testing.
- Archive upgrade records.

---

# 9. Common Issues

| Problem | Possible Cause | Recommended Action |
|----------|----------------|--------------------|
| Upgrade cannot start | Detector not connected | Verify communication |
| Firmware package invalid | Wrong firmware package | Select correct firmware |
| Upgrade interrupted | Network disconnected | Reconnect and retry |
| Detector cannot reconnect | Firmware incomplete | Retry upgrade or contact R&D |
| Version mismatch | Incorrect firmware version | Upgrade compatible firmware |
| Image acquisition abnormal | Parameter mismatch | Verify detector configuration |

---

# 10. Best Practices

For every firmware upgrade:

✓ Record firmware version before upgrade.

✓ Record firmware version after upgrade.

✓ Record detector serial number.

✓ Verify SDK compatibility.

✓ Verify image acquisition.

✓ Save upgrade logs.

✓ Record abnormal phenomena.

---

# 11. Related Documents

## Upgrade Module

- README.md
- UpgradeWorkflow.md
- VersionVerification.md
- UpgradeFailure.md
- FAQ.md

## Related Knowledge Base

- ../../03_Hardware/Firmware.md
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case
- ../../12_ErrorCode
- ../../17_Tools/FirmwareUpgrade.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Firmware Upgrade documentation |