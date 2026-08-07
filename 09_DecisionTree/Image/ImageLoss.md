# Image Loss Decision Tree

> Module: Image
>
> Category: Master Decision Tree
>
> Version: v4.0
>
> Last Updated: 2026-08-06

---

# Purpose

This decision tree is the primary entry point for troubleshooting when no image is acquired.

Image Loss may originate from:

- Detector
- Power
- Network
- SDK
- Firmware
- Trigger
- Generator
- Readout
- FPGA
- Application Software

This document guides FAE engineers through systematic layer-by-layer isolation.

---

# Symptom

No image is acquired after exposure.

Typical symptoms include:

- No image displayed
- Exposure completed but no image received
- Timeout waiting for image
- Image acquisition failed
- Detector triggered but no frame received
- Black display after exposure

---

# Symptom Classification

Before troubleshooting, identify the observed behavior.

□ Detector Offline

□ Detector Online but No Image

□ Exposure Not Triggered

□ Trigger Sent but No Frame Returned

□ Timeout

□ Intermittent Image Loss

□ Continuous Image Loss

□ Multi-frame Acquisition Failure

---

# Layer Isolation

Troubleshoot from the application layer down to the detector hardware.

```
Application
      │
      ▼
SDK
      │
      ▼
Communication
      │
      ▼
FPGA
      │
      ▼
Readout
      │
      ▼
ADC
      │
      ▼
TFT
      │
      ▼
Detector
```

| Layer | Verification | If Failed |
|---------|-------------|-----------|
| Application | SDK Demo | Customer Software |
| SDK | SDK Version | Firmware |
| Communication | Ping / Network | Network |
| FPGA | Detector Status | FPGA Investigation |
| Readout | Detector Log | Readout Investigation |
| Detector | Ready Status | Hardware Investigation |

---

# Acquisition Timeline

Follow the acquisition sequence.

```
Power On
    │
    ▼
Detector Boot
    │
    ▼
Detector Online
    │
    ▼
Network Connected
    │
    ▼
SDK Detects Detector
    │
    ▼
Read Detector Information
    │
    ▼
Detector Ready
    │
    ▼
Trigger Received
    │
    ▼
Exposure Started
    │
    ▼
Frame Readout
    │
    ▼
Frame Transfer
    │
    ▼
Image Reconstruction
    │
    ▼
Display
```

If any step fails, investigate that stage before proceeding.

---

# Affected Pipeline

Possible hardware path

```
Detector

↓

TFT

↓

Readout

↓

ADC

↓

FPGA

↓

DDR Buffer

↓

Ethernet

↓

SDK

↓

Application
```

Verification Status

```
Detector          □

Power             □

Trigger           □

Readout           □

ADC               □

FPGA              □

Network           □

SDK               □

Application       □
```

---

# Diagnostic Flow

```
                    Image Loss
                         │
              Detector Online?
                         │
          ┌──────────────┴──────────────┐
          │                             │
         NO                            YES
          │                             │
DetectorOffline.md               Continue
                                       │
                                       ▼
                 SDK Demo Detects Detector?
                                       │
                  ┌────────────────────┴────────────────────┐
                  │                                         │
                 NO                                        YES
                  │                                         │
           SDK Investigation                       Continue
                                                    │
                                                    ▼
                    Detector Status = Ready?
                                                    │
                   ┌────────────────────┴────────────────────┐
                   │                                         │
                  NO                                        YES
                   │                                         │
            Detector Initialization                 Continue
                                                    │
                                                    ▼
                   Trigger Received?
                                                    │
                   ┌────────────────────┴────────────────────┐
                   │                                         │
                  NO                                        YES
                   │                                         │
             Trigger Investigation                  Continue
                                                    │
                                                    ▼
                  Exposure Completed?
                                                    │
                   ┌────────────────────┴────────────────────┐
                   │                                         │
                  NO                                        YES
                   │                                         │
            Generator Investigation                Continue
                                                    │
                                                    ▼
                 Frame Received?
                                                    │
                   ┌────────────────────┴────────────────────┐
                   │                                         │
                  NO                                        YES
                   │                                         │
           Readout / FPGA Investigation             Continue
                                                    │
                                                    ▼
               Image Displayed?
                                                    │
                   ┌────────────────────┴────────────────────┐
                   │                                         │
                  NO                                        YES
                   │                                         │
           Image Processing Investigation          Problem Solved
```

