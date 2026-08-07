# Calibration Status

> iDetector Calibrate Module - Calibration Status

---

# 1. Purpose

The **Calibration Status** page is used to verify the current calibration status of the detector.

It allows engineers to determine whether all required calibration templates have been generated successfully before image acquisition.

Calibration Status is also used to verify detector readiness after firmware upgrade, parameter recovery, detector replacement, and factory calibration.

---

# 2. Scope

This document describes the calibration status verification functions in the iDetector Calibrate module.

The status includes:

- Offset Template
- Gain Template
- Defect Template
- Ghost Template
- Calibration Configuration
- Calibration Version
- Detector Calibration State

---

# 3. Calibration Dependency

Detector calibration follows the dependency below.

```text
Offset

↓

Gain

↓

Defect

↓

Ghost (Optional)
```

If one template is invalid, all dependent templates should be regenerated.

---

# 4. Calibration Status Items

## Offset Template

Purpose

Compensates detector dark current.

Status

- Generated
- Missing
- Invalid

---

## Gain Template

Purpose

Compensates detector pixel response differences.

Status

- Generated
- Missing
- Invalid

---

## Defect Template

Purpose

Compensates defective pixels.

Status

- Generated
- Missing
- Invalid

---

## Ghost Template

Purpose

Compensates long-term image persistence caused by amorphous silicon defects.

Status

- Enabled
- Disabled
- Missing

Ghost Calibration is optional and only required when Ghost correction is enabled.

---

# 5. Engineering Verification

Before detector delivery:

Verify

✓ Offset Template

✓ Gain Template

✓ Defect Template

Ghost Template (If Required)

---

Before customer installation:

Verify

- Detector Communication
- Calibration Templates
- Detector Firmware
- Detector Parameters

---

After firmware upgrade:

Verify

- Calibration templates still exist.
- Detector parameters remain valid.
- Image quality is normal.

---

After detector replacement:

Verify

- Detector SN
- Calibration template matching
- Detector configuration
- Image acquisition

---

# 6. Typical Workflow

```text
Connect Detector

↓

Open Calibrate

↓

Check Calibration Status

↓

Verify Offset

↓

Verify Gain

↓

Verify Defect

↓

Verify Ghost

↓

Detector Ready
```

---

# 7. Engineering Recommendations

Always verify calibration status:

- Before shipment
- Before customer acceptance
- After firmware upgrade
- After parameter recovery
- After detector replacement
- Before investigating image quality issues

Never copy calibration templates between different detectors unless specifically approved by R&D.

---

# 8. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Offset missing | Offset Calibration not completed |
| Gain missing | Gain Calibration failed |
| Defect missing | Defect Calibration failed |
| Ghost unavailable | Ghost not enabled or template missing |
| Image abnormal after calibration | Template mismatch |
| Calibration status inconsistent | Incorrect detector configuration |

---

# 9. Related Documents

## Calibrate Module

- README.md
- OffsetCalibration.md
- GainCalibration.md
- DefectCalibration.md
- GhostCalibration.md
- CalibrationLog.md
- FAQ.md

## Knowledge Base

- ../../05_Calibration
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Calibration Status documentation |