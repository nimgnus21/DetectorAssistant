# White Dots Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v2.0
>
> Last Updated: 2026-08-06

---

# Symptom

White dot artifacts appear in acquired images.

Typical symptoms include:

- Single white pixel
- Multiple white pixels
- Bright pixel cluster
- Fixed-position white dots
- White dots visible in every image
- White dots remain after recalibration

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
                    White Dots
                         │
          Present in Every Image?
                         │
              YES                NO
               │                  │
         Continue          Check Exposure
               │
               ▼
       SDK Demo Shows Defect?
               │
        YES             NO
         │               │
 Continue          Customer Software
         │
         ▼
 Offset Calibration Passed?
         │
    YES         NO
     │           │
Continue   Rebuild Offset
     │
     ▼
 Gain Calibration Passed?
     │
 YES         NO
  │           │
Continue   Rebuild Gain
  │
  ▼
 Position Fixed?
  │
YES         NO
 │           │
Hardware     Calibration /
Analysis     Exposure
 │
 ▼
Pixel Saturation?
 │
YES         NO
 │           │
Suspect Pixel     Continue Investigation
or ADC
```

---

# Diagnosis Hint

White dots usually indicate abnormal high pixel output.

If the defect:

- appears at the same coordinates,
- exists in RAW images,
- remains after Offset and Gain calibration,

hardware failure is likely.

If white dots only appear under high exposure conditions, verify exposure parameters and detector saturation behavior.

---

# Hardware Hint

Possible affected hardware

★★★★★ Pixel Cell

★★★★★ ADC Channel

★★★★☆ Gain Circuit

★★★★☆ TFT Leakage

★★★☆☆ Readout Circuit

---

# Quick Checklist

□ Verify Offset Calibration

□ Verify Gain Calibration

□ Compare RAW Image

□ Compare Another Detector

□ Verify Exposure Parameters

□ Verify Detector Temperature

□ Verify Firmware Version

□ Verify SDK Version

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
- Exposure Parameters
- Calibration Log

---

# Possible Root Causes

## Pixel

- Hot Pixel

- Pixel Saturation

- Pixel Leakage

---

## ADC

- ADC Saturation

- ADC Channel Failure

---

## Gain

- Gain Correction Error

- Gain Overflow

---

## Readout

- Readout Noise

- Sampling Error

---

# Recommended Actions

Priority 1

- Verify Offset calibration.
- Verify Gain calibration.

Priority 2

- Compare RAW and processed images.

Priority 3

- Verify exposure settings.

Priority 4

- Compare another detector.

Priority 5

- Escalate if hardware defect is suspected.

---

# Escalation Criteria

Escalate when:

- White dots remain after recalibration.
- RAW image contains the same defect.
- Pixel position is fixed.
- Exposure settings have been verified.
- Hardware failure is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/ImageWorkflow.md

## Case

- 11_Case/Image/WhiteDots.md

## Failure Knowledge

- 07_FailureKnowledge/Pixel/
- 07_FailureKnowledge/ADC/
- 07_FailureKnowledge/Gain/

## Reference

- 15_Reference/ImageReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v2.0 | 2026-08-06 | Initial release |