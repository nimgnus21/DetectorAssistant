# Preventive Maintenance

> Module: Standard Operating Procedure
>
> SOP ID: SOP-008
>
> Category: Preventive Maintenance

---

# Scope

This SOP describes the standard preventive maintenance procedure for Flat Panel Detectors (FPDs).

This procedure applies to:

- Periodic maintenance
- Customer routine inspection
- Annual maintenance
- Preventive health checks
- Post-installation inspection

---

# Objective

Maintain detector performance through regular inspection and preventive maintenance, reducing unexpected failures and extending service life.

---

# Responsibility

| Role | Responsibility |
|------|----------------|
| FAE | Perform preventive maintenance |
| Customer | Cooperate during maintenance |
| Technical Support Engineer | Analyze abnormal findings |
| Quality Engineer | Review maintenance records when required |

---

# Maintenance Interval

| Item | Recommended Interval |
|------|----------------------|
| Visual inspection | Every visit |
| Communication verification | Every visit |
| Image quality verification | Every visit |
| Firmware verification | Every 6 months |
| Calibration verification | Every 6 months or after repair |
| Complete preventive maintenance | Every 12 months |

---

# Required Tools

## Hardware

- Detector
- Host Computer
- Ethernet Cable
- Test Phantom (if available)

## Software

- SDK Tool
- DTDI Tool
- Image Viewer

---

# Required Files

- Detector.log
- Maintenance Record
- Calibration Information
- Firmware Information

---

# Safety Precautions

- Disconnect power before inspecting connectors.
- Prevent electrostatic discharge (ESD).
- Do not use corrosive cleaning agents.
- Do not open the detector enclosure.

---

# Maintenance Workflow

```text
Visual Inspection

↓

Power Verification

↓

Communication Verification

↓

Detector Status Check

↓

Firmware Verification

↓

Calibration Verification

↓

Image Quality Verification

↓

Log Collection

↓

Maintenance Record

↓

Maintenance Completed
```

---

# Procedure

## Step 1 – Visual Inspection

### Process

Inspect:

- Detector housing
- Display panel
- Connectors
- Ethernet port
- Trigger connector
- Battery compartment (wireless models)

### Acceptance Criteria

No visible damage.

---

## Step 2 – Verify Power

### Process

Verify:

- Detector starts normally.
- Battery level (wireless).
- External power supply.

### Acceptance Criteria

Power supply operates normally.

---

## Step 3 – Verify Communication

### Process

Check:

- Ethernet connection
- Detector connection
- SDK connection
- Ping test

### Acceptance Criteria

Communication stable.

---

## Step 4 – Verify Detector Status

### Process

Read:

- Detector State
- Temperature
- Humidity
- Detector Information

### Acceptance Criteria

Detector status is **Ready**.

---

## Step 5 – Verify Firmware

### Process

Verify:

- Firmware Version
- SDK Compatibility

Determine whether an upgrade is recommended.

### Acceptance Criteria

Firmware compatible with deployed SDK.

---

## Step 6 – Verify Calibration

### Process

Verify:

- Offset Template
- Gain Template
- Defect Template
- Active Calibration SubSet

### Acceptance Criteria

Calibration valid.

---

## Step 7 – Verify Image Quality

### Process

Acquire standard test image.

Inspect:

- Uniformity
- Noise
- Dead Pixels
- Line Artifacts
- Ghost
- Contrast

### Acceptance Criteria

Image quality acceptable.

---

## Step 8 – Collect Logs

### Process

Archive:

- Detector.log
- Firmware Version
- SDK Version
- Test Images

### Acceptance Criteria

Maintenance evidence archived.

---

## Step 9 – Complete Maintenance

### Process

Complete maintenance report.

Record:

- Inspection items
- Findings
- Corrective actions
- Recommendations

---

# Maintenance Checklist

| Inspection Item | Status |
|-----------------|--------|
| Housing | □ Pass □ Fail |
| Connector | □ Pass □ Fail |
| Power | □ Pass □ Fail |
| Communication | □ Pass □ Fail |
| Firmware | □ Pass □ Fail |
| Calibration | □ Pass □ Fail |
| Image Quality | □ Pass □ Fail |
| Detector.log | □ Collected |

---

# Exception Matrix

| Finding | Recommended Action |
|----------|--------------------|
| Communication unstable | Perform network troubleshooting |
| Firmware outdated | Schedule firmware upgrade |
| Calibration abnormal | Execute calibration SOP |
| Image quality degraded | Perform image troubleshooting |
| Physical damage | Evaluate for detector replacement or RMA |

---

# Records

Record:

- Customer Name
- Site
- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Maintenance Date
- Maintenance Engineer
- Detector.log
- Test Images
- Maintenance Result
- Recommendations

---

# Notes

- Preventive maintenance should be completed before major software upgrades whenever possible.
- Preserve maintenance records for trend analysis.
- Repeated abnormalities should trigger further investigation even if current operation is acceptable.
- Any hardware damage should be photographed and attached to the maintenance record.

---

# Related Documents

- SOP/DetectorInstallation
- SOP/Calibration
- SOP/FirmwareUpgrade
- SOP/ImageTroubleshooting
- SOP/DetectorReplacement
- 06_Workflow
- 07_FailureKnowledge
- 09_DecisionTree
- 11_Case
- 12_ErrorCode
- 13_Template
- 14_Glossary

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |