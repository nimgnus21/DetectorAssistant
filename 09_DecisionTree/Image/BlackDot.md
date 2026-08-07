# Black Dots Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v2.0
>
> Last Updated: 2026-08-06

---

# Symptom

Black dot artifacts appear in one or more acquired images.

Typical symptoms include:

- Single black pixel
- Multiple black pixels
- Fixed-position black dots
- Clustered black dots
- Black dots visible in every image
- Black dots remain after calibration

---

# Symptom Classification

Identify the observed defect pattern.

□ Single Pixel

□ Multiple Pixels

□ Pixel Cluster

□ Fixed Position

□ Random Position

□ Appears in Every Image

□ Appears Occasionally

---

# Diagnostic Flow

```
                    Black Dots
                        │
          Present in Every Image?
                        │
              YES                NO
               │                  │
         Continue          Check Exposure
               │
               ▼
      SDK Demo Also Shows Defect?
               │
        YES             NO
         │               │
 Continue          Customer Software
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
 Position Changes?
  │
YES         NO
 │           │
Calibration   Hardware Analysis
Issue
```

---

# Diagnosis Hint

Black dots generally indicate pixels that continuously output a low or zero signal.

If the defect:

- remains at exactly the same coordinates,
- appears in RAW images,
- persists after Offset and Gain recalibration,

the probability of a detector hardware defect is high.

If the defect position changes between images, calibration or exposure conditions should be investigated first.

---

# Hardware Hint

Possible affected modules

★★★★★ Pixel Cell

★★★★★ TFT Pixel Switch

★★★★☆ Storage Capacitor

★★★☆☆ Readout Circuit

★★☆☆☆ ADC Channel

---

# Quick Checklist

□ Verify Offset Calibration

□ Verify Gain Calibration

□ Compare RAW Image

□ Compare Another Detector

□ Verify Detector Temperature

□ Verify Firmware Version

□ Verify SDK Version

□ Confirm Fixed Position

---

# Required Evidence

Collect:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- RAW Image
- Processed Image
- Offset File
- Gain File
- Detector Status
- Calibration Log

---

# Possible Root Causes

## Pixel Defect

- Dead Pixel

- Pixel Leakage

- Pixel Short

---

## TFT

- TFT Switching Failure

- TFT Leakage

---

## Calibration

- Offset abnormal

- Gain abnormal

---

## Readout

- Pixel Readout Failure

- ADC Sampling Error

---

# Recommended Actions

Priority 1

Verify Offset and Gain calibration.

Priority 2

Compare RAW and processed images.

Priority 3

Verify whether the defect remains at the same coordinates.

Priority 4

Compare with another detector.

Priority 5

Escalate if hardware defect is suspected.

---

# Escalation Criteria

Escalate when:

- Defect remains after complete recalibration.
- Defect appears in RAW images.
- Pixel position never changes.
- Another detector operates normally under identical conditions.
- Pixel hardware failure is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/ImageWorkflow.md

## Case

- 11_Case/Image/BlackDots.md

## Failure Knowledge

- 07_FailureKnowledge/TFT/
- 07_FailureKnowledge/Pixel/
- 07_FailureKnowledge/Readout/

## Reference

- 15_Reference/ImageReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v2.0 | 2026-08-06 | Initial release |