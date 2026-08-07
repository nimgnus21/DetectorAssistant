# Noise Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v1.0
>
> Last Updated: 2026-08-06

---

# Symptom

The acquired image exhibits abnormal noise that affects diagnostic image quality.

Typical symptoms include:

- Grainy image
- Random bright or dark pixels
- Increased background noise
- Low Signal-to-Noise Ratio (SNR)
- Noise level higher than normal
- Noise appears across the entire image

---

# Diagnostic Flow

```
                     Image Noise
                          │
                 Noise on Every Image?
                          │
             ┌────────────┴────────────┐
             │                         │
            NO                        YES
             │                         │
      Check Exposure             Continue
                                     │
                                     ▼
                Exposure Parameters Correct?
                                     │
                  ┌──────────────────┴──────────────────┐
                  │                                     │
                 NO                                    YES
                  │                                     │
          Correct Exposure                     Continue
                                     │
                                     ▼
               Offset Calibration Passed?
                                     │
                  ┌──────────────────┴──────────────────┐
                  │                                     │
                 NO                                    YES
                  │                                     │
        Rebuild Offset                     Continue
                                     │
                                     ▼
                Gain Calibration Passed?
                                     │
                  ┌──────────────────┴──────────────────┐
                  │                                     │
                 NO                                    YES
                  │                                     │
          Rebuild Gain                      Continue
                                     │
                                     ▼
             Compare with Another Detector
                                     │
                  ┌──────────────────┴──────────────────┐
                  │                                     │
             Noise Disappears                  Noise Remains
                  │                                     │
        Environment Related              Continue
                                                     │
                                                     ▼
                 Same Noise with SDK Demo?
                                                     │
                                   ┌─────────────────┴─────────────────┐
                                   │                                   │
                                  NO                                  YES
                                   │                                   │
                        Customer Software                  Continue
                                                     │
                                                     ▼
                  Hardware Defect Suspected?
                                                     │
                                   ┌─────────────────┴─────────────────┐
                                   │                                   │
                                  YES                                 NO
                                   │                                   │
                       Go to Defect Failure           Continue Investigation
```

---

# Quick Checklist

Verify:

- □ Exposure parameters
- □ Detector temperature
- □ Offset calibration
- □ Gain calibration
- □ Firmware version
- □ SDK version
- □ Generator stability
- □ Image acquired with SDK Demo

---

# Required Evidence

Collect before escalation:

- Detector Model

- Detector SN

- Firmware Version

- SDK Version

- Original Image

- Offset File

- Gain File

- Exposure Parameters

- SDK Log

- Detector Status Screenshot

---

# Possible Root Causes

## Exposure

- Low exposure dose
- Incorrect exposure settings
- Generator instability

---

## Calibration

- Offset calibration abnormal
- Gain calibration abnormal

---

## Detector

- Excessive detector noise
- Readout circuit abnormality
- ADC abnormality

---

## Software

- Image processing settings
- SDK configuration

---

## Environment

- Electromagnetic interference
- Power instability
- Temperature variation

---

# Recommended Actions

Priority 1

- Verify exposure conditions.
- Compare with previous images.

Priority 2

- Regenerate Offset.
- Regenerate Gain.

Priority 3

- Test using the official SDK Demo.
- Compare with another detector.

Priority 4

- Escalate if detector hardware is suspected.

---

# Escalation Criteria

Escalate when:

- Noise persists after complete recalibration.
- Noise appears with the official SDK Demo.
- Multiple calibrated images show the same abnormality.
- Comparison testing confirms detector-specific behavior.
- Hardware failure is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/ImageWorkflow.md

## Case

- 11_Case/Image/Noise.md

## Tools

- 17_Tools/ImageTools.md

## Reference

- 15_Reference/ImageReference.md

## Failure Knowledge

- 07_FailureKnowledge/Image/
- 07_FailureKnowledge/Readout/

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-06 | Initial release |