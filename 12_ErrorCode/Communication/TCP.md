# Communication Error Code - TCP

> Module: Communication
>
> Category: TCP Error Codes

---

# Overview

This document describes TCP communication-related error codes.

These errors occur during detector connection establishment, command transmission, detector response, and TCP session maintenance.

---

# Related Commands

- Cmd_Connect
- Cmd_Disconnect
- Cmd_Reset

---

# Related Events

- Evt_ConnectProcess
- Evt_TaskResult_Failed
- Evt_GeneralError
- Evt_TransactionAborted

---

# Error Codes

---

## Err_GeneralSocketErr

### Description

Failed to establish a TCP/UDP connection, or an existing connection was unexpectedly disconnected.

### Possible Causes

- Detector is powered off.
- Ethernet cable is disconnected.
- Detector network service is unavailable.
- Firewall blocks communication.
- Network adapter malfunction.
- TCP session disconnected unexpectedly.

### Recommended Actions

1. Verify detector power status.
2. Check Ethernet cable connection.
3. Confirm detector network configuration.
4. Temporarily disable the firewall for testing.
5. Restart the network adapter.
6. Reconnect the detector.

---

## Err_DetectorRespTimeout

### Description

The SDK did not receive a response from the detector within the specified timeout period.

### Possible Causes

- Detector firmware is busy.
- Detector is rebooting.
- Network latency is excessive.
- Detector communication has been interrupted.
- Command execution exceeds the timeout period.

### Recommended Actions

1. Verify detector is online.
2. Confirm detector status is **Ready**.
3. Retry the command.
4. Reconnect the detector.
5. Restart the detector if the problem persists.

---

## Err_DetectorNotFound

### Description

The detector with the specified serial number could not be found during the connection process.

### Possible Causes

- Detector is powered off.
- Detector is disconnected from the network.
- Incorrect detector serial number.
- Detector and PC are located on different network segments.
- Detector IP configuration is incorrect.

### Recommended Actions

1. Verify detector power.
2. Verify Ethernet connection.
3. Confirm detector serial number.
4. Verify detector IP address.
5. Verify PC and detector are on the same subnet.
6. Reconnect the detector.

---

# Related Events

## Evt_ConnectProcess

Reports the progress of detector connection.

When connection fails, this event is usually followed by **Evt_TaskResult_Failed** with one of the TCP-related error codes.

---

## Evt_TaskResult_Failed

Indicates that a TCP communication command failed.

- **nParam1** — Command ID
- **nParam2** — Error Code

---

## Evt_TransactionAborted

Indicates that the current communication transaction has been aborted.

Possible reasons include:

- Connection timeout.
- Detector response timeout.
- Communication interruption.
- Network exception.

---

# Diagnostic Checklist

When TCP communication errors occur, verify the following:

- Detector is powered on.
- Detector status is **Ready**.
- Ethernet cable is connected.
- Detector IP address is correct.
- PC IP configuration is correct.
- TCP port is not blocked.
- Firewall allows detector communication.
- Detector responds to Ping.
- Detector.log contains no socket exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Connection/DetectorOffline.md
- 09_DecisionTree/Connection/ConnectionTimeout.md
- 09_DecisionTree/Software/DetectorNotFound.md

---

# Related Case

- 11_Case/Communication/ConnectionFailed.md
- 11_Case/Communication/NetworkConfiguration.md
- 11_Case/Communication/Timeout.md

---

# Related FailureKnowledge

- 07_FailureKnowledge/SystemFailure/CommunicationFailure.md
- 07_FailureKnowledge/SystemFailure/StartupFailure.md

---

# Related Log

```
Detector.log
```

TCP communication failures should always be analyzed together with the SDK runtime log, detector connection status, network configuration, and detector response status.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |