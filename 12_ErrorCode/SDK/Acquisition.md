# SDK Error Code - Acquisition

> Module: SDK  
> Category: Acquisition Error Codes

---

# Overview

This document describes SDK acquisition-related error codes.

These errors occur during image acquisition, exposure synchronization, task execution, image transmission, or acquisition buffer management.

---

# Related Commands

- Cmd_StartAcq
- Cmd_StopAcq
- Cmd_ClearAcq
- Cmd_ForceDarkContinuousAcq

---

# Related Events

- Evt_Image
- Evt_WaitImage_Timeout
- Evt_TaskResult_Failed
- Evt_TaskResult_Succeed
- Evt_AutoTask_Started
- Evt_TransactionAborted

---

# Error Codes

---

## Err_TaskTimeOut

### Description

The acquisition task exceeded the allowed execution time.

### Possible Causes

- Detector did not receive an exposure.
- Exposure synchronization failed.
- Detector communication delayed.
- Detector stopped responding during acquisition.

### Recommended Actions

- Verify exposure conditions.
- Verify detector communication.
- Restart acquisition.
- Check Detector.log.

---

## Err_FrameLost_BufOverflow

### Description

Frame data was lost because the acquisition buffer overflowed.

### Possible Causes

- Host computer could not process incoming images fast enough.
- Continuous acquisition frame rate too high.
- System memory resources insufficient.
- Disk writing speed too slow.

### Recommended Actions

- Reduce acquisition frame rate.
- Stop unnecessary applications.
- Use SSD storage.
- Increase available memory.

---

## Err_PacketLost_BufOverflow

### Description

Network packets were lost because the receive buffer overflowed.

### Possible Causes

- Network throughput exceeded processing capability.
- Gigabit network congestion.
- CPU usage too high.
- Packet processing delayed.

### Recommended Actions

- Verify Gigabit Ethernet connection.
- Reduce network load.
- Restart acquisition.
- Check network performance.

---

## Err_ImgChBreak

### Description

Image transmission channel was interrupted.

### Possible Causes

- Network disconnected during acquisition.
- Detector communication interrupted.
- Detector rebooted unexpectedly.
- Communication timeout.

### Recommended Actions

- Verify detector connection.
- Check Ethernet cable.
- Reconnect detector.
- Restart acquisition.

---

## Err_BadImgQuality

### Description

The acquired image quality does not meet the required standard.

### Possible Causes

- Incorrect exposure parameters.
- Detector calibration invalid.
- Excessive image noise.
- Detector hardware abnormality.

### Recommended Actions

- Verify exposure settings.
- Regenerate calibration templates if necessary.
- Check detector status.
- Review image quality.

---

## Err_CallbackNotFinished

### Description

The previous image callback has not completed.

### Possible Causes

- User callback function blocked.
- Image processing takes too long.
- Callback thread occupied.

### Recommended Actions

- Reduce callback processing time.
- Move image processing to a worker thread.
- Return from callback as quickly as possible.

---

# Related Events

The following SDK events are closely related to acquisition:

## Evt_Image

Image received successfully.

---

## Evt_WaitImage_Timeout

The SDK waited for an image longer than the configured timeout period.

This event usually indicates:

- Exposure was not triggered.
- Image was lost.
- Detector communication interrupted.

---

## Evt_AutoTask_Started

An internal acquisition task started automatically.

Common scenarios include:

- AED acquisition.
- External trigger acquisition.
- Automatic acquisition sequence.

---

## Evt_TaskResult_Failed

Acquisition task failed.

Refer to **nParam2** for the corresponding SDK error code.

---

## Evt_TransactionAborted

The current acquisition transaction was aborted.

Refer to **nParam2** for the failure reason.

---

# Diagnostic Checklist

When acquisition-related errors occur, verify the following:

- Detector status is **Ready**.
- Acquisition started successfully.
- Exposure was triggered.
- Detector received X-ray exposure.
- Ethernet communication is stable.
- No packet loss.
- Host PC performance is sufficient.
- Detector.log contains no acquisition exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Software/DetectorBusy.md
- 09_DecisionTree/Image/ImageLoss.md

---

# Related Case

- 11_Case/Communication/Timeout.md
- 11_Case/Communication/ImageLoss.md

---

# Related Log

```
Detector.log
```

Acquisition-related failures should always be analyzed together with Detector.log, acquisition parameters, exposure conditions, and network status.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |