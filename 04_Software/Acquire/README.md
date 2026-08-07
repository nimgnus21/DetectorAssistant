# Acquire

> iDetector Image Acquisition Module

---

# 1. Purpose

The **Acquire** module is responsible for image acquisition and image management within the iDetector software.

This module provides the primary operating interface for detector exposure, image reception, image display, and image storage. It is the core functional module used during detector testing, clinical integration, factory verification, and field troubleshooting.

---

# 2. Scope

This module documents all functions available under the **Acquire** page of the iDetector software.

Typical functions include:

- Image acquisition
- Exposure control
- Image reception
- Image preview
- Image management
- Image saving
- Image export
- Acquisition status monitoring

The descriptions in this module shall follow the corresponding iDetector software version.

---

# 3. Module Objectives

The Acquire module enables engineers to:

- Acquire detector images
- Monitor acquisition progress
- Display acquired images
- Save acquired images
- Export image files
- Verify image quality
- Assist troubleshooting of image-related issues

---

# 4. Functional Overview

The Acquire page is the primary workspace for detector image acquisition.

Typical functions include:

- Exposure
- Image Reception
- Image Preview
- Image Display
- Window/Level Adjustment
- Zoom
- Pan
- Image Save
- Image Export
- Acquisition Status

The available functions may vary depending on the software version, detector model, acquisition mode, and user permissions.

---

# 5. Documentation Structure

The Acquire module consists of documents describing each functional area of the Acquire page.

Recommended documentation includes:

```text
Acquire
│
├── README.md
├── ImageAcquisition.md
├── Exposure.md
├── ImageDisplay.md
├── WindowLevel.md
├── ImageSave.md
├── ImageExport.md
├── AcquisitionStatus.md
└── FAQ.md
```

Document names may be adjusted according to the actual iDetector interface.

---

# 6. Typical Engineering Workflow

Typical acquisition workflow:

```text
Launch iDetector

↓

Connect Detector

↓

Configure Detector

↓

Open Acquire Page

↓

Prepare Exposure

↓

Start Exposure

↓

Receive Image

↓

Review Image

↓

Save / Export Image
```

---

# 7. Common Engineering Tasks

Typical engineering operations include:

- Verifying detector communication
- Performing image acquisition tests
- Evaluating image quality
- Saving RAW images
- Exporting image data
- Verifying exposure success
- Confirming detector readiness
- Supporting customer image verification

---

# 8. Relationship with Other Modules

The Acquire module works together with other software modules.

| Module | Relationship |
|----------|--------------|
| Home | Displays acquisition summary and software status |
| Detector | Provides connected detector |
| Calibrate | Provides correction data for acquired images |
| SDK | Controls detector acquisition through SDK |
| Settings | Provides acquisition-related configuration |
| Log | Records acquisition events and diagnostic logs |

---

# 9. Related Knowledge Base Modules

The Acquire page is closely related to the following DetectorAssistant modules.

| Knowledge Module | Purpose |
|------------------|---------|
| 02_SDK | Acquisition API and callback interfaces |
| 03_Hardware | Detector imaging hardware |
| 05_Calibration | Image correction principles |
| 06_Workflow | Image acquisition workflow |
| 07_FailureKnowledge | Image acquisition failures |
| 08_ImageDiagnosis | Image quality analysis |
| 09_DecisionTree | Image troubleshooting |
| 10_SOP | Standard acquisition procedures |
| 11_Case | Image-related engineering cases |
| 12_ErrorCode | Acquisition-related error codes |

---

# 10. Documentation Principles

Each document within the Acquire module should follow a consistent structure.

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
- ../Calibrate/README.md
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

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Acquire module documentation |