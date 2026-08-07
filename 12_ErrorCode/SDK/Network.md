# SDK Error Code - Network

> Module: SDK
>
> Category: Error Code
>
> Last Updated: 2026-08-07

---

# Overview

This document describes SDK network communication-related error codes.

These errors typically occur during detector discovery, detector connection, network communication, or detector response.

---

# Related Commands

- Cmd_Connect
- Cmd_Disconnect

---

# Related Events

- Evt_ConnectProcess
- Evt_GeneralError
- Evt_TaskResult_Failed
- Evt_TransactionAborted

---

# Error Codes

---

## Err_DetectorRespTimeout

### Description

Timed out while waiting for detector response.

### Possible Causes

- Detector is powered off.
- Detector is disconnected.
- Network communication interrupted.
- Detector firmware is not responding.
- Detector is busy processing another task.

### Recommended Actions

1. Verify detector power.
2. Verify Ethernet connection.
3. Ping the detector.
4. Reconnect the detector.
5. Restart the detector if necessary.

### Related Commands

- Cmd_Connect

### Related Events

- Evt_TaskResult_Failed
- Evt_ConnectProcess

---

## Err_GeneralSocketErr

### Description

Failed to establish a TCP/UDP connection, or an existing connection has been disconnected.

### Possible Causes

- Network cable disconnected.
- Incorrect IP configuration.
- Firewall blocking communication.
- Network interface unavailable.
- Detector disconnected unexpectedly.

### Recommended Actions

1. Verify network cable.
2. Verify IP configuration.
3. Disable firewall temporarily for testing.
4. Restart network adapter.
5. Reconnect detector.

### Related Commands

- Cmd_Connect
- Cmd_Disconnect

### Related Events

- Evt_TaskResult_Failed

---

## Err_CommDeviceNotFound

### Description

Communication device not found.

### Possible Causes

- Incorrect network adapter selected.
- Ethernet adapter disabled.
- Driver not installed.
- USB-Ethernet adapter disconnected.

### Recommended Actions

1. Verify network adapter.
2. Enable Ethernet adapter.
3. Reinstall driver if necessary.
4. Restart SDK.

### Related Commands

- Cmd_Connect

### Related Events

- Evt_TaskResult_Failed

---

## Err_CommDeviceOccupied

### Description

Communication device is occupied.

### Possible Causes

- Another application is using the network interface.
- Detector is already connected by another SDK instance.
- Previous connection was not released correctly.

### Recommended Actions

1. Close other detector software.
2. Disconnect previous session.
3. Restart SDK.
4. Restart detector if necessary.

### Related Commands

- Cmd_Connect
- Cmd_Disconnect

### Related Events

- Evt_TaskResult_Failed

---

## Err_CommParamNotMatch

### Description

Communication parameters such as IP address do not match.

### Possible Causes

- Detector IP incorrect.
- PC IP configuration incorrect.
- Subnet mismatch.
- Configuration file mismatch.

### Recommended Actions

1. Verify detector IP.
2. Verify PC IP.
3. Verify subnet mask.
4. Verify SDK configuration.
5. Restart connection.

### Related Commands

- Cmd_Connect

### Related Events

- Evt_TaskResult_Failed

---

# Diagnostic Checklist

Verify the following items before escalation:

- Detector powered on.
- Ethernet cable connected.
- Network adapter enabled.
- Correct detector IP configured.
- Same subnet between PC and detector.
- Detector responds to Ping.
- Detector.log contains no socket errors.

---

# Related DecisionTree

- 09_DecisionTree/Connection/DetectorOffline.md
- 09_DecisionTree/Connection/ConnectionTimeout.md
- 09_DecisionTree/Connection/NetworkFailure.md

---

# Related Case

- 11_Case/Communication/ConnectionFailed.md
- 11_Case/Communication/NetworkConfiguration.md
- 11_Case/Communication/Timeout.md

---

# Related FailureKnowledge

- 07_FailureKnowledge/SystemFailure/CommunicationTimeout.md
- 07_FailureKnowledge/SoftwareFailure/CommunicationFailure.md

---

# Related Log

```
Detector.log
```

Network-related errors should always be analyzed together with Detector.log and network configuration.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |