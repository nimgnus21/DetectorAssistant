# Detector Connection

> iDetector Detector Connection

---

# 1. Purpose

The **Detector Connection** page is responsible for establishing, maintaining, and terminating communication between the iDetector software and the detector.

A successful detector connection is the prerequisite for all subsequent operations, including image acquisition, calibration, firmware upgrade, and detector diagnostics.

---

# 2. Scope

This document describes the detector connection functions provided by the **Detector** page of the iDetector software.

Typical functions include:

- Connecting to a detector
- Disconnecting from a detector
- Monitoring connection status
- Reconnecting to a detector
- Verifying communication availability

The available functions depend on the detector model, communication mode, and iDetector software version.

---

# 3. Functional Description

The Detector Connection page is responsible for establishing communication between the host computer and the selected detector.

Typical operations include:

- Selecting a detector
- Initiating a connection
- Disconnecting an active connection
- Reconnecting after communication interruption
- Monitoring connection state

A successful connection enables all detector-related operations within the software.

---

# 4. Connection Prerequisites

Before connecting to a detector, verify:

- The detector is powered on.
- The detector is available in the Device List.
- Network or communication settings are correct.
- The detector is not occupied by another application.
- The required SDK components are functioning normally.

---

# 5. Typical Workflow

```text
Launch iDetector

↓

Open Detector Page

↓

Select Detector

↓

Connect Detector

↓

Verify Connection Status

↓

Confirm Detector Information

↓

Ready for Image Acquisition
```

---

# 6. Engineering Applications

Typical engineering scenarios include:

- Initial detector installation
- Daily detector operation
- Reconnecting after detector restart
- Network recovery
- SDK communication verification
- Customer site troubleshooting
- Detector replacement verification

---

# 7. Connection Status

Typical detector connection states include:

- Not Connected
- Connecting
- Connected
- Connection Lost
- Reconnecting
- Connection Failed

The exact status names displayed by the software shall follow the corresponding iDetector version.

---

# 8. Common Issues

Typical connection-related issues include:

- Detector cannot be connected
- Connection timeout
- Detector offline
- SDK initialization failure
- Network communication failure
- Detector occupied by another application
- Connection interrupted during operation

Refer to the corresponding Failure Knowledge and Decision Tree documents for troubleshooting procedures.

---

# 9. Best Practices

To ensure reliable communication:

- Verify detector power before connecting.
- Confirm network configuration before troubleshooting.
- Avoid disconnecting the detector during image acquisition or calibration.
- Disconnect the detector properly before shutting down the software when required.
- Record abnormal connection events for technical support.

---

# 10. Related Documents

### Software Module

- README.md
- DeviceList.md
- DetectorInformation.md
- DetectorStatus.md
- DetectorConfiguration.md
- DetectorActivation.md

### Knowledge Base

- 02_SDK
- 03_Hardware
- 06_Workflow
- 07_FailureKnowledge
- 09_DecisionTree
- 10_SOP
- 11_Case
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Detector Connection documentation |