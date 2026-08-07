# Image Shift Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v3.0
>
> Last Updated: 2026-08-06

---

# Symptom

The acquired image is shifted from its expected position.

Typical symptoms include:

- Horizontal image shift
- Vertical image shift
- Partial image displacement
- Cropped image
- Image offset after exposure
- Fixed image translation
- Image position changes between acquisitions

---

# Symptom Classification

Identify the observed behavior before troubleshooting.

□ Horizontal Shift

□ Vertical Shift

□ Fixed Shift Distance

□ Random Shift

□ Every Image

□ Intermittent

□ Appears After Firmware Upgrade

□ Appears During Continuous Acquisition

---

# Affected Pipeline

Possible image processing path:

```
Detector
    │
    ▼
Gate Driver
    │
    ▼
Readout Circuit
    │
    ▼
ADC
    │
    ▼
FPGA Frame Buffer
    │
    ▼
Image Mapping
    │
    ▼
SDK
    │
    ▼
Application Display
```

Verification Status

```
Detector            □

Gate Driver         □

Readout             □

ADC                 □

FPGA                □

Image Mapping       □

SDK                 □

Application         □
```

---

# Diagnostic Flow

```
                    Image Shift
                          │
             Present in Every Image?
                          │
              ┌───────────┴───────────┐
              │                       │
             NO                      YES
              │                       │
      Check Trigger          Continue
                                      │
                                      ▼
                   SDK Demo Reproduces?
                                      │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
          Customer Application              Continue
                                              │
                                              ▼
                 Offset Calibration Passed?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
               Regenerate Offset            Continue
                                              │
                                              ▼
                  Gain Calibration Passed?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
                Regenerate Gain             Continue
                                              │
                                              ▼
                Trigger Configuration Correct?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
              Correct Trigger Mode         Continue
                                              │
                                              ▼
                 Image Mapping Correct?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
              Investigate FPGA             Continue
                                              │
                                              ▼
                 Hardware Investigation
```

---

# Diagnosis Hint

Image Shift is usually caused by synchronization or image reconstruction problems rather than defective pixels.

Typical investigation order:

1. Trigger synchronization
2. Readout timing
3. FPGA frame buffer
4. Image mapping
5. SDK rendering

If the image shift is reproduced in RAW images, the issue is typically located before image processing.

---

# Hardware Hint

Possible related hardware

★★★★★ FPGA

★★★★★ Timing Controller

★★★★☆ Readout Controller

★★★★☆ Trigger Circuit

★★★☆☆ DDR Buffer

★★☆☆☆ SDK

---

# Expected Result

After each verification:

### Trigger

Expected Result

- Trigger mode matches system configuration.
- Trigger delay is correct.
- Exposure synchronization succeeds.

---

### Offset

Expected Result

- Offset completes successfully.
- New Offset file is generated.
- Detector status = Ready.

---

### Gain

Expected Result

- Gain completes successfully.
- Gain file is updated.
- Image shift remains unchanged or is eliminated.

---

### SDK Demo

Expected Result

- SDK Demo reproduces the same symptom.

If not reproduced:

→ Suspect customer application.

---

# Quick Checklist

Verify:

- □ Firmware Version
- □ SDK Version
- □ Trigger Mode
- □ Trigger Delay
- □ Offset Calibration
- □ Gain Calibration
- □ RAW Image
- □ SDK Demo
- □ Detector Status

---

# Required Evidence

Collect before escalation:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Trigger Configuration
- Exposure Parameters
- RAW Image
- Processed Image
- SDK Log
- Detector Status Screenshot

---

# Possible Root Causes

## Trigger

- Incorrect trigger mode
- Trigger delay mismatch
- Synchronization failure

---

## FPGA

- Frame buffer corruption
- Image mapping error
- Frame synchronization failure

---

## Readout

- Readout timing abnormal
- Frame alignment error

---

## Software

- SDK rendering issue
- Customer application processing error

---

# Recommended Actions

Priority 1

- Verify trigger configuration.
- Verify Offset and Gain calibration.

Priority 2

- Compare RAW and processed images.
- Verify with SDK Demo.

Priority 3

- Verify FPGA frame synchronization.

Priority 4

- Escalate for hardware investigation if required.

---

# Escalation Criteria

Escalate when:

- Image shift is reproducible.
- RAW image shows the same displacement.
- SDK Demo reproduces the issue.
- Trigger configuration has been verified.
- FPGA or timing hardware is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/ImageWorkflow.md

## Case

- 11_Case/Image/ImageShift.md

## Failure Knowledge

- 07_FailureKnowledge/FPGA/
- 07_FailureKnowledge/Readout/
- 07_FailureKnowledge/Trigger/

## Reference

- 15_Reference/ImageReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v3.0 | 2026-08-06 | Added Affected Pipeline and Expected Result |