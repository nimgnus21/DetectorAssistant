# FAQ

> Frequently Asked Questions — Calibrate Module

---

# 1. Purpose

This document summarizes the most frequently encountered questions related to the **Calibrate** module of iDetector.

It provides Field Application Engineers (FAEs), Technical Support Engineers, and Service Engineers with quick troubleshooting guidance for detector calibration, template generation, and calibration verification.

Detailed troubleshooting procedures are available in the corresponding **Failure Knowledge**, **Decision Tree**, **SOP**, and **Case** modules.

---

# 2. Frequently Asked Questions

---

## Q1. Why can't Offset Calibration start?

### Possible Causes

- Detector not connected
- Detector status is not Ready
- Detector communication abnormal
- Detector initialization failed

### Recommended Actions

- Verify detector communication.
- Confirm detector status is Ready.
- Restart detector if necessary.
- Retry Offset Calibration.

---

## Q2. Why does Offset Calibration fail?

### Possible Causes

- Detector communication interrupted
- Detector unstable
- Previous acquisition not completed

### Recommended Actions

- Wait until detector becomes stable.
- Verify communication.
- Retry calibration.
- Check calibration log.

---

## Q3. Why can't Gain Calibration start?

### Possible Causes

- Offset Template missing
- Detector not Ready
- X-ray generator unavailable
- Exposure parameters incorrect

### Recommended Actions

- Verify Offset Calibration completed.
- Verify generator status.
- Verify exposure parameters.
- Repeat Gain Calibration.

---

## Q4. Why is Gain Calibration unsuccessful?

### Possible Causes

- Exposure field not uniform
- Detector moved during calibration
- Exposure output unstable

### Recommended Actions

- Remove all objects from the beam.
- Maintain detector position.
- Verify generator stability.
- Repeat calibration.

---

## Q5. Why are bad pixels still visible after Defect Calibration?

### Possible Causes

- Defect Template not generated
- Defect Correction disabled
- Detector requires recalibration

### Recommended Actions

- Verify Defect Template.
- Enable Defect Correction.
- Repeat Defect Calibration if required.

---

## Q6. Why can't Ghost Calibration be started?

### Possible Causes

- Ghost function not enabled
- Required templates missing
- Configuration incomplete

### Recommended Actions

- Set:

```ini
Cfg_EnableGhost=1
```

- Restart software if required.
- Verify Offset, Gain, and Defect templates exist.
- Follow the correct Ghost Calibration procedure.

---

## Q7. Which templates are required before Ghost Calibration?

Required templates:

- Offset Template
- Gain Template
- Defect Template

For engineering practice:

- Method 1 requires **PreOffset**.
- Method 2 requires **PostOffset**.

---

## Q8. Why is Ghost still visible after Ghost Calibration?

### Possible Causes

- Incorrect calibration method selected
- Wrong detector configuration
- Ghost Template not generated successfully

### Recommended Actions

- Verify calibration method.
- Confirm Ghost Template generation.
- Repeat Ghost Calibration.

---

## Q9. Should templates be copied from another detector?

### Answer

No.

Calibration templates are detector-specific.

Templates generated for one detector should not be copied to another detector unless explicitly approved by R&D.

---

## Q10. When should all templates be regenerated?

Recommended situations include:

- Detector replacement
- Firmware requiring recalibration
- Template corruption
- Persistent image quality abnormalities
- R&D recommendation

Typical regeneration order:

```text
Offset

↓

Gain

↓

Defect

↓

Ghost (Optional)
```

---

# 3. Engineering Best Practices

Before calibration:

- Verify detector communication.
- Verify detector status.
- Verify detector temperature.
- Verify generator stability.

During calibration:

- Do not disconnect the detector.
- Do not modify parameters.
- Monitor calibration progress.

After calibration:

- Verify all templates.
- Acquire verification images.
- Save calibration logs.
- Archive calibration records.

---

# 4. Escalation Checklist

Before reporting calibration issues to R&D, prepare:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Calibration Log
- Error Message
- Test Images
- Offset / Gain / Defect / Ghost Template Status

---

# 5. Related Documents

## Calibrate Module

- README.md
- OffsetCalibration.md
- GainCalibration.md
- DefectCalibration.md
- GhostCalibration.md
- CalibrationStatus.md
- CalibrationLog.md

## Knowledge Base

- ../../05_Calibration
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
| v1.0 | 2026-08-07 | Initial Calibrate FAQ documentation |