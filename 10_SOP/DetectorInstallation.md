# Detector Installation

> Module: Standard Operating Procedure
>
> SOP ID: SOP-001
>
> Category: Installation

---

# Scope

This SOP describes the complete installation procedure for Flat Panel Detectors (FPDs), including hardware preparation, software preparation, detector connection, functional verification, and final acceptance.

This procedure applies to both first-time installations and detector replacements.

---

# Objective

Ensure that the detector is installed correctly, communicates normally with the host computer, and is ready for calibration and image acquisition.

---

# Responsibility

| Role | Responsibility |
|------|----------------|
| FAE | Perform detector installation and verification |
| Technical Support Engineer | Provide remote assistance if required |
| Customer | Provide installation environment and equipment |
| R&D Engineer | Support abnormal cases requiring escalation |

---

# Preconditions

Before installation, confirm the following:

- Detector model matches the project requirements.
- Detector appearance has no visible damage.
- Battery is sufficiently charged (wireless detector).
- Power supply is available.
- Host computer is operational.
- Correct SDK version is installed.
- Detector firmware is compatible with the SDK.
- Required calibration files are available (if applicable).

---

# Required Tools

Hardware

- Detector
- Host Computer
- Power Adapter
- Ethernet Cable
- Trigger Cable (if required)
- Network Switch (if required)

Software

- Detector SDK
- Detector Configuration Tool
- DTDI Tool (if required)

---

# Required Files

- SDK Installation Package
- Detector Configuration Files
- Firmware Package (if required)
- Calibration Templates (if required)
- License File (if required)

---

# Safety Precautions

Before installation:

- Do not connect or disconnect cables while power is unstable.
- Avoid electrostatic discharge (ESD).
- Do not place heavy objects on the detector.
- Prevent liquid from entering the detector.
- Verify the detector model and serial number before configuration.

---

# Procedure

## Step 1 – Verify Equipment

### Input

Detector package.

### Process

- Verify detector model.
- Verify serial number.
- Check appearance.
- Inspect connectors.
- Confirm accessories are complete.

### Output

Detector verified.

### Acceptance Criteria

- No physical damage.
- Correct model.
- Correct accessories.

### Exception Handling

If abnormalities are found, stop installation and report to the supplier.

---

## Step 2 – Prepare Host Computer

### Input

Installation computer.

### Process

- Verify operating system.
- Install SDK.
- Install required drivers.
- Disable firewall or configure exceptions if necessary.
- Confirm sufficient disk space.

### Output

Host computer ready.

### Acceptance Criteria

SDK installed successfully.

### Exception Handling

Refer to:

- DecisionTree/Software
- ErrorCode/Initialization

---

## Step 3 – Connect Detector

### Input

Detector and host computer.

### Process

- Connect power.
- Connect Ethernet cable.
- Connect trigger cable (if required).
- Power on detector.
- Wait until detector startup completes.

### Output

Detector powered on.

### Acceptance Criteria

Detector starts normally.

### Exception Handling

If the detector cannot power on, refer to:

- FailureKnowledge/SystemFailure
- StartupFailure

---

## Step 4 – Configure Network

### Input

Detector network interface.

### Process

- Verify IP address.
- Verify subnet mask.
- Verify gateway if required.
- Confirm host and detector are on the same subnet.
- Perform Ping test.

### Output

Network configured.

### Acceptance Criteria

Detector responds to Ping.

### Exception Handling

Refer to:

- SOP/NetworkConfiguration
- DecisionTree/Connection

---

## Step 5 – Connect Through SDK

### Input

Detector SDK.

### Process

- Launch application.
- Execute detector connection.
- Verify detector status.

### Output

Detector connected.

### Acceptance Criteria

Detector state becomes Ready.

### Exception Handling

Refer to:

- DecisionTree/Connection
- ErrorCode/Communication

---

## Step 6 – Verify Detector

### Input

Connected detector.

### Process

- Read detector information.
- Read firmware version.
- Read temperature.
- Read humidity.
- Verify communication.

### Output

Detector verified.

### Acceptance Criteria

All information can be read successfully.

### Exception Handling

Refer to:

- DecisionTree/Device
- ErrorCode/Device

---

## Step 7 – Acquire Test Image

### Input

Detector Ready.

### Process

- Start acquisition.
- Perform exposure.
- Receive image.
- Verify image quality.

### Output

Test image acquired.

### Acceptance Criteria

- Image received successfully.
- No communication errors.
- No obvious image artifacts.

### Exception Handling

Refer to:

- SOP/ImageTroubleshooting
- DecisionTree/Image

---

## Step 8 – Complete Installation

### Input

Verified detector.

### Process

- Save detector information.
- Record firmware version.
- Record SDK version.
- Archive installation information.

### Output

Installation completed.

---

# Acceptance Checklist

- Detector powers on normally.
- Detector can be connected.
- Network communication is normal.
- Detector status is Ready.
- Firmware version verified.
- SDK version verified.
- Test image acquired successfully.
- No abnormal events reported.

---

# Records

Record the following information:

- Customer Name
- Installation Date
- Detector Model
- Detector Serial Number
- Firmware Version
- SDK Version
- Computer Name
- IP Address
- Operator
- Test Image
- Detector.log

---

# Related Documents

- 03_Hardware
- 04_Communication
- 05_Calibration
- 06_Workflow/PowerOnWorkflow
- 06_Workflow/ConnectionWorkflow
- 09_DecisionTree/Connection
- 11_Case/Communication
- 12_ErrorCode/Communication
- 14_Glossary

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |