# Mosaic Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v3.0
>
> Last Updated: 2026-08-06

---

# Symptom

The acquired image contains mosaic artifacts, missing blocks, repeated blocks, or incorrectly assembled image regions.

Typical symptoms include:

- Image divided into blocks
- Missing image regions
- Repeated image blocks
- Misaligned image tiles
- Corrupted image frame
- Partial image corruption

---

# Symptom Classification

Identify the observed pattern.

□ Fixed Mosaic

□ Random Mosaic

□ Missing Block

□ Repeated Block

□ Corrupted Block

□ Every Image

□ Intermittent

□ Appears During Continuous Acquisition

---

# Affected Pipeline

Possible image acquisition pipeline:

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
FPGA
    │
    ▼
DDR Frame Buffer
    │
    ▼
Frame Packet Assembly
    │
    ▼
SDK
    │
    ▼
Application
```

Verification Status

```
Detector            □

Gate Driver         □

Readout             □

ADC                 □

FPGA                □

DDR Buffer          □

Packet Assembly     □

SDK                 □

Application         □
```

---

# Diagnostic Flow

```
                    Mosaic Artifact
                           │
                Every Image Affected?
                           │
               ┌───────────┴───────────┐
               │                       │
              NO                      YES
               │                       │
      Continuous Capture?       Continue
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
                  RAW Image Also Corrupted?
                                                 │
                    ┌──────────────────┴──────────────────┐
                    │                                     │
                   NO                                    YES
                    │                                     │
           SDK Processing Issue                 Continue
                                                 │
                                                 ▼
                  Frame Packet Complete?
                                                 │
                    ┌──────────────────┴──────────────────┐
                    │                                     │
                   NO                                    YES
                    │                                     │
             Network / Packet Loss              Continue
                                                 │
                                                 ▼
                  DDR Buffer Normal?
                                                 │
                    ┌──────────────────┴──────────────────┐
                    │                                     │
                   NO                                    YES
                    │                                     │
               FPGA Memory Issue                Continue
                                                 │
                                                 ▼
                  FPGA Frame Assembly Normal?
                                                 │
                    ┌──────────────────┴──────────────────┐
                    │                                     │
                   NO                                    YES
                    │                                     │
              FPGA Investigation               Continue
                                                 │
                                                 ▼
                   Hardware Investigation
```

---

# Diagnosis Hint

Mosaic artifacts usually indicate that image data is not reconstructed correctly.

Unlike pixel or line defects, mosaic artifacts are typically caused by:

- Frame assembly errors
- Packet loss
- Buffer corruption
- FPGA processing abnormalities
- Communication interruption

If the RAW image already contains mosaic artifacts, the problem is usually located before SDK processing.

---

# Hardware Hint

Possible related hardware

★★★★★ FPGA

★★★★★ DDR Memory

★★★★☆ Readout Controller

★★★★☆ Communication Interface

★★★☆☆ Network Controller

★★☆☆☆ SDK

---

# Expected Result

### SDK Demo

Expected Result

- Mosaic artifact can be reproduced.

If not reproduced:

→ Investigate customer application.

---

### RAW Image

Expected Result

- RAW image is complete.

If corrupted:

→ Investigate FPGA or frame acquisition.

---

### Communication

Expected Result

- No packet loss.
- Stable network throughput.
- No timeout.

---

### FPGA

Expected Result

- Frame assembly completed correctly.
- Buffer integrity verified.

---

# Quick Checklist

Verify:

- □ Firmware Version
- □ SDK Version
- □ RAW Image
- □ SDK Demo
- □ Network Stability
- □ Packet Loss
- □ Continuous Acquisition
- □ Detector Status

---

# Required Evidence

Collect before escalation:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- RAW Image
- Processed Image
- SDK Log
- Network Capture (if available)
- Detector Status Screenshot

---

# Possible Root Causes

## FPGA

- Frame assembly error
- Buffer corruption
- DMA abnormality

---

## DDR Memory

- Memory corruption
- Buffer overflow

---

## Communication

- Packet loss
- Timeout
- Bandwidth limitation

---

## Software

- SDK reconstruction error
- Customer application processing error

---

# Recommended Actions

Priority 1

- Verify SDK Demo.
- Compare RAW and processed images.

Priority 2

- Verify communication stability.
- Check packet loss.

Priority 3

- Verify FPGA frame assembly.
- Verify DDR buffer.

Priority 4

- Escalate for FPGA investigation.

---

# Escalation Criteria

Escalate when:

- Mosaic artifacts are reproducible.
- RAW image contains the same corruption.
- SDK Demo reproduces the issue.
- Network communication has been verified.
- FPGA or memory hardware is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/ImageWorkflow.md

## Case

- 11_Case/Image/Mosaic.md

## Failure Knowledge

- 07_FailureKnowledge/FPGA/
- 07_FailureKnowledge/Readout/
- 07_FailureKnowledge/Communication/

## Reference

- 15_Reference/ImageReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v3.0 | 2026-08-06 | Initial release |