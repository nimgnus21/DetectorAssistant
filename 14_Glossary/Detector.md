# Detector

> Module: Glossary
>
> Category: Detector Terminology

---

# Overview

This document defines the standard terminology related to flat panel detectors (FPDs) used throughout the DetectorAssistant knowledge base.

These terms are referenced by SDK documentation, workflows, troubleshooting guides, SOPs, and technical support documents.

---

# Detector

## Definition

A Flat Panel Detector (FPD) is an X-ray imaging device that converts X-ray energy into digital image data.

## Typical Usage

- Detector Connection
- Detector Initialization
- Detector Configuration
- Detector Calibration

## Related Terms

- Static Detector
- Dynamic Detector
- Detector SN

---

# Static Detector

## Definition

A detector designed primarily for single-frame image acquisition.

## Characteristics

- Single exposure acquisition
- Low frame rate
- Typically used in DR systems

## Related Terms

- Dynamic Detector
- Acquisition

---

# Dynamic Detector

## Definition

A detector capable of continuous image acquisition at configurable frame rates.

## Characteristics

- Continuous acquisition
- Multiple application modes
- Supports FPS configuration

## Related Terms

- Frame Rate
- Application Mode

---

# Detector SN

## Definition

The unique serial number assigned to each detector.

## Purpose

Used for:

- Detector identification
- License management
- Calibration template matching
- Service records

---

# Detector ID

## Definition

A unique identifier used by the SDK to locate and communicate with a detector.

## Related Terms

- Detector SN
- Detector Connection

---

# Detector Status

## Definition

The current operating state of the detector.

Typical states include:

- Unknown
- Ready
- Busy

---

# Unknown

## Definition

The detector object has been created but is not connected.

## Available Operations

- Read configuration
- Modify configuration
- Scan detectors
- Open local files

---

# Ready

## Definition

The detector is connected and ready for normal operation.

## Typical Operations

- Image acquisition
- Calibration
- Firmware upgrade
- Parameter configuration

---

# Busy

## Definition

The detector is executing an internal task and temporarily rejects additional device operations.

## Typical Causes

- Image acquisition
- Calibration
- Firmware upgrade
- Internal processing

---

# Detector Connection

## Definition

The process of establishing communication between the SDK and the detector.

## Successful Result

The detector enters the **Ready** state.

---

# Detector Disconnection

## Definition

The detector is disconnected intentionally or unexpectedly.

## Typical Causes

- Network interruption
- Power loss
- Manual disconnect

---

# Detector Reset

## Definition

Restarting the detector to reinitialize its operating state.

## Notes

For dynamic detectors, if Offset, Gain, or Defect templates were previously loaded, the appropriate calibration subset may need to be selected again after reset.

---

# Detector Configuration

## Definition

The process of reading or modifying detector operating parameters.

## Examples

- Network settings
- Trigger mode
- Application mode
- Calibration subset

---

# Application Mode

## Definition

A predefined operating configuration for a detector.

## Typical Parameters

- FPS
- PGA
- Binning
- Exposure timing

---

# Subset

## Definition

A unique configuration name used to identify an application mode and its associated calibration templates.

## Purpose

Used when selecting calibration templates or application modes.

---

# Frame

## Definition

A single image acquired by the detector.

## Related Terms

- Continuous Acquisition
- Frame Rate

---

# Frame Rate (FPS)

## Definition

The number of image frames acquired per second.

## Unit

FPS (Frames Per Second)

---

# Continuous Acquisition

## Definition

A detector operating mode in which image frames are acquired continuously.

## Related Terms

- Dynamic Detector
- Frame
- FPS

---

# Trigger Mode

## Definition

The method used to initiate image acquisition.

## Common Types

- Software Trigger
- Hardware Trigger
- AED Trigger

---

# Exposure Window

## Definition

The time interval during which the detector accepts X-ray exposure.

---

# ROI (Region of Interest)

## Definition

A specified region within an image selected for processing or analysis.

---

# Binning

## Definition

A technique that combines adjacent pixels into a larger effective pixel.

## Purpose

- Increase sensitivity
- Reduce image noise
- Increase acquisition speed

---

# PGA (Programmable Gain Amplifier)

## Definition

An adjustable analog amplifier used before analog-to-digital conversion to optimize detector signal amplitude.

---

# Detector Working Directory

## Definition

The directory used by the SDK to store detector configuration files, calibration templates, logs, and related resources.

## Typical Contents

- Detector.log
- Calibration Templates
- Configuration Files

---

# Related Modules

- 02_SDK
- 03_Hardware
- 05_Calibration
- 06_Workflow
- 07_FailureKnowledge
- 09_DecisionTree
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |