# Ghost Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v3.1
>
> Last Updated: 2026-08-06

---

# Symptom

Ghost artifacts remain visible in acquired images.

Typical symptoms include:

- Residual image after exposure
- Double image
- Previous object outline remains visible
- Shadow artifact
- Image persistence
- Localized residual image

---

# Symptom Classification

Identify the observed behavior.

□ Single Ghost

□ Multiple Ghosts

□ Local Ghost

□ Full Image Ghost

□ Fixed Position

□ Exposure Related

□ Appears Occasionally

□ Appears Every Image

---

# Comparison

Differentiate Ghost from Image Lag before troubleshooting.

| Item | Ghost Artifact | Image Lag |
|------|----------------|-----------|
| Appears in a single image | ✔ Yes | ✘ Usually No |
| Related to previous frame | Possible | ✔ Strongly |
| Continuous acquisition required | Usually No | ✔ Yes |
| Depends on frame interval | Low | High |
| Caused by calibration | Possible | Rare |
| Caused by charge retention | Possible | ✔ Primary Cause |
| Typical appearance | Residual shadow | Previous frame persistence |

---

# Affected Pipeline

Possible acquisition pipeline

```
Exposure
    │
    ▼
Detector Pixel
    │
    ▼
TFT
    │
    ▼
Readout
    │
    ▼
ADC
    │
    ▼
FPGA
    │
    ▼
Image Processing
    │
    ▼
Display
```

Verification Status

```
Exposure            □

Pixel               □

TFT                 □

Readout             □

ADC                 □

FPGA                □

Image Processing    □

SDK                 □
```

---

# Diagnostic Flow

```
                    Ghost Artifact
                          │
             Reproducible Every Exposure?
                          │
              ┌───────────┴───────────┐
              │                       │
             NO                      YES
              │                       │
     Check Exposure           Continue
                                      │
                                      ▼
                SDK Demo Reproduces?
                                      │
                   ┌──────────────────┴──────────────────┐
                   │                                     │
                  NO                                    YES
                   │                                     │
          Customer Application                 Continue
                                                │
                                                ▼
           Offset Calibration Completed?
                                                │
                   ┌──────────────────┴──────────────────┐
                   │                                     │
                  NO                                    YES
                   │                                     │
          Regenerate Offset                   Continue
                                                │
                                                ▼
            Gain Calibration Completed?
                                                │
                   ┌──────────────────┴──────────────────┐
                   │                                     │
                  NO                                    YES
                   │                                     │
          Regenerate Gain                    Continue
                                                │
                                                ▼
          Ghost Correction Executed?
                                                │
                   ┌──────────────────┴──────────────────┐
                   │                                     │
                  NO                                    YES
                   │                                     │
      Execute Ghost Correction               Continue
                                                │
                                                ▼
           Ghost Still Present?
                                                │
                   ┌──────────────────┴──────────────────┐
                   │                                     │
                  NO                                    YES
                   │                                     │
            Calibration Issue             Hardware Investigation
```

---

# Diagnosis Hint

Ghost artifacts are usually caused by incomplete removal of residual image information.

Typical investigation order:

1. Offset Calibration

2. Gain Calibration

3. Ghost Correction

4. Exposure Conditions

5. Pixel / TFT

6. Image Processing

If Ghost disappears after Ghost Correction, calibration is the most likely cause.

If Ghost remains unchanged after complete recalibration, hardware investigation should begin.

---

# Hardware Hint

Possible affected hardware

★★★★★ Pixel Cell

★★★★★ TFT

★★★★☆ Readout Circuit

★★★★☆ FPGA

★★★☆☆ ADC

★★☆☆☆ SDK Processing

---

# Expected Result

### Offset

Expected Result

- Offset completed successfully.
- Detector Ready.

---

### Gain

Expected Result

- Gain completed successfully.
- Image quality improved.

---

### Ghost Correction

Expected Result

- Ghost artifact significantly reduced or removed.

---

### SDK Demo

Expected Result

- Ghost reproduced.

If SDK Demo is normal:

→ Investigate customer application.

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| SDK Demo | Verify detector output | Same ghost reproduced |
| Calibration Tool | Execute Ghost Correction | Ghost reduced |
| RAW Image Viewer | Compare RAW image | Determine if ghost exists before processing |
| Detector Log | Verify detector status | No internal errors |

---

# Quick Checklist

Verify

□ Offset Calibration

□ Gain Calibration

□ Ghost Correction

□ Exposure Parameters

□ Firmware Version

□ SDK Version

□ RAW Image

□ SDK Demo

□ Detector Status

---

# Required Evidence

Collect before escalation

- Detector Model

- Detector SN

- Firmware Version

- SDK Version

- Exposure Parameters

- RAW Image

- Processed Image

- Ghost Correction Log

- SDK Log

- Detector Status Screenshot

---

# Possible Root Causes

## Calibration

- Offset abnormal

- Gain abnormal

- Ghost correction incomplete

---

## Detector

- Pixel charge retention

- TFT leakage

---

## Exposure

- High exposure dose

- Incorrect calibration exposure

---

## Software

- Image processing abnormal

- SDK rendering issue

---

# Recommended Actions

Priority 1

- Execute complete calibration.

Priority 2

- Perform Ghost Correction.

Priority 3

- Compare RAW and processed images.

Priority 4

- Verify with SDK Demo.

Priority 5

- Escalate if detector hardware is suspected.

---

# Escalation Criteria

Escalate when:

- Ghost remains after complete recalibration.

- SDK Demo reproduces the issue.

- RAW image contains the same artifact.

- Another detector works normally.

- Pixel or TFT hardware failure is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/CalibrationWorkflow.md

- 06_Workflow/ImageWorkflow.md

## Case

- 11_Case/Image/Ghost.md

- 11_Case/Calibration/GhostCorrection.md

## Failure Knowledge

- 07_FailureKnowledge/TFT/

- 07_FailureKnowledge/Pixel/

- 07_FailureKnowledge/Calibration/

## Reference

- 15_Reference/ImageReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v3.1 | 2026-08-06 | Initial release |