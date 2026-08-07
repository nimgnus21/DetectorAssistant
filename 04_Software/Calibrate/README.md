# Calibrate

> iDetector Calibration Module

---

# 1. Purpose

The **Calibrate** module is responsible for detector calibration management within the iDetector software.

This module provides the operational interface for generating, managing, loading, and verifying detector calibration data. Proper calibration ensures image consistency, detector stability, and diagnostic image quality.

The Calibrate module is one of the most important engineering functions during detector commissioning, maintenance, factory testing, and troubleshooting.

---

# 2. Scope

This module documents all functions available under the **Calibrate** page of the iDetector software.

Typical functions include:

- Offset Calibration
- Gain Calibration
- Defect Calibration
- Dynamic Correction
- Calibration File Management
- Calibration Status
- Calibration Verification

The descriptions in this module shall follow the corresponding iDetector software version.

---

# 3. Module Objectives

The Calibrate module enables engineers to:

- Generate calibration data
- Load calibration files
- Verify calibration status
- Execute detector calibration procedures
- Improve image quality
- Eliminate detector artifacts
- Restore detector calibration after maintenance

---

# 4. Functional Overview

The Calibrate page provides all detector calibration-related functions.

Typical functions include:

- Offset Calibration
- Gain Calibration
- Defect Calibration
- Dynamic Correction
- Calibration File Loading
- Calibration Result Display
- Calibration Status
- Calibration History

The available functions may vary depending on the detector model, SDK version, firmware version, and software version.

---

# 5. Documentation Structure

The Calibrate module consists of documents describing each functional area of the calibration page.

Recommended documentation includes:

```text
Calibrate
│
├── README.md
├── OffsetCalibration.md
├── GainCalibration.md
├── DefectCalibration.md
├── DynamicCorrection.md
├── CalibrationFile.md
├── CalibrationStatus.md
├── CalibrationVerification.md
└── FAQ.md
```

Document names may be adjusted according to the actual iDetector interface and terminology.

---

# 6. Typical Engineering Workflow

Typical calibration workflow:

```text
Launch iDetector

↓

Connect Detector

↓

Confirm Detector Status

↓

Open Calibrate Page

↓

Select Calibration Type

↓

Acquire Calibration Images

↓

Generate Calibration Data

↓

Load Calibration File

↓

Verify Calibration Result

↓

Complete Calibration
```

---

# 7. Common Engineering Tasks

Typical engineering operations include:

- Initial detector calibration
- Recalibration after detector replacement
- Recalibration after firmware upgrade
- Image artifact correction
- Calibration file regeneration
- Calibration file loading
- Calibration result verification
- Calibration status inspection

---

# 8. Relationship with Other Modules

The Calibrate module works together with other software modules.

| Module | Relationship |
|----------|--------------|
| Detector | Provides detector connection and device information |
| Acquire | Uses calibration data during image acquisition |
| SDK | Executes calibration through SDK interfaces |
| Settings | Provides calibration-related configuration |
| Upgrade | Calibration verification after firmware upgrade |
| Log | Records calibration operations and diagnostic logs |

---

# 9. Related Knowledge Base Modules

The Calibrate page is closely related to the following DetectorAssistant modules.

| Knowledge Module | Purpose |
|------------------|---------|
| 02_SDK | Calibration APIs and SDK interfaces |
| 03_Hardware | Detector hardware architecture |
| 05_Calibration | Calibration principles and algorithms |
| 06_Workflow | Calibration workflow |
| 07_FailureKnowledge | Calibration failure analysis |
| 08_ImageDiagnosis | Image quality evaluation |
| 09_DecisionTree | Calibration troubleshooting |
| 10_SOP | Standard calibration procedures |
| 11_Case | Calibration-related engineering cases |
| 12_ErrorCode | Calibration-related error codes |

---

# 10. Documentation Principles

Each document within the Calibrate module should follow a consistent structure.

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

# 11. Related Documents

### Software Module

- ../README.md
- ../Home/README.md
- ../Detector/README.md
- ../Acquire/README.md
- ../SDK/README.md
- ../Settings/README.md
- ../Upgrade/README.md
- ../Log/README.md

### Knowledge Base

- ../../02_SDK
- ../../03_Hardware
- ../../05_Calibration
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../08_ImageDiagnosis
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case
- ../../12_ErrorCode
- ../../17_Tools

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Calibrate module documentation |