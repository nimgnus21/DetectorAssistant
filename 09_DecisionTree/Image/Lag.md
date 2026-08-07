# Image Lag Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v3.0
>
> Last Updated: 2026-08-06

---

# Symptom

The detector exhibits image lag during continuous image acquisition.

Typical symptoms include:

- Previous image appears in the next frame
- Residual signal during dynamic imaging
- Delayed image refresh
- Increasing lag during continuous exposure
- Motion artifact caused by image persistence

---

# Symptom Classification

Identify the observed behavior.

□ Single-frame lag

□ Multi-frame lag

□ Continuous lag

□ Dynamic imaging only

□ High-dose only

□ Low-dose only

□ Every acquisition

□ Intermittent

---

# Affected Pipeline

Possible acquisition pipeline:

```
X-ray Exposure
      │
      ▼
Detector Pixel
      │
      ▼
TFT Switching
      │
      ▼
Charge Readout
      │
      ▼
ADC
      │
      ▼
FPGA Buffer
      │
      ▼
SDK
      │
      ▼
Display
```

Verification Status

```
Exposure            □

Detector Pixel      □

TFT                 □

Readout             □

ADC                 □

FPGA                □

SDK                 □
```

---

# Diagnostic Flow

```
                  Image Lag
                      │
          Continuous Acquisition?
                      │
          ┌───────────┴───────────┐
          │                       │
         NO                      YES
          │                       │
   Check Ghost Artifact     Continue
                                   │
                                   ▼
          SDK Demo Reproduces?
                                   │
                ┌──────────────────┴──────────────────┐
                │                                     │
               NO                                    YES
                │                                     │
      Customer Application                  Continue
                                             │
                                             ▼
      Offset / Gain Calibration Correct?
                                             │
                ┌──────────────────┴──────────────────┐
                │                                     │
               NO                                    YES
                │                                     │
        Recalibrate Detector                Continue
                                             │
                                             ▼
          Exposure Parameters Correct?
                                             │
                ┌──────────────────┴──────────────────┐
                │                                     │
               NO                                    YES
                │                                     │
        Adjust Exposure                     Continue
                                             │
                                             ▼
        Lag Persists After Recalibration?
                                             │
                ┌──────────────────┴──────────────────┐
                │                                     │
               NO                                    YES
                │                                     │
        Calibration Issue                 Hardware Investigation
```

---

# Diagnosis Hint

Image lag is usually related to incomplete charge release between consecutive exposures.

Common causes include:

- Pixel charge retention
- TFT switching abnormality
- High exposure dose
- Detector recovery time too short
- Continuous acquisition timing

Unlike Ghost artifacts, image lag is strongly dependent on acquisition sequence and timing.

---

# Hardware Hint

Possible related hardware

★★★★★ Pixel Cell

★★★★★ TFT Switch

★★★★☆ Readout Circuit

★★★★☆ FPGA Timing

★★★☆☆ ADC

---

# Expected Result

### Continuous Acquisition

Expected Result

- Consecutive images are independent.
- No residual image from previous frame.

---

### Exposure Test

Expected Result

- Lag decreases after increasing frame interval.

---

### Calibration

Expected Result

- Offset and Gain calibration complete successfully.
- No change in lag characteristics after recalibration indicates a possible hardware issue.

---

### SDK Demo

Expected Result

- Same lag behavior is reproducible.

---

# Quick Checklist

Verify:

- □ Continuous acquisition mode
- □ Exposure interval
- □ Offset calibration
- □ Gain calibration
- □ Firmware version
- □ SDK version
- □ Detector temperature
- □ SDK Demo

---

# Required Evidence

Collect before escalation:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Exposure Parameters
- Frame Rate
- RAW Image Sequence
- SDK Log
- Detector Status Screenshot

---

# Possible Root Causes

## Detector

- Pixel charge retention
- TFT switching abnormality

---

## Exposure

- High exposure dose
- Frame interval too short

---

## Readout

- Readout timing abnormal
- Charge discharge incomplete

---

## Software

- Continuous acquisition configuration
- SDK timing configuration

---

# Recommended Actions

Priority 1

- Verify exposure interval.
- Verify continuous acquisition settings.

Priority 2

- Perform Offset and Gain recalibration.

Priority 3

- Compare with SDK Demo.
- Compare with another detector.

Priority 4

- Escalate for detector hardware analysis.

---

# Escalation Criteria

Escalate when:

- Lag is reproducible under controlled conditions.
- Lag remains after recalibration.
- SDK Demo reproduces the issue.
- Another detector does not exhibit the same behavior.
- Pixel or TFT hardware failure is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/ImageWorkflow.md

## Case

- 11_Case/Image/Lag.md

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
| v3.0 | 2026-08-06 | Initial release |