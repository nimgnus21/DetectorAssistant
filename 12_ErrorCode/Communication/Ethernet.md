# Communication Error Code - Ethernet

> Module: Communication
>
> Category: Ethernet Error Codes

---

# Overview

This document describes Ethernet communication-related error codes.

These errors occur before or during detector communication and are primarily related to the local Ethernet interface, communication device selection, and network parameter configuration.

---

# Related Commands

- Cmd_Connect
- Cmd_Disconnect

---

# Related Events

- Evt_ConnectProcess
- Evt_TaskResult_Failed
- Evt_GeneralError

---

# Error Codes

---

## Err_CommDeviceNotFound

### Description

The SDK cannot find the specified communication device.

### Possible Causes

- Ethernet adapter is disabled.
- Ethernet driver is not installed correctly.
- USB-to-Ethernet adapter is disconnected.
- Incorrect communication interface selected.
- Network adapter failed to initialize.

### Recommended Actions

1. Verify that the Ethernet adapter is enabled.
2. Check Device Manager for abnormal devices.
3. Reconnect the USB-to-Ethernet adapter if used.
4. Restart the network adapter.
5. Restart the SDK and reconnect the detector.

---

## Err_CommDeviceOccupied

### Description

The communication device is currently occupied.

### Possible Causes

- Another application is using the communication interface.
- Another SDK instance is connected to the detector.
- Previous connection was not released correctly.
- Detector communication service has not exited normally.

### Recommended Actions

1. Close all detector-related applications.
2. Disconnect the previous detector connection.
3. Restart the SDK.
4. Restart the detector if necessary.

---

## Err_CommParamNotMatch

### Description

Communication parameters do not match the detector configuration.

Typical mismatched parameters include:

- IP Address
- Subnet Mask
- Network Configuration

### Possible Causes

- Incorrect detector IP configuration.
- Incorrect PC network configuration.
- Detector and PC are on different subnets.
- Incorrect SDK configuration file.
- Detector network parameters have been modified.

### Recommended Actions

1. Verify detector IP address.
2. Verify PC IP address.
3. Confirm both devices are on the same subnet.
4. Verify SDK working directory configuration.
5. Reconnect the detector.

---

# Diagnostic Checklist

When Ethernet communication errors occur, verify the following:

- Ethernet cable connected correctly.
- Detector powered on.
- Network adapter enabled.
- Network adapter driver installed correctly.
- Detector IP configuration correct.
- PC IP configuration correct.
- Same subnet between PC and detector.
- No IP address conflict.
- Detector responds to Ping.
- Detector.log contains no communication exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Connection/DetectorOffline.md
- 09_DecisionTree/Connection/ConnectionTimeout.md
- 09_DecisionTree/Connection/NetworkFailure.md

---

# Related Case

- 11_Case/Communication/ConnectionFailed.md
- 11_Case/Communication/NetworkConfiguration.md

---

# Related FailureKnowledge

- 07_FailureKnowledge/SystemFailure/CommunicationFailure.md

---

# Related Log

```
Detector.log
```

Ethernet communication failures should always be analyzed together with the SDK runtime log, detector network configuration, and PC network configuration.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |