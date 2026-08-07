# Detector Replacement

> Module: Standard Operating Procedure
>
> SOP ID: SOP-007
>
> Category: Detector Replacement

---

# Scope

This SOP describes the standard procedure for replacing a Flat Panel Detector (FPD).

This procedure applies to:

- Detector hardware failure
- Detector replacement after RMA
- Detector model replacement
- Spare detector deployment
- Engineering verification after replacement

---

# Objective

Replace the detector safely and efficiently while ensuring that the replacement detector operates correctly and maintains normal communication, calibration, and image quality.

---

# Responsibility

| Role | Responsibility |
|------|----------------|
| FAE | Perform detector replacement and verification |
| Technical Support Engineer | Provide remote support when required |
| Customer | Provide installation environment and cooperate during testing |
| Quality Engineer | Verify replacement records if required |

---

# Preconditions

Before replacement, confirm:

- Replacement detector model is correct.
- Replacement detector has passed inspection.
- Detector Serial Number (SN) has been recorded.
- Firmware version has been confirmed.
- SDK version is compatible.
- Required calibration templates are available.
- Customer approval has been obtained.
- Existing detector information has been backed up.

---

# Required Tools

## Hardware

- Replacement Detector
- Host Computer
- Power Adapter
- Ethernet Cable
- Trigger Cable (if required)

## Software

- Detector SDK
- DTDI Tool
- Configuration Tool
- Firmware Upgrade Tool (if required)

---

# Required Files

- Detector.log
- Detector Configuration
- Calibration Templates
- Firmware Package (if required)
- Customer Installation Record

---

# Safety Precautions

Before replacement:

- Turn off detector power.
- Disconnect power before unplugging cables.
- Observe ESD protection requirements.
- Prevent liquid contamination.
- Do not reuse damaged cables or connectors.

---

# Replacement Workflow

```text
Record Original Information

↓

Power Off Detector

↓

Remove Original Detector

↓

Install Replacement Detector

↓

Configure Network

↓

Verify Communication

↓

Verify Firmware

↓

Load / Generate Calibration

↓

Acquire Test Image

↓

Customer Verification

↓

Replacement Completed
```

---

# Procedure

## Step 1 – Record Original Detector Information

### Process

Record:

- Detector Model
- Detector Serial Number
- Firmware Version
- SDK Version
- IP Address
- Calibration Version

Backup:

- Detector.log
- Configuration Files
- Calibration Templates (if available)

### Output

Original detector information archived.

---

## Step 2 – Remove Original Detector

### Process

- Stop image acquisition.
- Disconnect SDK.
- Power off detector.
- Disconnect Ethernet cable.
- Disconnect trigger cable.
- Remove detector.

### Acceptance Criteria

Detector removed safely.

---

## Step 3 – Install Replacement Detector

### Process

- Verify detector model.
- Verify detector SN.
- Connect power.
- Connect Ethernet cable.
- Connect trigger cable (if required).
- Power on detector.

### Acceptance Criteria

Replacement detector starts normally.

---

## Step 4 – Configure Detector

### Process

- Configure IP address.
- Verify subnet mask.
- Configure gateway if required.
- Verify detector communication.

### Acceptance Criteria

Detector responds normally.

### Exception Handling

Refer to:

- SOP/NetworkConfiguration

---

## Step 5 – Verify Communication

### Process

- Connect detector through SDK.
- Verify detector status.
- Read detector information.
- Read temperature.
- Read humidity.

### Acceptance Criteria

Detector status is **Ready**.

---

## Step 6 – Verify Firmware

### Process

Compare:

- Installed firmware version
- Required firmware version

If necessary:

- Upgrade firmware.

### Acceptance Criteria

Firmware version is correct.

### Exception Handling

Refer to:

- SOP/FirmwareUpgrade

---

## Step 7 – Restore Detector Configuration

### Process

Restore or configure:

- Detector parameters
- Network settings
- User parameters
- Working mode

### Acceptance Criteria

Configuration restored successfully.

---

## Step 8 – Restore Calibration

### Process

If existing calibration templates are valid:

- Download templates.
- Select templates.

Otherwise:

- Perform Offset Calibration.
- Perform Gain Calibration.
- Perform Defect Calibration.

### Acceptance Criteria

Calibration completed successfully.

### Exception Handling

Refer to:

- SOP/Calibration

---

## Step 9 – Verify Image Quality

### Process

Acquire standard test images.

Verify:

- Uniformity
- Noise
- Line artifacts
- Defective pixels
- Ghost
- Image distortion

### Acceptance Criteria

Image quality meets acceptance requirements.

---

## Step 10 – Customer Acceptance

### Process

Verify together with customer:

- Communication
- Image acquisition
- Clinical workflow (if applicable)
- Image quality

Obtain customer confirmation.

### Acceptance Criteria

Customer accepts replacement.

---

## Step 11 – Complete Replacement

### Process

Archive:

- Detector.log
- Test Images
- Replacement Record
- Firmware Version
- Calibration Version

Update equipment records.

### Output

Replacement completed.

---

# Acceptance Checklist

- Replacement detector installed.
- Detector powers on normally.
- Detector status is Ready.
- Communication verified.
- Firmware verified.
- Calibration verified.
- Test image acquired successfully.
- Customer acceptance completed.
- Records archived.

---

# Exception Matrix

| Symptom | Possible Cause | Action |
|----------|----------------|--------|
| Detector cannot power on | Power or hardware issue | Verify power supply and hardware |
| Detector cannot connect | Network configuration | Refer to SOP/NetworkConfiguration |
| Firmware mismatch | Incorrect firmware | Upgrade firmware |
| Calibration unavailable | Missing templates | Restore or regenerate templates |
| Poor image quality | Calibration or hardware | Perform calibration and verify detector |

---

# Records

Record:

- Customer Name
- Installation Site
- Replacement Date
- Original Detector SN
- Replacement Detector SN
- Firmware Version
- SDK Version
- Calibration Version
- Detector.log
- Test Images
- Operator
- Customer Confirmation

---

# Notes

- Always archive the original detector information before replacement.
- Verify firmware compatibility before restoring calibration templates.
- Calibration templates from another detector must not be applied unless compatibility has been confirmed.
- If the replacement detector has a different firmware version, complete firmware verification before calibration.
- Perform complete functional verification before returning the detector to service.

---

# Related Documents

- SOP/DetectorInstallation
- SOP/NetworkConfiguration
- SOP/Calibration
- SOP/FirmwareUpgrade
- SOP/ImageTroubleshooting
- 06_Workflow
- 09_DecisionTree
- 11_Case
- 12_ErrorCode
- 13_Template/RMA
- 14_Glossary

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |