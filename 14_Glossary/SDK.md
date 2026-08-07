# SDK

> Module: Glossary
>
> Category: SDK Terminology

---

# Overview

This document defines the standard terminology related to the Software Development Kit (SDK) used for detector control, communication, image acquisition, calibration, and firmware management.

The terminology defined here serves as the unified reference for SDK-related documentation throughout DetectorAssistant.

---

# SDK

## Definition

Software Development Kit.

A software library that provides APIs for controlling the detector and accessing its functions.

## Typical Functions

- Detector Connection
- Image Acquisition
- Calibration
- Firmware Upgrade
- Parameter Configuration

---

# API

## Definition

Application Programming Interface.

A callable software interface provided by the SDK.

## Examples

- Cmd_Connect
- Cmd_StartAcq
- Cmd_Reset

---

# Command

## Definition

An SDK function used to send an operation request to the detector.

## Examples

- Connect Detector
- Start Acquisition
- Generate Calibration
- Upgrade Firmware

---

# Event

## Definition

An asynchronous notification sent from the SDK to the application.

## Purpose

Notify the application of detector status, task results, warnings, errors, or image arrival.

## Examples

- Evt_Image
- Evt_TaskResult_Succeed
- Evt_GeneralError

---

# Callback

## Definition

A user-defined function registered with the SDK to receive events asynchronously.

## Purpose

Handle detector events without polling.

---

# Callback Function

## Definition

A software function executed automatically when an SDK event occurs.

---

# Attribute

## Definition

A readable or writable parameter exposed by the SDK.

## Examples

- Detector Information
- Firmware Version
- Temperature
- Humidity

---

# Property

## Definition

A detector configuration value maintained by the SDK.

Property values may be stored in detector RAM or ROM.

---

# Detector Object

## Definition

The software instance representing a detector managed by the SDK.

---

# Session

## Definition

The communication lifecycle between an application and a detector.

Typical stages include:

- Create Object
- Connect
- Operate
- Disconnect
- Destroy Object

---

# Acquisition

## Definition

The process of receiving image data from the detector.

## Types

- Single Acquisition
- Continuous Acquisition

---

# Single Acquisition

## Definition

Acquisition of a single image after one exposure.

---

# Continuous Acquisition

## Definition

Continuous reception of image frames without recreating the acquisition session.

---

# Image Buffer

## Definition

Memory allocated by the SDK to temporarily store incoming image data.

---

# Frame Buffer

## Definition

Memory area used to store one or more acquired image frames.

---

# Task

## Definition

An executable operation managed internally by the SDK.

## Examples

- Calibration
- Firmware Upgrade
- Image Acquisition

---

# Task Result

## Definition

The execution result returned by the SDK.

## Typical Results

- Success
- Failed
- Cancelled

---

# Timeout

## Definition

The maximum waiting time before an operation is considered unsuccessful.

---

# Initialization

## Definition

The process of preparing the SDK before detector communication begins.

---

# Working Directory

## Definition

The directory used by the SDK to store logs, calibration templates, configuration files, and temporary data.

---

# Detector.log

## Definition

The runtime log generated automatically by the SDK.

## Purpose

Record communication, commands, events, warnings, and errors for troubleshooting.

---

# Configuration File

## Definition

A file containing detector or SDK configuration parameters.

---

# DLL

## Definition

Dynamic Link Library.

The binary library implementing SDK functionality.

---

# Thread Safety

## Definition

The capability of the SDK to operate correctly when accessed from multiple threads.

---

# SDK Version

## Definition

The release version of the installed SDK.

## Purpose

Used for compatibility verification and troubleshooting.

---

# Firmware Compatibility

## Definition

The compatibility relationship between SDK versions and detector firmware versions.

---

# SDK Exception

## Definition

An unexpected software exception occurring during SDK execution.

---

# Return Value

## Definition

The value returned immediately after an SDK API is called.

It indicates whether the command has been accepted, not necessarily whether the operation has completed.

---

# Asynchronous Operation

## Definition

An SDK operation that returns immediately while execution continues internally.

Completion is reported through Events.

---

# Synchronous Operation

## Definition

An SDK operation that does not return until execution has completed.

---

# Related SDK Commands

Examples include:

- Cmd_Connect
- Cmd_Disconnect
- Cmd_StartAcq
- Cmd_StopAcq
- Cmd_Reset
- Cmd_UpdateFirmware
- Cmd_OffsetGeneration

---

# Related SDK Events

Examples include:

- Evt_Image
- Evt_GeneralWarn
- Evt_GeneralError
- Evt_TaskResult_Succeed
- Evt_TaskResult_Failed

---

# Related Modules

- 02_SDK
- 06_Workflow
- 09_DecisionTree
- 11_Case
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |