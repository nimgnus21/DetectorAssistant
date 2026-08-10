# SDK Error Code - Network

> Module: SDK
>
> Category: Network Communication Error Codes

---

# Overview

This document describes SDK network communication-related error codes during detector discovery, connection, command/response communication, and communication-device management.

Network errors must be interpreted with physical link state, IP configuration, detector state, `Detector.log`, and—when intermittent loss or timing is suspected—packet evidence.

> **Diagnostic boundary:** a successful Ping only proves basic IP reachability. It does not by itself prove SDK command communication or image transmission is normal.

---

# Related Commands

- `Cmd_Connect`
- `Cmd_Disconnect`

# Related Events

- `Evt_ConnectProcess`
- `Evt_GeneralError`
- `Evt_TaskResult_Failed`
- `Evt_TransactionAborted`

---

# Error Code → Diagnostic Entry

| Error | Primary Entry | Secondary Check | Tool / Evidence |
|---|---|---|---|
| `Err_DetectorRespTimeout` | [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md) | [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) | Ping, Wireshark when intermittent, `Detector.log` |
| `Err_GeneralSocketErr` | [UnableToConnect](../../09_DecisionTree/Connection/UnableToConnect.md) | [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) | Ping, IP configuration, `Detector.log` |
| `Err_CommDeviceNotFound` | [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md) | Local NIC/adapter verification | Adapter state, driver, SDK configuration |
| `Err_CommDeviceOccupied` | [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md) | Session/application cleanup | Connected client/session, `Detector.log` |
| `Err_CommParamNotMatch` | [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) | NetworkConfiguration | Detector/PC IP, subnet, configuration evidence |

---

# Error Codes

## Err_DetectorRespTimeout

Timed out while waiting for detector response.

### Diagnostic Path

1. Record the command/API and failure time.
2. Verify detector power and physical link.
3. Use [Ping](../../17_Tools/Ping/README.md) to establish basic reachability.
4. Enter [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md).
5. If Ping is intermittent or SDK communication remains unstable, continue through [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) and capture traffic with [Wireshark](../../17_Tools/Wireshark/README.md) when appropriate.
6. Export the relevant log interval with [LogExport](../../17_Tools/SDKTool/LogExport.md).

---

## Err_GeneralSocketErr

Failed to establish a socket connection, or an existing connection was disconnected.

### Diagnostic Path

1. Verify Ethernet cable and selected network adapter.
2. Verify detector IP, PC IP, and subnet.
3. Test basic reachability with [Ping](../../17_Tools/Ping/README.md).
4. Follow [UnableToConnect](../../09_DecisionTree/Connection/UnableToConnect.md).
5. If the connection is established but drops intermittently, continue to [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) and collect packet evidence with [Wireshark](../../17_Tools/Wireshark/README.md).
6. Preserve `Detector.log` before repeated reconnect attempts.

---

## Err_CommDeviceNotFound

The configured communication device is not available.

### Diagnostic Path

1. Identify the exact adapter/interface expected by the SDK.
2. Verify that the adapter is enabled and recognized by the operating system.
3. Reconnect any USB-to-Ethernet adapter and verify driver state.
4. Verify SDK communication configuration.
5. Restart the SDK and reconnect through [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md).

---

## Err_CommDeviceOccupied

The communication device or session is occupied.

### Diagnostic Path

1. Identify other detector software, SDK instances, or active sessions.
2. Close the conflicting client through the normal shutdown path.
3. Verify whether a previous connection was released.
4. Enter [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md) when runtime state remains occupied.
5. Preserve logs before restarting the detector if the condition persists.

---

## Err_CommParamNotMatch

Communication parameters do not match the detector or SDK configuration.

### Diagnostic Path

1. Record detector IP, PC IP, subnet mask, and relevant SDK configuration.
2. Compare the values before modifying them.
3. Follow [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) and [NetworkConfiguration](../../10_SOP/NetworkConfiguration.md).
4. Verify the corrected configuration with [Ping](../../17_Tools/Ping/README.md).
5. Reconnect and perform a controlled communication test.

---

# Evidence Package

Collect:

- Exact error code/event and timestamp
- Command/API that failed
- Detector power and link status
- Selected network adapter
- Detector IP, PC IP, subnet, and relevant gateway where used
- Ping result
- Packet capture for intermittent loss/timing issues
- `Detector.log`
- Result after one controlled reconnect

---

# Related DecisionTree / SOP / Tool

- [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md)
- [UnableToConnect](../../09_DecisionTree/Connection/UnableToConnect.md)
- [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md)
- [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md)
- [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md)
- [NetworkConfiguration](../../10_SOP/NetworkConfiguration.md)
- [Ping](../../17_Tools/Ping/README.md)
- [Wireshark](../../17_Tools/Wireshark/README.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.1 | 2026-08-10 | Added direct DecisionTree/SOP/tool mapping and evidence boundaries |
| v1.0 | 2026-08-07 | Initial release |