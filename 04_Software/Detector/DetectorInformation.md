# Detector Information

> iDetector Detector Information

---

# 1. Purpose

The **Detector Information** page provides detailed hardware and software information for the currently selected detector.

It enables engineers to verify detector identity, confirm hardware and firmware information, check communication status, and collect essential device information for installation, maintenance, troubleshooting, firmware upgrades, and technical support.

---

# 2. Scope

This document describes the **Detector Information** page of the iDetector software.

Typical functions include:

- Viewing detector information
- Verifying detector identity
- Confirming firmware information
- Viewing hardware information
- Viewing communication information
- Collecting device information for technical support

The actual interface and displayed information depend on the corresponding iDetector software version and detector model.

---

# 3. Functional Description

The Detector Information page displays the current operating information of the selected detector.

Typical information includes:

- Detector Name
- Detector Model
- Detector Serial Number (SN)
- Detector ID
- Firmware Version
- FPGA Version
- SDK Version
- Hardware Version
- Communication Mode
- Connection Status
- Battery Status (Wireless Models)
- Network Information (Wireless Models)

The available information may vary depending on detector type and software version.

---

# 4. Engineering Applications

The Detector Information page is commonly used for:

- Confirming detector identity before operation
- Verifying detector model
- Checking firmware version
- Confirming hardware version
- Collecting detector information before firmware upgrade
- Recording detector information for RMA
- Providing detector information during technical support

---

# 5. Typical Workflow

```text
Launch iDetector

↓

Open Detector Page

↓

Select Target Detector

↓

Open Detector Information

↓

Verify Detector Identity

↓

Verify Firmware Version

↓

Verify Hardware Information

↓

Record Required Information

↓

Continue Engineering Operation
```

---

# 6. Information Verification Checklist

Before performing engineering operations, it is recommended to verify:

- Detector Model
- Serial Number (SN)
- Firmware Version
- Hardware Version
- Connection Status
- Communication Mode
- SDK Compatibility
- Detector Online Status

If any information is abnormal, investigate before proceeding with calibration, acquisition, or firmware upgrade.

---

# 7. Common Engineering Scenarios

Typical scenarios include:

- New detector installation
- Detector replacement
- Firmware upgrade preparation
- Technical support
- Factory acceptance testing
- Customer site inspection
- Engineering quality verification
- RMA information collection

---

# 8. Common Issues

Typical issues include:

- Detector information not displayed
- Firmware version unavailable
- Serial number missing
- Incorrect detector model
- Hardware information unavailable
- Detector reported as Offline
- Communication information abnormal

Refer to the corresponding Failure Knowledge and Decision Tree documents for troubleshooting procedures.

---

# 9. Related Documents

### Software Module

- README.md
- DeviceList.md
- DetectorConnection.md
- DetectorStatus.md
- DetectorConfiguration.md
- DetectorActivation.md

### Knowledge Base

- 03_Hardware
- 06_Workflow
- 07_FailureKnowledge
- 09_DecisionTree
- 10_SOP
- 11_Case
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Detector Information documentation |