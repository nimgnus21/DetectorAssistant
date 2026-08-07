# Communication Error Code - UDP

> Module: Communication
>
> Category: UDP Error Codes

---

# Overview

This document describes UDP communication-related error codes.

UDP communication is primarily used for detector image transmission. These errors are generally related to packet integrity, packet sequence, network quality, buffer management, and image transmission reliability.

---

# Related Commands

- Cmd_StartAcq
- Cmd_StopAcq
- Cmd_ClearAcq

---

# Related Events

- Evt_Image
- Evt_WaitImage_Timeout
- Evt_TaskResult_Failed
- Evt_GeneralError
- Evt_TransactionAborted

---

# Error Codes

---

## Err_InvalidPacketNo

### Description

Received an invalid packet sequence number.

### Possible Causes

- Packet sequence disorder.
- Packet duplication.
- Packet loss during transmission.
- Detector communication interrupted.

### Recommended Actions

1. Verify network stability.
2. Restart image acquisition.
3. Reconnect the detector if necessary.
4. Check Detector.log for abnormal packet sequence.

---

## Err_InvalidPacketFormat

### Description

The received UDP packet format is invalid.

### Possible Causes

- Packet header corrupted.
- Unsupported protocol version.
- Incomplete packet transmission.
- Communication protocol mismatch.

### Recommended Actions

1. Verify SDK and firmware compatibility.
2. Restart detector communication.
3. Upgrade firmware if necessary.
4. Verify network integrity.

---

## Err_PacketDataCheckFailed

### Description

UDP packet integrity verification failed.

The received packet failed checksum or data validation.

### Possible Causes

- Packet corruption during transmission.
- Network interference.
- Hardware communication abnormality.
- Invalid packet payload.

### Recommended Actions

1. Check Ethernet connection.
2. Verify network quality.
3. Restart acquisition.
4. Capture network packets for further analysis if necessary.

---

## Err_PacketLost_BufOverflow

### Description

UDP packets were lost because the receive buffer overflowed.

### Possible Causes

- Image transmission rate too high.
- Host computer processing speed insufficient.
- CPU usage too high.
- Network receive buffer too small.

### Recommended Actions

1. Reduce acquisition frame rate.
2. Close unnecessary applications.
3. Improve host computer performance.
4. Verify Gigabit Ethernet connection.

---

## Err_FrameLost_BufOverflow

### Description

One or more image frames were lost because the frame buffer overflowed.

### Possible Causes

- Continuous acquisition speed too high.
- Image processing slower than acquisition speed.
- Memory resources insufficient.
- Disk writing performance insufficient.

### Recommended Actions

1. Reduce acquisition frame rate.
2. Save images to SSD.
3. Increase available system memory.
4. Move image processing to a background thread.

---

# Related Events

## Evt_Image

Indicates that a complete image has been received successfully.

Failure to receive this event may indicate:

- Packet loss.
- Frame loss.
- Communication interruption.

---

## Evt_WaitImage_Timeout

The SDK did not receive a complete image within the configured timeout period.

Possible reasons include:

- UDP packet loss.
- Exposure not triggered.
- Detector communication interrupted.
- Network congestion.

---

## Evt_TransactionAborted

The current image transmission transaction has been aborted.

Possible causes include:

- Communication timeout.
- Packet verification failure.
- Detector communication interruption.

---

# Diagnostic Checklist

When UDP communication errors occur, verify the following:

- Detector status is **Ready**.
- Gigabit Ethernet connection is normal.
- No excessive network latency.
- No packet loss.
- No switch or router abnormalities.
- Host computer performance is sufficient.
- Detector.log contains no packet-related exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Image/ImageLoss.md
- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Connection/NetworkFailure.md

---

# Related Case

- 11_Case/Communication/ImageLoss.md
- 11_Case/Communication/Timeout.md

---

# Related FailureKnowledge

- 07_FailureKnowledge/SystemFailure/CommunicationFailure.md
- 07_FailureKnowledge/ImageFailure/ImageLoss.md

---

# Related Log

```
Detector.log
```

UDP communication failures should always be analyzed together with Detector.log, network quality, acquisition parameters, and image transmission status.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |