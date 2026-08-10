# Communication Error Code - TCP

> Module: Communication
>
> Category: TCP Error Codes

---

# Overview

This document covers TCP/session-level errors during detector connection establishment, command transmission, detector response, and session maintenance.

---

# Protocol Diagnostic Boundary

```text
TCP Error
   ↓
Physical link + IP reachability
   ↓
Ping: basic IP reachability only
   ↓
Connection DecisionTree
   ↓
Wireshark when TCP/session timing or disconnect evidence is required
   ↓
Detector.log + event timestamp
```

Ping success does not prove the required TCP service, port, SDK session, or detector command path is healthy.

---

# Error Code → Diagnostic Entry

| Error | Primary Entry | Tool | Evidence |
|---|---|---|---|
| `Err_GeneralSocketErr` | [UnableToConnect](../../09_DecisionTree/Connection/UnableToConnect.md) | Ping → Wireshark if session fails | IP/subnet, socket event, log |
| `Err_DetectorRespTimeout` | [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md) | Ping + Wireshark when intermittent | Command/API, timing, response/log |
| `Err_DetectorNotFound` | [DetectorNotFound](../../09_DecisionTree/Software/DetectorNotFound.md) / [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md) | Ping | Detector identity, IP, power/link |

---

# Error Codes

## Err_GeneralSocketErr

Failed to establish a socket connection, or an existing TCP/UDP connection disconnected unexpectedly.

### Diagnostic Path

1. Record the failing command and timestamp.
2. Verify detector power, link, IP configuration, and subnet.
3. Test basic reachability with [Ping](../../17_Tools/Ping/README.md).
4. Follow [UnableToConnect](../../09_DecisionTree/Connection/UnableToConnect.md).
5. If the connection is reachable but session establishment/disconnect remains abnormal, capture traffic with [Wireshark](../../17_Tools/Wireshark/README.md).
6. Correlate the capture with `Detector.log` using the same failure time.

---

## Err_DetectorRespTimeout

The SDK did not receive a detector response within the configured timeout.

### Diagnostic Path

1. Record the command/API and timeout time.
2. Verify detector state before retry.
3. Use [Ping](../../17_Tools/Ping/README.md) to establish basic reachability.
4. Enter [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md).
5. If Ping is normal but command responses time out, collect TCP/session evidence with [Wireshark](../../17_Tools/Wireshark/README.md).
6. Preserve the related `Detector.log` interval.

---

## Err_DetectorNotFound

The detector with the requested identity could not be found during connection.

### Diagnostic Path

1. Verify detector power and Ethernet link.
2. Verify the requested detector identity and connection configuration.
3. Verify detector/PC network reachability with [Ping](../../17_Tools/Ping/README.md) where the detector IP is known.
4. Follow [DetectorNotFound](../../09_DecisionTree/Software/DetectorNotFound.md) or [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md) according to whether identity/configuration or network availability is the primary symptom.

---

# Related Events

## Evt_ConnectProcess

Reports connection progress. On failure, preserve the progress stage and subsequent failure code.

## Evt_TaskResult_Failed

Use the command ID and error code together to select the diagnostic branch. Do not diagnose from the event name alone.

## Evt_TransactionAborted

Preserve transaction time and preceding events, then check timeout, response, and communication evidence before reconnecting repeatedly.

---

# Evidence Package

Collect:

- Exact error/event and timestamp
- Command/API and connection stage
- Detector power/link state
- Detector IP, PC IP, subnet
- Ping result
- Wireshark capture when session-level failure persists
- `Detector.log`
- Result after one controlled reconnect

---

# Related DecisionTree / SOP / Tool

- [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md)
- [UnableToConnect](../../09_DecisionTree/Connection/UnableToConnect.md)
- [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md)
- [DetectorNotFound](../../09_DecisionTree/Software/DetectorNotFound.md)
- [NetworkConfiguration](../../10_SOP/NetworkConfiguration.md)
- [Ping](../../17_Tools/Ping/README.md)
- [Wireshark](../../17_Tools/Wireshark/README.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.1 | 2026-08-10 | Added TCP-level decision/tool/evidence chain and Ping boundary |
| v1.0 | 2026-08-07 | Initial release |