# Horizontal Line Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v2.0
>
> Last Updated: 2026-08-06

---

# Symptom

Horizontal line artifacts appear in the acquired image.

Typical symptoms include:

- Single horizontal line
- Multiple horizontal lines
- Bright horizontal line
- Dark horizontal line
- Fixed-position horizontal line
- Intermittent horizontal line

---

# Symptom Classification

Identify the observed pattern.

□ Single Line

□ Multiple Lines

□ Bright Line

□ Dark Line

□ Fixed Position

□ Random Position

□ Appears Every Image

□ Appears Occasionally

---

# Diagnostic Flow

```
             Horizontal Line
                    │
      Appears in Every Image?
                    │
           YES             NO
            │               │
      Continue        Check Exposure
            │
            ▼
     SDK Demo Reproduces?
            │
      YES          NO
       │            │
Continue      Customer Software
       │
       ▼
Offset Calibration Normal?
       │
 YES         NO
  │           │
Continue   Rebuild Offset
  │
  ▼
Gain Calibration Normal?
  │
YES         NO
 │           │
Continue   Rebuild Gain
 │
 ▼
Fixed Position?
 │
YES         NO
 │           │
Continue   Timing Issue
 │
 ▼
Hardware Analysis
```

---

# Diagnosis Hint

Why suspect hardware?

A horizontal line generally indicates that one detector row is abnormal.

Possible affected modules include:

- Gate Driver
- Row Timing
- TFT Gate Control
- Readout Timing
- FPGA Timing Logic

If the line position is fixed across repeated acquisitions and remains after recalibration, hardware investigation should be prioritized.

---

# Hardware Hint

Possible related hardware:

★★★★★ Gate Driver

★★★★☆ TFT Gate

★★★★☆ Timing Controller

★★★☆☆ FPGA

★★☆☆☆ Readout Circuit

---

# Quick Checklist

□ Offset regenerated

□ Gain regenerated

□ Firmware verified

□ SDK verified

□ Same position confirmed

□ SDK Demo verified

□ RAW image collected

---

# Required Evidence

Collect:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- RAW Image
- Window Image
- Offset File
- Gain File
- Calibration Log
- Detector Status

---

# Possible Root Causes

## Calibration

- Offset abnormal

- Gain abnormal

---

## Hardware

- Gate Driver failure

- TFT Gate failure

- Timing Controller abnormal

- FPGA timing error

---

## Software

- SDK display issue

- Image rendering issue

---

# Recommended Actions

Priority 1

Verify calibration.

Priority 2

Compare RAW image.

Priority 3

Compare another detector.

Priority 4

Escalate to hardware investigation.

---

# Escalation Criteria

Escalate when:

- Fixed-position line remains after calibration.
- SDK Demo reproduces the issue.
- RAW image contains the same artifact.
- Comparison detector is normal.
- Hardware fault is suspected.

---

# Related Documents

Workflow

Case

FailureKnowledge

Reference

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v2.0 | 2026-08-06 | Added Diagnosis Hint and Hardware Hint |