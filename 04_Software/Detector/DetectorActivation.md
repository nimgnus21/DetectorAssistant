# Detector Activation

> iDetector Detector Activation

---

# 1. Purpose

The **Detector Activation** page is responsible for activating, registering, and verifying supported detectors within the iDetector software.

Detector activation establishes the operational relationship between the detector, firmware, SDK, and software environment, ensuring that the detector can be used normally for image acquisition, calibration, and engineering operations.

Some detector models or deployment environments may not require manual activation. The availability of this function depends on the detector model, firmware version, SDK version, licensing mechanism, and iDetector software version.

---

# 2. Scope

This document describes the detector activation functions provided by the **Detector** page of the iDetector software.

Typical functions include:

- Detector Activation
- Activation Status Verification
- Device Registration
- License Verification
- Activation Information
- Activation Result Confirmation

The actual functions available shall follow the corresponding iDetector software version.

---

# 3. Functional Description

The Detector Activation page is used to initialize or activate a detector before it enters normal operation.

Typical activation-related information may include:

- Activation Status
- Detector Identification
- Device Registration Information
- License Information
- Activation Result
- Activation Time
- Activation History

The displayed information may vary depending on detector model and software version.

---

# 4. Engineering Applications

Typical engineering scenarios include:

- Initial detector deployment
- Factory acceptance testing
- Customer site installation
- Detector replacement
- License replacement
- System migration
- Detector recovery after maintenance
- Engineering verification

---

# 5. Typical Workflow

```text
Launch iDetector

↓

Connect Detector

↓

Open Detector Activation

↓

Verify Detector Information

↓

Perform Activation (if required)

↓

Verify Activation Result

↓

Confirm Detector Status

↓

Ready for Normal Operation
```

---

# 6. Activation Verification Checklist

After detector activation, engineers should verify:

- Detector activation completed successfully.
- Detector status is **Ready**.
- Detector can establish communication normally.
- Detector information is displayed correctly.
- Image acquisition functions normally.
- Calibration functions are available.
- No activation-related warning or error is displayed.

---

# 7. Common Engineering Scenarios

Typical activation operations include:

- Activating a newly delivered detector
- Re-activating a detector after system replacement
- Verifying activation after firmware update
- Confirming detector authorization
- Validating detector availability before customer delivery
- Restoring detector operation after maintenance

---

# 8. Common Issues

Typical activation-related issues include:

- Detector activation failed
- Activation button unavailable
- Activation timeout
- Invalid activation information
- License verification failed
- Detector remains unavailable after activation
- Activation completed but detector cannot be connected

Refer to the corresponding Failure Knowledge, Decision Tree, and Error Code modules for troubleshooting procedures.

---

# 9. Best Practices

Engineers are recommended to:

- Verify detector information before activation.
- Confirm firmware and SDK compatibility.
- Perform activation in a stable communication environment.
- Record activation information for engineering records.
- Verify detector operation after activation.
- Confirm successful image acquisition before delivering the detector.

---

# 10. Related Documents

### Software Module

- README.md
- DeviceList.md
- DetectorInformation.md
- DetectorConnection.md
- DetectorStatus.md
- DetectorConfiguration.md

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
| v1.0 | 2026-08-07 | Initial Detector Activation documentation |