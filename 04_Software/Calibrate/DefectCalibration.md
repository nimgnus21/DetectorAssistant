# Defect Calibration

> iDetector Calibrate Module - Defect Calibration

---

# 1. Purpose

**Defect Calibration** is used to identify abnormal detector pixels and generate a Defect Template.

The generated template is used during image correction to compensate defective pixels and improve image quality.

According to the iDetector calibration workflow, Defect Calibration should be performed **after Offset Calibration and Gain Calibration have been successfully completed**.

---

# 2. Scope

This document describes the **Create Defect** function in the **Calibrate** page of iDetector.

It includes:

- Defect template generation
- Calibration workflow
- Engineering precautions
- Verification methods
- Common issues

---

# 3. Calibration Principle

Defect Calibration analyzes detector response using previously generated calibration templates.

During calibration, the software identifies abnormal detector pixels that exceed predefined thresholds and generates a Defect Template for subsequent image correction.

The Defect Template is applied automatically when Defect Correction is enabled.

---

# 4. Prerequisites

Before starting Defect Calibration, verify:

- Offset Calibration completed successfully.
- Gain Calibration completed successfully.
- Detector communication is normal.
- Detector status is **Ready**.
- Calibration templates are valid.

---

# 5. Typical Workflow

```text
Connect Detector

↓

Open Calibrate

↓

Select Create Defect

↓

Verify Offset Template

↓

Verify Gain Template

↓

Click Start

↓

Generate Defect Template

↓

Calibration Completed
```

---

# 6. Operating Procedure

### Step 1

Connect the detector and confirm it is in the **Ready** state.

---

### Step 2

Open:

Calibrate

↓

Create Defect

---

### Step 3

Verify that valid Offset and Gain Templates already exist.

---

### Step 4

Click **Start** to begin Defect Calibration.

The software analyzes detector response and generates the Defect Template.

---

### Step 5

Wait until template generation completes.

Do not interrupt detector communication during this process.

---

### Step 6

Confirm that the Defect Template has been generated successfully.

---

# 7. Expected Result

After successful Defect Calibration:

- Defect Template is generated.
- Defect correction becomes available.
- Defective pixels are compensated during image processing.
- Image quality is improved.

---

# 8. Engineering Recommendations

Before calibration:

- Complete Offset Calibration.
- Complete Gain Calibration.
- Ensure detector communication is stable.

During calibration:

- Do not disconnect the detector.
- Do not perform image acquisition simultaneously.
- Monitor calibration progress.

After calibration:

- Acquire a verification image.
- Confirm that defective pixels have been corrected.
- Archive calibration records if required.

---

# 9. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Defect Calibration failed | Offset or Gain Template missing |
| Calibration interrupted | Communication abnormal |
| Defect Template invalid | Previous calibration abnormal |
| Bad pixels still visible | Defect Correction disabled or template not applied |

---

# 10. Verification

After calibration, verify:

- Defect Template exists.
- Defect Correction can be enabled.
- Test images show no obvious bad pixels.
- Image quality meets engineering requirements.

---

# 11. Related Documents

## Calibrate Module

- README.md
- OffsetCalibration.md
- GainCalibration.md
- GhostCalibration.md
- CalibrationStatus.md
- CalibrationLog.md
- FAQ.md

## Knowledge Base

- ../../05_Calibration
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Defect Calibration documentation based on iDetector User Manual |