---

# Diagnosis Hint

Image Loss is usually caused by one of the following categories:

1. Detector not initialized
2. Communication failure
3. Trigger failure
4. Exposure failure
5. Readout failure
6. FPGA frame acquisition failure
7. SDK or application failure

Always verify each layer before moving to hardware replacement.

---

# Hardware Hint

Most likely hardware modules

★★★★★ Communication

★★★★★ FPGA

★★★★★ Readout

★★★★☆ Trigger

★★★★☆ Detector

★★★☆☆ ADC

★★★☆☆ Power

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| SDK Demo | Verify detector communication | Detector detected and image acquired |
| Ping | Verify Ethernet communication | Stable response |
| Detector Log | Verify detector state | Ready |
| Firmware Tool | Read firmware version | Correct version |
| Wireshark | Analyze packet transfer | No packet loss |
| Calibration Tool | Verify detector readiness | Calibration available |

---

# Expected Result

Power

✓ Detector powered correctly.

Network

✓ Stable communication.

SDK

✓ Detector detected successfully.

Detector

✓ Ready.

Trigger

✓ Trigger received.

Exposure

✓ Exposure completed.

Frame

✓ Frame transferred successfully.

Display

✓ Image displayed normally.

---

# Quick Checklist

□ Detector Online

□ Detector Ready

□ Firmware Verified

□ SDK Verified

□ Network Stable

□ Trigger Verified

□ Generator Ready

□ Frame Received

□ SDK Demo Tested

---

# Required Evidence

Collect before escalation

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Detector Log
- SDK Log
- Network Configuration
- Trigger Configuration
- Exposure Parameters
- Wireshark Capture (if available)
- Detector Status Screenshot

---

# Possible Root Causes

## Communication

- Ethernet disconnected
- Packet loss
- IP conflict

## Firmware

- Version mismatch
- Initialization failure

## Trigger

- Trigger not received
- Trigger mode incorrect

## Readout

- Readout failure
- Frame timeout

## FPGA

- Frame acquisition failure
- DMA abnormality

## Software

- SDK failure
- Customer application issue

---

# Recommended Actions

Priority 1

- Verify detector online status.
- Verify SDK Demo.

Priority 2

- Verify network communication.
- Verify detector Ready state.

Priority 3

- Verify trigger and exposure.

Priority 4

- Verify frame transfer and FPGA status.

Priority 5

- Escalate for hardware investigation.

---

# Escalation Criteria

Escalate when:

- Detector is online but no image can be acquired.
- SDK Demo reproduces the issue.
- Frame acquisition repeatedly fails.
- Network and firmware have been verified.
- FPGA or readout hardware failure is suspected.

---

# Related Documents

## Connection

- 09_DecisionTree/Connection/DetectorOffline.md

## Firmware

- 09_DecisionTree/Firmware/VersionMismatch.md

## Calibration

- 09_DecisionTree/Calibration/OffsetGenerationFailed.md
- 09_DecisionTree/Calibration/GainCalibrationFailed.md
- 09_DecisionTree/Calibration/DefectFailure.md

## Image

- 09_DecisionTree/Image/Noise.md
- 09_DecisionTree/Image/ImageShift.md
- 09_DecisionTree/Image/Mosaic.md
- 09_DecisionTree/Image/Lag.md
- 09_DecisionTree/Image/Ghost.md

## Failure Knowledge

- 07_FailureKnowledge/

## Reference

- 15_Reference/SDKReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v4.0 | 2026-08-06 | Initial Master Decision Tree |