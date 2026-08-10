# Communication Error Code - UDP

> Module: Communication
>
> Category: UDP/Image Transmission Error Codes

---

# Overview

This document covers UDP/image-transmission errors related to packet integrity, packet sequence, packet loss, receive-buffer overflow, frame-buffer overflow, and image delivery timeout.

---

# Protocol Diagnostic Boundary

```text
UDP / Image Transmission Error
        ↓
Preserve original image/RAW + event time
        ↓
Determine: packet integrity / packet loss / host buffer / exposure timeout
        ↓
ImageLoss / AcquisitionTimeout / NetworkFailure
        ↓
Wireshark for packet-level evidence
        ↓
Ping only for basic IP reachability
        ↓
Detector.log + acquisition parameters + host resource evidence
```

A successful Ping does not exclude UDP packet loss, receive-buffer overflow, frame loss, or image transmission failure.

---

# Error Code → Diagnostic Entry

| Error | Primary Entry | Tool / Evidence |
|---|---|---|
| `Err_InvalidPacketNo` | [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) | Wireshark, event time, log |
| `Err_InvalidPacketFormat` | [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) | Wireshark, SDK/FW compatibility, log |
| `Err_PacketDataCheckFailed` | [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) | Wireshark, physical/network evidence |
| `Err_PacketLost_BufOverflow` | [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) | Wireshark, frame rate, host/network state |
| `Err_FrameLost_BufOverflow` | [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md) | Host CPU/memory/storage, acquisition parameters |
| `Evt_WaitImage_Timeout` | [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md) | Exposure + image/network/log evidence |

---

# Error Codes

## Err_InvalidPacketNo

Received an invalid packet sequence number.

### Diagnostic Path

1. Preserve the failure timestamp and acquisition parameters.
2. Check whether the issue is reproducible.
3. Enter [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md).
4. Capture packet evidence with [Wireshark](../../17_Tools/Wireshark/README.md).
5. Correlate packet sequence evidence with `Detector.log`.

---

## Err_InvalidPacketFormat

The received UDP packet format is invalid.

### Diagnostic Path

1. Preserve the original event and packet evidence.
2. Verify SDK, firmware, and detector compatibility before changing network settings.
3. Follow [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md).
4. Use [Wireshark](../../17_Tools/Wireshark/README.md) when packet-level evidence is required.
5. If version mismatch evidence exists, continue to [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md).

---

## Err_PacketDataCheckFailed

UDP packet integrity validation failed.

### Diagnostic Path

1. Verify physical link and network path.
2. Preserve `Detector.log` and failure time.
3. Enter [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md).
4. Capture traffic with [Wireshark](../../17_Tools/Wireshark/README.md).
5. Compare capture evidence before replacing hardware or changing firmware.

---

## Err_PacketLost_BufOverflow

UDP packets were lost because the receive buffer overflowed.

### Diagnostic Path

1. Record acquisition frame rate and image size.
2. Record host CPU/memory and network receive conditions.
3. Use [Wireshark](../../17_Tools/Wireshark/README.md) to distinguish observed packet loss from host-side overload where possible.
4. Enter [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md).
5. Change frame rate or host/network settings only as controlled tests and record results.

---

## Err_FrameLost_BufOverflow

One or more image frames were lost because the frame buffer overflowed.

### Diagnostic Path

1. Record continuous-acquisition frame rate and processing pipeline.
2. Record CPU, memory, storage, and application processing load.
3. Enter [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md).
4. Use [Wireshark](../../17_Tools/Wireshark/README.md) only if network loss is still suspected; do not assume every frame-buffer overflow is a network fault.
5. Preserve the result of one controlled load-reduction test.

---

# Related Events

## Evt_Image

Indicates complete image reception. Missing image events must be correlated with acquisition state, exposure evidence, network evidence, and timeout events.

## Evt_WaitImage_Timeout

The SDK did not receive a complete image within the configured timeout. Follow [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md) and distinguish exposure failure from communication/image-delivery failure.

## Evt_TransactionAborted

Preserve the transaction time and preceding error/event, then select the corresponding network or acquisition branch instead of retrying blindly.

---

# Evidence Package

Collect:

- Exact error/event and timestamp
- Acquisition mode, frame rate, image size
- Exposure evidence where applicable
- Original image/RAW when available
- Ping result only as basic reachability evidence
- Wireshark capture for packet/sequence/integrity issues
- Host CPU, memory, storage evidence for buffer errors
- `Detector.log`
- Result after one controlled retry

---

# Related DecisionTree / SOP / Tool

- [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md)
- [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md)
- [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md)
- [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md)
- [ImageTroubleshooting](../../10_SOP/ImageTroubleshooting.md)
- [NetworkConfiguration](../../10_SOP/NetworkConfiguration.md)
- [Ping](../../17_Tools/Ping/README.md)
- [Wireshark](../../17_Tools/Wireshark/README.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.1 | 2026-08-10 | Added UDP packet/buffer diagnostic branching and protocol evidence boundaries |
| v1.0 | 2026-08-07 | Initial release |