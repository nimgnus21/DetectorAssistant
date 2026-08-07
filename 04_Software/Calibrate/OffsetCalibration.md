# Offset Calibration

> iDetector Calibrate Module - Offset Calibration

---

# 1. Purpose

**Offset Calibration** is the first step of detector image calibration.

Its purpose is to collect detector dark-field data without X-ray exposure and generate the Offset Template, providing the baseline for subsequent Gain Calibration and Defect Calibration.

According to the iDetector User Manual, Offset Calibration is divided into:

- Pre-Offset Calibration
- Post-Offset Calibration

Pre-Offset is performed without X-ray exposure, while Post-Offset is used under specific detector operating conditions.

---

# 2. Scope

This document describes the **Create Offset** function in the **Calibrate** page of iDetector.

It includes:

- Offset calibration principles
- Offset template generation
- Engineering workflow
- Precautions
- Common issues

---

# 3. Calibration Principle

Offset Calibration acquires multiple dark-field images under stable detector operating conditions and generates an Offset Template.

According to the iDetector User Manual:

- Offset Calibration removes detector background signals.
- Gain Calibration depends on Offset Calibration results.
- Defect Calibration also depends on previously generated calibration templates.

Therefore, Offset Calibration must be completed before subsequent calibration operations. :contentReference[oaicite:0]{index=0}

---

# 4. Calibration Types

## Pre-Offset Calibration

Pre-Offset Calibration is performed **without X-ray exposure**.

Multiple dark-field images are collected and used to generate the Offset Template.

This is the most common Offset calibration method.

---

## Post-Offset Calibration

Post-Offset Calibration is used under specific detector operating modes.

Whether Post-Offset calibration is available depends on the detector model and firmware.

---

# 5. Typical Workflow

```text
Connect Detector

↓

Open Calibrate

↓

Select Create Offset

↓

Verify Detector Ready

↓

Click

Start create offset template file

↓

Acquire Dark Images

↓

Generate Offset Template

↓

Calibration Completed
```

This workflow follows the Offset template generation process described in the iDetector User Manual. :contentReference[oaicite:1]{index=1}

---

# 6. Operating Procedure

### Step 1

Connect the detector successfully.

---

### Step 2

Open

Calibrate

↓

Create Offset

---

### Step 3

Click

**Start create offset template file**

to start Offset template generation.

:contentReference[oaicite:2]{index=2}

---

### Step 4

Wait until Offset template generation completes.

Do not interrupt detector communication during the calibration process.

---

### Step 5

Verify Offset template generation succeeds.

---

# 7. Important Notes

The iDetector User Manual specifically states:

Before generating an Offset Template, the SDK checks whether an exposure has recently occurred.

If a previous exposure is detected, the SDK waits for a period of time before starting Offset generation to prevent residual image (ghost) information from being incorporated into the Offset Template. :contentReference[oaicite:3]{index=3}

Engineering recommendation:

- Do not perform Offset Calibration immediately after X-ray exposure.
- Allow sufficient detector recovery time.
- Do not interrupt communication during template generation.

---

# 8. Expected Result

After successful calibration:

- Offset Template is generated.
- Detector background signal is compensated.
- Gain Calibration can be performed.
- Detector is ready for subsequent calibration procedures.

---

# 9. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Offset generation failed | Detector communication abnormal |
| Calibration cannot start | Detector not Ready |
| Calibration timeout | Communication interrupted |
| Offset template invalid | Detector not stabilized |
| Ghost artifact after calibration | Offset generated too soon after exposure |

---

# 10. Engineering Recommendations

Before Offset Calibration:

- Ensure detector communication is stable.
- Confirm no exposure is in progress.
- Verify detector temperature is stable.
- Avoid moving the detector.

After Offset Calibration:

- Verify template generation succeeds.
- Continue with Gain Calibration.
- Archive calibration records if required.

---

# 11. Related Documents

## Calibrate Module

- README.md
- GainCalibration.md
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
| v1.0 | 2026-08-07 | Initial Offset Calibration documentation based on iDetector User Manual |