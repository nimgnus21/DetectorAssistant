# Device List

> iDetector Device List

---

# 1. Purpose

The **Device List** page is the primary interface for discovering, displaying, selecting, and managing detectors within the iDetector software.

It provides engineers with a centralized view of all available detectors and serves as the starting point for detector connection, status verification, and device management.

---

# 2. Scope

This document describes the Device List page of the iDetector software.

Typical functions include:

- Displaying available detectors
- Refreshing the device list
- Selecting a detector
- Viewing detector status
- Opening detector management functions

The actual interface and available functions depend on the corresponding iDetector software version.

---

# 3. Functional Description

The Device List is responsible for presenting detector information detected by the software.

Typical information displayed may include:

- Detector Name
- Device ID
- Serial Number
- Communication Status
- Connection Status
- Detector Model
- Firmware Version
- SDK Status

The displayed information varies depending on the detector type and software version.

---

# 4. Typical Workflow

A typical workflow is shown below.

```text
Launch iDetector

↓

Open Detector Page

↓

Search Available Devices

↓

Display Device List

↓

Select Target Detector

↓

Verify Device Information

↓

Connect Detector

↓

Ready for Operation
```

---

# 5. Engineering Applications

Typical engineering scenarios include:

- Connecting a newly installed detector
- Verifying detector communication
- Confirming detector identification
- Checking detector online status
- Selecting the detector for image acquisition
- Confirming detector firmware information

---

# 6. Common Issues

Typical issues related to the Device List include:

- No detector displayed
- Detector shown as Offline
- Duplicate detector entries
- Detector cannot be selected
- Detector information incomplete
- Device list refresh failure

Detailed troubleshooting procedures are described in the corresponding Failure Knowledge and Decision Tree modules.

---

# 7. Related Documents

### Software Module

- README.md
- DetectorInformation.md
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

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Device List documentation |