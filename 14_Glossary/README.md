# Glossary

> DetectorAssistant Technical Glossary

---

# Overview

The Glossary module provides standardized definitions for technical terms used throughout the DetectorAssistant knowledge base.

Its purpose is to ensure consistent terminology across documentation, reduce ambiguity, and help engineers quickly understand concepts encountered during installation, calibration, troubleshooting, firmware upgrades, software development, and after-sales support.

This module serves as the unified terminology reference for all other modules.

---

# Scope

The glossary covers terminology related to:

- Detector Hardware
- Detector Firmware
- SDK
- Network Communication
- Calibration
- Image Processing
- X-ray Generator
- Software Development
- Technical Support

---

# Directory Structure

```text
14_Glossary
├── README.md
├── Detector.md
├── Hardware.md
├── SDK.md
├── Communication.md
├── Calibration.md
├── Image.md
├── Firmware.md
├── Network.md
└── Generator.md
```

---

# Module Description

## Detector

Detector structure, operating states, detector parameters, detector identification, detector working modes, and detector-related terminology.

---

## Hardware

Hardware architecture and components.

Examples:

- TFT
- Scintillator
- ADC
- FPGA
- Gate Driver
- Readout Board
- Power Board

---

## SDK

Software Development Kit terminology.

Examples:

- SDK
- API
- Callback
- Event
- Command
- Attribute
- Acquisition
- Trigger

---

## Communication

Detector communication terminology.

Examples:

- TCP
- UDP
- Ping
- Packet
- Timeout
- DHCP
- Static IP
- Broadcast

---

## Calibration

Calibration terminology.

Examples:

- Offset
- Gain
- Defect
- PreOffset
- HW Gain
- HW Defect
- Ghost Correction
- Template

---

## Image

Image acquisition and processing terminology.

Examples:

- Raw Image
- Corrected Image
- Dynamic Range
- Pixel
- Bad Pixel
- Lag
- Ghost
- Noise
- Saturation

---

## Firmware

Firmware-related terminology.

Examples:

- Firmware
- Bootloader
- Upgrade
- Rollback
- Version
- Flash

---

## Network

Computer networking terminology.

Examples:

- IP Address
- Subnet Mask
- Gateway
- MAC Address
- Bandwidth
- Latency
- Packet Loss

---

## Generator

X-ray generator terminology.

Examples:

- Trigger
- AED
- DR Trigger
- Exposure
- Exposure Window
- kV
- mA
- mAs
- Pulse Width

---

# Writing Standard

Each glossary entry should include the following fields:

```text
Term

Definition

Purpose

Typical Usage

Related Terms

Related Documents
```

---

# Example

## Offset

Definition

A calibration template used to remove the detector's dark current signal before image correction.

Purpose

Improve image consistency by compensating for detector background noise.

Related Terms

- Gain
- Defect
- Template

Related Documents

- 05_Calibration
- 06_Workflow
- 11_Case

---

# Related Modules

- 03_Hardware
- 04_Communication
- 05_Calibration
- 06_Workflow
- 07_FailureKnowledge
- 08_Image
- 09_DecisionTree
- 11_Case
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |