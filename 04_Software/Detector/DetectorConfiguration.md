# Detector Configuration

> iDetector Detector Configuration

---

# 1. Purpose

The **Detector Configuration** page provides configuration and management functions for the connected detector.

It allows engineers to configure detector operating parameters, communication parameters, working modes, and device-specific settings required for normal operation. Proper detector configuration is essential for stable communication, reliable image acquisition, and correct detector behavior.

---

# 2. Scope

This document describes the detector configuration functions provided by the **Detector** page of the iDetector software.

Typical functions include:

- Viewing detector configuration
- Modifying detector parameters
- Saving detector configuration
- Loading detector configuration
- Restoring default configuration
- Verifying configuration status

The actual configuration items depend on the detector model, firmware version, SDK version, and iDetector software version.

---

# 3. Functional Description

The Detector Configuration page is used to configure operational parameters for the connected detector.

Typical configurable items may include:

- Communication Parameters
- Network Parameters
- Detector Operating Mode
- Acquisition Parameters
- Device Preferences
- System Parameters

The available configuration items vary according to detector type and software version.

---

# 4. Engineering Applications

Typical engineering scenarios include:

- Initial detector deployment
- Customer site configuration
- Detector replacement
- Network configuration
- Communication parameter adjustment
- Factory configuration verification
- Engineering maintenance
- Restoring detector settings

---

# 5. Typical Workflow

```text
Launch iDetector

↓

Connect Detector

↓

Open Detector Configuration

↓

Review Current Configuration

↓

Modify Required Parameters

↓

Save Configuration

↓

Verify Configuration

↓

Return Detector to Ready State
```

---

# 6. Configuration Principles

Before modifying detector parameters, engineers should:

- Confirm the detector is connected.
- Verify the detector model.
- Understand the purpose of each parameter.
- Record the original configuration if required.
- Confirm parameter compatibility with the current firmware and SDK versions.

Configuration changes should be performed only when necessary.

---

# 7. Configuration Verification

After saving configuration changes, verify:

- Configuration saved successfully.
- Detector remains connected.
- Detector status is **Ready**.
- Communication is stable.
- Image acquisition functions normally.
- Calibration functions normally (if applicable).

---

# 8. Common Engineering Scenarios

Typical configuration operations include:

- Configuring a newly installed detector
- Adjusting communication settings
- Restoring factory configuration
- Preparing detectors for customer delivery
- Updating configuration after firmware upgrade
- Verifying detector settings after maintenance

---

# 9. Common Issues

Typical configuration-related issues include:

- Configuration cannot be saved
- Configuration changes not applied
- Detector becomes unavailable after configuration
- Invalid parameter values
- Communication failure after configuration
- Configuration inconsistent with detector firmware

Refer to the corresponding Failure Knowledge and Decision Tree documents for troubleshooting procedures.

---

# 10. Best Practices

Engineers are recommended to:

- Modify only parameters required for the current task.
- Avoid changing unknown parameters.
- Verify detector status after configuration.
- Keep records of configuration changes during engineering support.
- Confirm successful image acquisition after configuration changes.

---

# 11. Related Documents

### Software Module

- README.md
- DeviceList.md
- DetectorInformation.md
- DetectorConnection.md
- DetectorStatus.md
- DetectorActivation.md

### Knowledge Base

- ../../03_Hardware
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case
- ../../12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Detector Configuration documentation |