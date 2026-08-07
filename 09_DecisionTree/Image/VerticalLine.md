# Vertical Line Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v1.0
>
> Last Updated: 2026-08-06

---

# Symptom

Vertical line artifacts appear in the acquired image.

Typical symptoms include:

- One vertical line
- Multiple vertical lines
- Bright vertical line
- Dark vertical line
- Intermittent vertical line
- Vertical stripe across the entire image

---

# Symptom Classification

Before troubleshooting, identify the defect pattern.

□ Single bright line

□ Single dark line

□ Multiple lines

□ Fixed-position line

□ Intermittent line

□ Line appears only after exposure

□ Line appears in every image

---

# Diagnostic Flow

```
                Vertical Line
                      │
         Present in Every Image?
                      │
          ┌───────────┴───────────┐
          │                       │
         NO                      YES
          │                       │
 Check Exposure             Continue
                                  │
                                  ▼
         SDK Demo Also Shows Line?
                                  │
                   ┌──────────────┴──────────────┐
                   │                             │
                  NO                            YES
                   │                             │
         Customer Software              Continue
                                  │
                                  ▼
        Offset Calibration Passed?
                                  │
                   ┌──────────────┴──────────────┐
                   │                             │
                  NO                            YES
                   │                             │
         Rebuild Offset                 Continue
                                  │
                                  ▼
         Gain Calibration Passed?
                                  │
                   ┌──────────────┴──────────────┐
                   │                             │
                  NO                            YES
                   │                             │
         Rebuild Gain                  Continue
                                  │
                                  ▼
      Position Changes After Calibration?
                                  │
                   ┌──────────────┴──────────────┐
                   │                             │
                  YES                           NO
                   │                             │
        Calibration Issue              Continue
                                  │
                                  ▼
       Compare Another Detector
                                  │
                   ┌──────────────┴──────────────┐
                   │                             │
            Problem Gone                 Still Present
                   │                             │
        Environment Related          Continue
                                  │
                                  ▼
          Suspect Hardware?
                                  │
         ┌──────────┬──────────┬──────────┐
         │          │          │
       TFT      Gate Driver   Readout
```

---

# Quick Checklist

Verify:

- □ Offset calibration
- □ Gain calibration
- □ Firmware version
- □ SDK version
- □ Exposure settings
- □ Detector temperature
- □ Same position in every image
- □ SDK Demo verification

---

# Required Evidence

Collect before escalation:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Original Image (RAW)
- Window/Level Image
- Offset File
- Gain File
- Calibration Log
- Detector Status Screenshot

---

# Possible Root Causes

## Calibration

- Offset abnormal

- Gain abnormal

---

## TFT

- TFT switching failure

- TFT leakage

---

## Gate Driver

- Gate output abnormal

- Missing gate pulse

---

## Readout Circuit

- Column readout abnormal

- Analog signal interruption

---

## ADC

- ADC channel abnormal

---

## FPGA

- Data acquisition abnormal

---

# Recommended Actions

Priority 1

- Verify Offset.

- Verify Gain.

Priority 2

- Compare RAW images.

- Compare with another detector.

Priority 3

- Check line position consistency.

Priority 4

- Escalate to hardware investigation.

---

# Escalation Criteria

Escalate when:

- Line remains after recalibration.

- Same line appears in SDK Demo.

- Line position is fixed.

- Another detector works normally.

- Hardware defect is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/ImageWorkflow.md

## Case

- 11_Case/Image/VerticalLine.md

## Failure Knowledge

- 07_FailureKnowledge/TFT/

- 07_FailureKnowledge/GateDriver/

- 07_FailureKnowledge/Readout/

## Reference

- 15_Reference/ImageReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-06 | Initial release |