# Ghost Calibration

> iDetector Calibrate Module - Ghost Calibration

---

# 1. Purpose

Ghost Calibration is used to compensate for long-term residual signals (Ghost) caused by amorphous silicon defects inside the detector.

Unlike Lag, Ghost cannot disappear within a short period of time and requires a dedicated Ghost Calibration template.

Ghost Calibration generates a Ghost Template that is used during image correction to reduce long-term image persistence.

---

# 2. Scope

This document describes the Ghost Calibration function provided by iDetector.

It includes:

- Ghost calibration configuration
- Calibration workflow
- Ghost template generation
- Engineering recommendations
- Common issues

---

# 3. Ghost vs Lag

## Lag

Lag is caused by:

- TFT turn-on time not long enough
- Characteristics of the amorphous silicon response curve

Lag usually decreases rapidly over time.

---

## Ghost

Ghost is caused by:

- Defects in the amorphous silicon layer

Ghost remains for a much longer period and requires Ghost Calibration for compensation.

---

# 4. Prerequisites

Before Ghost Calibration:

The following calibration templates **must already exist**.

- Offset Template
- Gain Template
- Defect Template

Ghost Calibration **cannot** be performed before these templates are generated.

---

# 5. Enable Ghost Calibration

Before Ghost Calibration:

Open the configuration file:

```text
CaliImpl.ini
```

Modify:

```ini
Cfg_EnableGhost=1
```

Restart iDetector if required.

---

# 6. Ghost Calibration Method 1

## Configuration

| Parameter | Value |
|-----------|-------|
| TriggerMode | Prep |
| PrepCapMode | Acq2 |
| SelfCapEnable | On |
| Self Cap Span Time | 100 |
| SelfClearEnable | Off |
| Delay Time | 1000 |
| Integrate Time | 70 |

After configuration:

Click

**Write**

to download the parameters to the detector.

---

## Required Calibration Templates

Method 1 requires:

- PreOffset Template
- Gain Template
- Defect Template

---

## Workflow

```text
Generate Offset

↓

Generate Gain

↓

Generate Defect

↓

Modify CaliImpl.ini

↓

Cfg_EnableGhost=1

↓

Configure Method 1 Parameters

↓

Write

↓

Generate Ghost Template
```

---

# 7. Ghost Calibration Method 2

## Configuration

| Parameter | Value |
|-----------|-------|
| TriggerMode | Prep |
| PrepCapMode | ClearAcq |
| SelfCapEnable | Off |
| SelfClearEnable | On |
| Delay Time | 2000 |
| Integrate Time | 125 |
| Self Clear Span Time | 1000 |

After configuration:

Click

**Write**

to download the parameters.

---

## Required Calibration Templates

Method 2 requires:

- PostOffset Template
- Gain Template
- Defect Template

---

## Workflow

```text
Generate PostOffset

↓

Generate Gain

↓

Generate Defect

↓

Modify CaliImpl.ini

↓

Cfg_EnableGhost=1

↓

Configure Method 2 Parameters

↓

Write

↓

Generate Ghost Template
```

---

# 8. Engineering Recommendations

Before Ghost Calibration:

- Complete Offset Calibration.
- Complete Gain Calibration.
- Complete Defect Calibration.
- Verify detector communication.
- Verify detector status is Ready.

During Ghost Calibration:

- Do not interrupt detector communication.
- Do not modify detector parameters.
- Do not disconnect the detector.
- Keep detector temperature stable.

---

# 9. Verification

After Ghost Calibration:

Verify:

- Ghost Template generated successfully.
- Ghost Correction can be enabled.
- Ghost artifact is reduced.
- Detector image quality is improved.

---

# 10. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Ghost template generation failed | Offset/Gain/Defect template missing |
| Ghost Calibration unavailable | Cfg_EnableGhost not enabled |
| Ghost artifact unchanged | Incorrect calibration method selected |
| Write failed | Detector communication abnormal |
| Calibration interrupted | Detector disconnected |

---

# 11. Related Documents

## Calibrate Module

- README.md
- OffsetCalibration.md
- GainCalibration.md
- DefectCalibration.md
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
| v1.0 | 2026-08-07 | Initial Ghost Calibration documentation |