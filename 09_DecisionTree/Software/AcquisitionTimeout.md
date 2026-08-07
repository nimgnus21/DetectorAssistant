# Acquisition Timeout Decision Tree

> Module: Software
>
> Category: Decision Tree
>
> Version: v4.0
>
> Last Updated: 2026-08-06

---

# Purpose

This decision tree is used when image acquisition starts successfully, but no image is received within the expected timeout period.

Typical acquisition sequence:

Application

↓

SDK

↓

Trigger

↓

Generator Exposure

↓

Detector Readout

↓

FPGA Frame Buffer

↓

Frame Transfer

↓

SDK Callback

↓

Display

Failure at any stage may result in an acquisition timeout.

---

# Symptom

The detector is online and initialized correctly, but image acquisition times out.

Typical symptoms include:

- Acquisition Timeout
- Wait Image Timeout
- Frame Receive Timeout
- Image Receive Failed
- SDK Wait Timeout
- Callback Timeout
- No Image Returned

---

# Symptom Classification

Identify the observed behavior.

□ Timeout Every Exposure

□ Intermittent Timeout

□ First Image Timeout

□ Continuous Acquisition Timeout

□ Single Detector Only

□ Multiple Detectors

□ Large Image Only

□ Random Timeout

---

# Acquisition Timeline

Follow the complete acquisition sequence.

```
Start Acquisition
        │
        ▼
Trigger Received
        │
        ▼
Generator Exposure
        │
        ▼
Detector Integration
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
DDR Buffer
        │
        ▼
Ethernet Transfer
        │
        ▼
SDK Callback
        │
        ▼
Application
```

Stop troubleshooting immediately at the first failed stage.

---

# Timeout Layer Isolation

```
Application
      │
      ▼
SDK
      │
      ▼
Network
      │
      ▼
FPGA
      │
      ▼
Readout
      │
      ▼
Detector
```

| Layer | Verification | If Failed |
|---------|-------------|-----------|
| Application | Callback executed | Application Debug |
| SDK | SDK Demo | SDK Investigation |
| Network | Ping / Wireshark | Network |
| FPGA | Frame Generated | FPGA Investigation |
| Readout | Detector Log | Readout |
| Detector | Exposure Status | Trigger / Hardware |

---

# Time Budget Reference

| Stage | Typical Status |
|---------|----------------|
| Trigger | Received |
| Exposure | Completed |
| Detector Readout | Completed |
| FPGA Processing | Completed |
| Frame Transfer | Completed |
| SDK Callback | Executed |
| Display | Image Visible |

Example timeout locations:

Trigger Timeout

↓

Trigger configuration

---

Exposure Timeout

↓

Generator

---

Readout Timeout

↓

Detector Readout

---

Transfer Timeout

↓

Ethernet

---

Callback Timeout

↓

SDK / Application

---

# Affected Pipeline

```
Application

↓

SDK

↓

Network

↓

FPGA

↓

ADC

↓

Readout

↓

Detector
```

Verification Status

```
Application      □

SDK              □

Network          □

Trigger          □

Detector         □

Readout          □

FPGA             □

Frame Transfer   □
```

---

# Diagnostic Flow

```
                Acquisition Timeout
                        │
               SDK Initialized?
                        │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
SDKInitializationFailed         Continue
                                       │
                                       ▼
               Detector Ready?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
Detector Initialization         Continue
                                       │
                                       ▼
             Trigger Received?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
Trigger Investigation           Continue
                                       │
                                       ▼
           Exposure Completed?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
Generator Investigation         Continue
                                       │
                                       ▼
            Frame Generated?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
Readout / FPGA                  Continue
                                       │
                                       ▼
          Frame Transferred?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
Network Investigation          Continue
                                       │
                                       ▼
        SDK Callback Executed?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
SDK Investigation             Application Investigation
```

---

# Error Mapping

| Symptom | Possible Module | Next Decision Tree |
|----------|-----------------|--------------------|
| Trigger Timeout | Trigger | Trigger Failure |
| Exposure Timeout | Generator | Generator Workflow |
| No Frame | FPGA / Readout | ImageLoss |
| Connection Lost | Network | DetectorOffline |
| SDK Timeout | SDK | SDKInitializationFailed |
| Callback Missing | Application | APIError |

---

# Diagnosis Hint

Acquisition timeout usually occurs because image acquisition stops before image delivery is completed.

Typical investigation order:

1. Trigger
2. Generator
3. Detector Status
4. Readout
5. FPGA
6. Ethernet Transfer
7. SDK Callback
8. Application

Always determine which stage stopped first.

---

# Software Hint

Most likely affected modules

★★★★★ Trigger

★★★★★ Readout

★★★★★ FPGA

★★★★☆ Network

★★★★☆ SDK

★★★☆☆ Application

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| SDK Demo | Verify acquisition | Image acquired |
| Detector Utility | Detector status | Ready |
| Wireshark | Verify frame transfer | Frame packets received |
| Ping | Verify communication | Stable response |
| Detector Log | Exposure / Readout | No errors |
| Generator Log | Verify exposure | Exposure completed |

---

# Expected Result

### Trigger

Expected Result

- Trigger received successfully.

---

### Exposure

Expected Result

- Exposure completed normally.

---

### Detector

Expected Result

- Detector status remains Ready.

---

### Frame Transfer

Expected Result

- Frame packets received completely.

---

### SDK

Expected Result

- Callback executed successfully.

---

### Application

Expected Result

- Image displayed without timeout.

---

# Quick Checklist

Verify

□ Detector Ready

□ SDK Demo

□ Trigger Configuration

□ Exposure Completed

□ Generator Status

□ Detector Log

□ Network Stable

□ Wireshark Capture

□ Callback Executed

---

# Required Evidence

Collect before escalation

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Trigger Configuration
- Exposure Parameters
- Detector Log
- SDK Log
- Generator Log
- Wireshark Capture
- Error Code
- Timeout Screenshot

---

# Possible Root Causes

## Trigger

- Trigger not received
- Incorrect trigger mode

---

## Generator

- Exposure not started
- Exposure aborted

---

## Detector

- Detector not ready
- Readout abnormal

---

## FPGA

- Frame generation failed
- DMA timeout

---

## Network

- Packet loss
- Network interruption

---

## SDK

- Callback timeout
- Receive timeout

---

## Application

- Callback not handled
- UI thread blocked

---

# Recommended Actions

Priority 1

- Verify SDK Demo.
- Verify detector Ready status.

Priority 2

- Verify trigger and exposure.

Priority 3

- Verify detector log and frame generation.

Priority 4

- Verify Ethernet communication using Wireshark.

Priority 5

- Verify SDK callback and application processing.

Priority 6

- Escalate if timeout remains reproducible after all software and communication checks.

---

# Escalation Criteria

Escalate when:

- SDK Demo reproduces the timeout.
- Detector status remains Ready.
- Exposure is confirmed complete.
- Frame transfer or FPGA abnormalities are suspected.
- The issue is reproducible on multiple PCs or applications.

---

# Related Documents

## Software

- 09_DecisionTree/Software/SDKInitializationFailed.md
- 09_DecisionTree/Software/DetectorNotFound.md
- 09_DecisionTree/Software/APIError.md
- 09_DecisionTree/Software/SDKException.md

## Image

- 09_DecisionTree/Image/ImageLoss.md

## Connection

- 09_DecisionTree/Connection/DetectorOffline.md

## Reference

- 15_Reference/SDKReference.md
- 15_Reference/TrainingReference.md

## Tools

- 17_Tools/SDKDemo.md
- 17_Tools/Wireshark.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v4.0 | 2026-08-06 | Initial release |