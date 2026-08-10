# Communication Error Code - Ethernet

> Module: Communication
>
> Category: Ethernet Error Codes

---

# Overview

This document covers errors related to the local Ethernet interface, communication-device selection, and network parameter configuration before or during detector communication.

---

# Protocol Diagnostic Boundary

```text
Ethernet Adapter / Link / IP Configuration Error
        ↓
Physical and OS Adapter Verification
        ↓
Ping: basic IP reachability
        ↓
NetworkConfiguration / NetworkFailure
        ↓
Wireshark only when intermittent packet-level evidence is needed
        ↓
Detector.log + configuration evidence
```

A successful Ping does not prove TCP command communication or image transmission is normal.

---

# Error Code → Diagnostic Entry

| Error | Primary Entry | Tool | Evidence |
|---|---|---|---|
| `Err_CommDeviceNotFound` | [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md) | [Ping](../../17_Tools/Ping/README.md) after adapter recovery | Adapter/driver state, selected interface, log |
| `Err_CommDeviceOccupied` | [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md) | [Log Viewer](../../17_Tools/Log%20Viewer/README.md) | Active client/session, runtime log |
| `Err_CommParamNotMatch` | [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) | [Ping](../../17_Tools/Ping/README.md) | Detector/PC IP, subnet, configuration |

---

# Error Codes

## Err_CommDeviceNotFound

The SDK cannot find the specified communication device.

### Diagnostic Path

1. Identify the expected Ethernet adapter.
2. Verify the adapter is enabled and recognized by the operating system.
3. Verify driver state and reconnect external USB-Ethernet hardware where applicable.
4. Restart the adapter only after recording its state.
5. Verify basic detector reachability with [Ping](../../17_Tools/Ping/README.md) after adapter recovery.
6. Continue through [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md).

---

## Err_CommDeviceOccupied

The communication device or interface is occupied.

### Diagnostic Path

1. Identify other detector software or SDK instances.
2. Close conflicting clients using the normal shutdown path.
3. Verify the previous connection was released.
4. Follow [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md) if runtime state remains occupied.
5. Preserve relevant evidence using [Log Viewer](../../17_Tools/Log%20Viewer/README.md) or [LogExport](../../17_Tools/SDKTool/LogExport.md).

---

## Err_CommParamNotMatch

Communication parameters do not match the detector configuration.

### Diagnostic Path

1. Record detector IP, PC IP, subnet mask, and SDK network configuration.
2. Compare values before changing them.
3. Correct the configuration through [NetworkConfiguration](../../10_SOP/NetworkConfiguration.md).
4. Verify reachability with [Ping](../../17_Tools/Ping/README.md).
5. If instability remains, enter [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md).

---

# Evidence Package

Collect:

- Exact error/event and timestamp
- Adapter/interface name
- Adapter enable/driver state
- Detector IP, PC IP, subnet, and relevant configuration
- Ping result
- `Detector.log`
- Result after one controlled reconnect

---

# Related DecisionTree / SOP / Tool

- [DetectorOffline](../../09_DecisionTree/Connection/DetectorOffline.md)
- [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md)
- [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md)
- [NetworkConfiguration](../../10_SOP/NetworkConfiguration.md)
- [Ping](../../17_Tools/Ping/README.md)
- [Log Viewer](../../17_Tools/Log%20Viewer/README.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.1 | 2026-08-10 | Added protocol-level DecisionTree/tool/evidence mapping |
| v1.0 | 2026-08-07 | Initial release |