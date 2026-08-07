# Detector Status

> iDetector Detector Status

---

# 1. Purpose

The **Detector Status** page provides real-time operational status information for the currently selected detector.

It allows engineers to monitor the detector's operating condition, communication status, power status, and system health before, during, and after engineering operations. The status information serves as an important reference for troubleshooting and operational verification.

---

# 2. Scope

This document describes the detector status functions provided by the **Detector** page of the iDetector software.

Typical functions include:

- Monitoring detector status
- Viewing communication status
- Viewing operating status
- Monitoring detector readiness
- Identifying abnormal conditions

The actual status items displayed depend on the detector model, communication mode, firmware version, and iDetector software version.

---

# 3. Functional Description

The Detector Status page continuously displays the current operating condition of the connected detector.

Typical information may include:

- Connection Status
- Detector Status
- Communication Status
- Detector Ready Status
- Exposure Status
- Calibration Status
- Firmware Status
- Battery Status (Wireless Models)
- Charging Status (Wireless Models)
- Network Status (Wireless Models)

The displayed information may differ between detector models.

---

# 4. Engineering Applications

The Detector Status page is commonly used for:

- Verifying detector readiness before image acquisition
- Monitoring detector operating condition
- Confirming successful detector connection
- Checking detector status after firmware upgrade
- Verifying detector status after calibration
- Monitoring detector during engineering testing
- Diagnosing detector communication problems

---

# 5. Typical Workflow

```text
Launch iDetector

↓

Connect Detector

↓

Open Detector Status

↓

Verify Detector Ready Status

↓

Confirm Communication Status

↓

Monitor Detector Status

↓

Perform Engineering Operation

↓

Observe Status Changes
```

---

# 6. Typical Status Categories

The software may display various detector states during operation.

Typical categories include:

### Communication Status

- Connected
- Disconnected
- Reconnecting
- Communication Error

---

### Operating Status

- Idle
- Ready
- Busy
- Acquiring Image
- Calibrating
- Upgrading Firmware

---

### Detector Health

- Normal
- Warning
- Error

---

### Power Status

(Wireless models)

- Battery Normal
- Battery Low
- Charging
- Fully Charged

---

The actual status names shall follow the corresponding iDetector software version.

---

# 7. Engineering Verification Checklist

Before beginning engineering operations, verify:

- Detector is online.
- Communication is stable.
- Detector status is **Ready**.
- No firmware upgrade is in progress.
- No calibration task is running.
- No communication errors are present.
- Battery level is sufficient (wireless models).

---

# 8. Common Engineering Scenarios

Typical scenarios include:

- Detector installation
- Customer acceptance testing
- Image acquisition preparation
- Calibration verification
- Firmware upgrade verification
- Remote technical support
- Detector troubleshooting
- Preventive maintenance

---

# 9. Common Issues

Typical detector status abnormalities include:

- Detector remains Offline
- Detector not Ready
- Detector Busy
- Status not updating
- Communication interrupted
- Battery warning
- Detector enters Error state
- Detector status inconsistent with actual operation

Refer to the corresponding Failure Knowledge and Decision Tree documents for troubleshooting procedures.

---

# 10. Best Practices

Engineers are recommended to:

- Verify detector status before every image acquisition.
- Monitor status during calibration and firmware upgrade.
- Do not interrupt detector operation while the detector is Busy.
- Record abnormal detector states together with software logs.
- Confirm detector returns to the Ready state after engineering operations.

---

# 11. Related Documents

### Software Module

- README.md
- DeviceList.md
- DetectorInformation.md
- DetectorConnection.md
- DetectorConfiguration.md
- DetectorActivation.md

### Knowledge Base

- ../../03_Hardware
- ../../06_Workflow
- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../10_SOP
- ../../11_Case
- ../../12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Detector Status documentation |