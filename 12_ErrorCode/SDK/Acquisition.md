# SDK Error Code - Acquisition

> Module: SDK
>
> Category: Acquisition Error Codes

---

# Overview

This document describes SDK errors and events related to image acquisition, exposure synchronization, task execution, image transmission, and acquisition buffer handling.

Acquisition errors must be interpreted together with the acquisition state, exposure condition, detector communication, original image/RAW evidence where available, and `Detector.log`.

---

# Related Commands

- `Cmd_StartAcq`
- `Cmd_StopAcq`
- `Cmd_ClearAcq`
- `Cmd_ForceDarkContinuousAcq`

# Related Events

- `Evt_Image`
- `Evt_WaitImage_Timeout`
- `Evt_TaskResult_Failed`
- `Evt_TaskResult_Succeed`
- `Evt_AutoTask_Started`
- `Evt_TransactionAborted`

---

# Error Code → Diagnostic Entry

| Error / Event | Primary Diagnostic Entry | Tool / Evidence |
|---|---|---|
| `Err_TaskTimeOut` / `Evt_WaitImage_Timeout` | [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md) | Detector.log, exposure evidence, Ping/Wireshark when communication is suspected |
| `Err_FrameLost_BufOverflow` | [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md) | Host performance, frame rate, memory/disk evidence |
| `Err_PacketLost_BufOverflow` | [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md) | [Wireshark](../../17_Tools/Wireshark/README.md), network evidence |
| `Err_ImgChBreak` | [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md) | Cable/network state, `Detector.log` |
| `Err_BadImgQuality` | [ImageTroubleshooting](../../10_SOP/ImageTroubleshooting.md) | Original image/RAW, [ImageJ](../../17_Tools/ImageJ/README.md), [Offset Viewer](../../17_Tools/Offset%20Viewer/README.md) |
| `Err_CallbackNotFinished` | [SDKException](../../09_DecisionTree/Software/SDKException.md) | Callback/API execution evidence |

---

# Error Codes

## Err_TaskTimeOut

The acquisition task exceeded the allowed execution time.

### Primary Checks

1. Confirm detector state is `Ready` before acquisition.
2. Verify acquisition started successfully.
3. Verify exposure was actually triggered and received.
4. Enter [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md).
5. If communication interruption is indicated, continue to [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md).
6. Export logs with [LogExport](../../17_Tools/SDKTool/LogExport.md).

---

## Err_FrameLost_BufOverflow

Frame data was lost because the acquisition buffer overflowed.

### Primary Checks

1. Record frame rate and acquisition mode.
2. Record host CPU, memory, and storage conditions.
3. Check whether continuous acquisition exceeds host processing capacity.
4. Reduce load only as a controlled test and record the result.
5. Enter [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md).

---

## Err_PacketLost_BufOverflow

Network packets were lost because the receive buffer overflowed.

### Primary Checks

1. Record network configuration and acquisition frame rate.
2. Verify link stability.
3. Capture traffic when packet loss is suspected using [Wireshark](../../17_Tools/Wireshark/README.md).
4. Continue through [NetworkFailure](../../09_DecisionTree/Connection/NetworkFailure.md).
5. Preserve the original capture and `Detector.log` for correlation.

---

## Err_ImgChBreak

Image transmission channel was interrupted.

### Primary Checks

1. Verify whether the detector disconnected or rebooted.
2. Check cable and network adapter state.
3. Enter [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md).
4. Reconnect and run a controlled acquisition test.

---

## Err_BadImgQuality

The acquired image quality does not meet the required standard.

### Primary Checks

1. Preserve the original abnormal image and RAW when available.
2. Enter [ImageTroubleshooting](../../10_SOP/ImageTroubleshooting.md).
3. Compare image characteristics with [ImageJ](../../17_Tools/ImageJ/README.md).
4. If calibration contribution is suspected, review [Offset Viewer](../../17_Tools/Offset%20Viewer/README.md) and the calibration path.
5. Do not regenerate templates before preserving the original evidence.

---

## Err_CallbackNotFinished

The previous image callback has not completed.

### Primary Checks

1. Record the callback/API involved.
2. Check whether callback processing blocks acquisition.
3. Move non-real-time processing outside the callback where applicable.
4. Enter [SDKException](../../09_DecisionTree/Software/SDKException.md).
5. Preserve SDK/application logs for reproduction.

---

# Related Events

## Evt_WaitImage_Timeout

The SDK waited for an image longer than the configured timeout period.

This event is a diagnostic entry, not proof of one specific cause. Check exposure, acquisition state, image delivery, and communication in that order through [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md).

## Evt_TaskResult_Failed / Evt_TransactionAborted

Use `nParam2` as the failure code where applicable, then return to the corresponding error-code entry. Preserve the event time and the related log segment.

---

# Evidence Package

Collect:

- Exact error code/event and timestamp
- Detector state before failure
- Acquisition mode and key parameters
- Exposure evidence
- Original image/RAW when available
- Network state/capture when applicable
- Host resource condition for buffer errors
- `Detector.log`
- Result after one controlled retry

---

# Related SOP / Tool

- [ImageTroubleshooting](../../10_SOP/ImageTroubleshooting.md)
- [NetworkConfiguration](../../10_SOP/NetworkConfiguration.md)
- [ImageJ](../../17_Tools/ImageJ/README.md)
- [Wireshark](../../17_Tools/Wireshark/README.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added error-to-decision/SOP/tool diagnostic mapping and evidence requirements |
| v1.0 | 2026-08-07 | Initial release |