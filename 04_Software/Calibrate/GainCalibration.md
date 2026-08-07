# Gain Calibration

> iDetector Calibrate Module - Gain Calibration

---

# 1. Purpose

**Gain Calibration** is used to compensate for pixel response non-uniformity under X-ray exposure.

After Gain Calibration, a Gain Template is generated and used together with the Offset Template during image correction to improve detector uniformity.

According to the iDetector User Manual, Gain Calibration shall be performed **after Offset Calibration has been successfully completed**.

---

# 2. Scope

This document describes the **Create Gain** function in the **Calibrate** page of iDetector.

It includes:

- Gain calibration principle
- Gain template generation
- Calibration workflow
- Engineering precautions
- Common issues

---

# 3. Calibration Principle

Gain Calibration acquires multiple flat-field images under stable X-ray exposure conditions.

The acquired images are analyzed to calculate the response coefficient of each detector pixel, generating the Gain Template.

The Gain Template is subsequently used during image acquisition to compensate detector response differences and improve image uniformity.

---

# 4. Prerequisites

Before starting Gain Calibration, verify that:

- Offset Calibration has completed successfully.
- Detector communication is normal.
- X-ray generator operates normally.
- Exposure parameters are stable.
- Detector position remains unchanged.
- No objects are present in the exposure field.

---

# 5. Typical Workflow

```text
Connect Detector

↓

Open Calibrate

↓

Select Create Gain

↓

Verify Offset Template

↓

Prepare Uniform X-ray Exposure

↓

Click Start

↓

Acquire Flat-field Images

↓

Generate Gain Template

↓

Calibration Completed
```

---

# 6. Operating Procedure

### Step 1

Connect the detector and confirm **Ready** status.

---

### Step 2

Open:

Calibrate

↓

Create Gain

---

### Step 3

Confirm that a valid Offset Template already exists.

---

### Step 4

Prepare a uniform radiation field according to the calibration requirements.

Ensure:

- No object in the beam
- Stable tube output
- Stable SID
- Stable detector position

---

### Step 5

Click **Start** to begin Gain Calibration.

The detector continuously acquires calibration images.

---

### Step 6

Wait until Gain Template generation finishes.

Do not interrupt detector communication during calibration.

---

### Step 7

Verify calibration completed successfully.

---

# 7. Expected Result

After successful Gain Calibration:

- Gain Template is generated.
- Detector uniformity is improved.
- Image brightness becomes more consistent.
- Detector is ready for Defect Calibration if required.

---

# 8. Engineering Recommendations

Before calibration:

- Complete Offset Calibration first.
- Verify generator output stability.
- Use a uniform radiation field.
- Avoid detector movement.

During calibration:

- Do not change exposure parameters.
- Do not disconnect the detector.
- Monitor calibration progress.

After calibration:

- Verify image uniformity.
- Archive calibration records.
- Continue with Defect Calibration if necessary.

---

# 9. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Gain calibration failed | Offset template unavailable |
| Calibration interrupted | Communication abnormal |
| Non-uniform result | Exposure field not uniform |
| Gain template invalid | Exposure unstable |
| Brightness still uneven | Offset or Gain calibration abnormal |

---

# 10. Related Documents

## Calibrate Module

- README.md
- OffsetCalibration.md
- DefectCalibration.md
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
| v1.0 | 2026-08-07 | Initial Gain Calibration documentation based on iDetector User Manual |