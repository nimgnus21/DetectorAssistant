# Upgrade

> iDetector Firmware Upgrade Module

---

# 1. Purpose

The **Upgrade** module provides firmware upgrade and version management functions for supported detectors within the iDetector software.

This module allows engineers to safely upgrade detector firmware, verify firmware versions, monitor upgrade progress, and recover from upgrade-related failures. Proper firmware management ensures compatibility between the detector, SDK, and iDetector software.

---

# 2. Scope

This module documents all functions available under the **Upgrade** page of the iDetector software.

Typical functions include:

- Firmware Upgrade
- Firmware Package Selection
- Upgrade Progress
- Upgrade Status
- Version Verification
- Upgrade Recovery
- Upgrade History

The descriptions in this module shall follow the corresponding iDetector software version.

---

# 3. Module Objectives

The Upgrade module enables engineers to:

- Upgrade detector firmware
- Verify firmware versions
- Monitor upgrade progress
- Confirm upgrade completion
- Restore firmware when necessary
- Troubleshoot firmware upgrade failures
- Maintain firmware compatibility

---

# 4. Functional Overview

The Upgrade page provides centralized firmware management for supported detectors.

Typical functions include:

- Firmware File Selection
- Firmware Version Information
- Upgrade Control
- Upgrade Progress Monitoring
- Upgrade Status
- Upgrade Result
- Firmware Verification

The available functions may vary depending on the detector model, firmware version, SDK version, and software version.

---

# 5. Documentation Structure

The Upgrade module consists of documents describing each functional area of the Upgrade page.

Recommended documentation includes:

```text
Upgrade
│
├── README.md
├── FirmwareUpgrade.md
├── FirmwarePackage.md
├── UpgradeProcess.md
├── UpgradeProgress.md
├── UpgradeStatus.md
├── UpgradeRecovery.md
├── VersionVerification.md
└── FAQ.md
```

Document names may be adjusted according to the actual iDetector interface.

---

# 6. Typical Engineering Workflow

Typical firmware upgrade workflow:

```text
Launch iDetector

↓

Connect Detector

↓

Open Upgrade Page

↓

Verify Current Firmware Version

↓

Select Firmware Package

↓

Start Upgrade

↓

Monitor Upgrade Progress

↓

Verify Upgrade Result

↓

Restart Detector (if required)

↓

Confirm New Firmware Version
```

---

# 7. Common Engineering Tasks

Typical engineering operations include:

- Upgrading detector firmware
- Confirming firmware compatibility
- Verifying firmware version
- Recovering failed upgrades
- Checking upgrade status
- Recording firmware information
- Preparing firmware for customer deployment
- Supporting firmware troubleshooting

---

# 8. Relationship with Other Modules

The Upgrade module works together with other software modules.

| Module | Relationship |
|----------|--------------|
| Detector | Provides detector connection and device information |
| SDK | Provides firmware communication interface |
| Settings | Provides upgrade-related configuration |
| Log | Records upgrade events and diagnostic logs |
| Home | Displays detector firmware summary information |

---

# 9. Related Knowledge Base Modules

The Upgrade page is closely related to the following DetectorAssistant modules.

| Knowledge Module | Purpose |
|------------------|---------|
| 02_SDK | Firmware APIs and communication interfaces |
| 03_Hardware | Detector hardware information |
| 06_Workflow | Firmware upgrade workflow |
| 07_FailureKnowledge | Firmware-related failures |
| 09_DecisionTree | Firmware troubleshooting |
| 10_SOP | Firmware upgrade procedures |
| 11_Case | Firmware upgrade engineering cases |
| 12_ErrorCode | Firmware-related error codes |
| 17_Tools | Firmware upgrade utilities |

---

# 10. Documentation Principles

Each document within the Upgrade module should follow a consistent structure.

- Purpose
- Interface Location
- Functional Description
- Parameters
- Operating Procedure
- Notes
- Common Issues
- Related Documents
- Revision History

Descriptions should correspond to the actual iDetector interface and terminology.

---

# 11. Safety Recommendations

Before performing a firmware upgrade, engineers should:

- Verify detector communication is stable.
- Confirm the correct firmware package is selected.
- Ensure the detector power supply is reliable.
- Do not disconnect the detector during the upgrade.
- Do not terminate the iDetector software until the upgrade is complete.
- Verify the firmware version after the upgrade.

---

# 12. Related Documents

### Software Module

- ../README.md
- ../Home/README.md
- ../Detector/README.md
- ../Acquire/README.md
- ../Calibrate/README.md
- ../SDK/README.md
- ../Settings/README.md
- ../Log/README.md

### Knowledge Base

- ../../02_SDK
- ../../03_Hardware
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case
- ../../12_ErrorCode
- ../../17_Tools

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Upgrade module documentation |