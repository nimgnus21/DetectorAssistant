# SDK Error Code - Image

> Module: SDK  
> Category: Image Error Codes

---

# Overview

This document describes SDK image-related error codes.

These errors occur during image transmission, image integrity verification, image quality evaluation, image callback processing, and image correction.

---

# Related Commands

- Cmd_StartAcq
- Cmd_StopAcq
- Cmd_ApplyDefectCorrection
- Cmd_SetCorrectOption

---

# Related Events

- Evt_Image
- Evt_TaskResult_Failed
- Evt_WaitImage_Timeout
- Evt_GeneralWarn
- Evt_GeneralError

---

# Error Codes

---

## Err_ImgChBreak

### Description

Image transmission channel was interrupted during acquisition.

### Possible Causes

- Ethernet communication interrupted.
- Detector disconnected unexpectedly.
- Network packet loss.
- Detector restarted during image transmission.
- Network adapter abnormal.

### Recommended Actions

1. Verify detector connection.
2. Check Ethernet cable.
3. Verify Gigabit network status.
4. Restart image acquisition.
5. Reconnect the detector if necessary.

---

## Err_BadImgQuality

### Description

The acquired image quality does not satisfy the SDK quality requirements.

### Possible Causes

- Incorrect exposure parameters.
- Low radiation dose.
- Detector calibration expired.
- Offset template abnormal.
- Gain template abnormal.
- Defect template abnormal.
- Detector hardware abnormal.
- Severe image noise.

### Recommended Actions

1. Verify exposure parameters.
2. Verify detector calibration status.
3. Regenerate calibration templates if necessary.
4. Check detector hardware.
5. Acquire another test image.

---

## Err_CallbackNotFinished

### Description

The previous image callback has not completed.

SDK cannot deliver the next image because the user callback is still executing.

### Possible Causes

- Image callback processing takes too long.
- Callback performs image processing.
- Callback performs disk I/O.
- Callback performs network communication.
- Callback thread blocked.

### Recommended Actions

1. Return from callback immediately.
2. Move image processing to a worker thread.
3. Avoid file operations inside callbacks.
4. Avoid blocking functions inside callbacks.
5. Reduce callback execution time.

---

# Related Events

## Evt_Image

Image received successfully.

The callback parameter points to an **IRayImage** structure.

Applications should:

- Copy required image data immediately.
- Avoid lengthy processing inside the callback.
- Return control to the SDK as soon as possible.

---

## Evt_WaitImage_Timeout

No image was received within the configured timeout.

Possible reasons include:

- No exposure occurred.
- Image transmission interrupted.
- Detector communication timeout.
- Image lost.

---

## Evt_GeneralWarn

General warning.

Image quality warnings may be reported through this event.

Refer to **nParam1** for the warning code.

---

## Evt_GeneralError

General error.

Critical image transmission failures may be reported through this event.

Refer to **nParam1** for the corresponding error code.

---

# Diagnostic Checklist

When image-related errors occur, verify the following:

- Detector status is Ready.
- Exposure completed normally.
- Image callback returns immediately.
- No callback blocking exists.
- Calibration templates are valid.
- Detector.log contains no image exceptions.
- Ethernet communication is stable.
- No packet loss exists.

---

# Related DecisionTree

- 09_DecisionTree/Image/ImageLoss.md
- 09_DecisionTree/Image/ImageNoise.md
- 09_DecisionTree/Image/Ghost.md
- 09_DecisionTree/Image/Offset.md
- 09_DecisionTree/Image/Gain.md
- 09_DecisionTree/Image/Defect.md

---

# Related Case

- 11_Case/Image/ImageLoss.md
- 11_Case/Image/ImageNoise.md
- 11_Case/Image/Ghost.md

---

# Related FailureKnowledge

- 07_FailureKnowledge/ImageFailure/ImageLoss.md
- 07_FailureKnowledge/ImageFailure/ImageNoise.md
- 07_FailureKnowledge/ImageFailure/Ghost.md

---

# Related Log

```
Detector.log
```

Image-related failures should always be analyzed together with Detector.log, original image data, exposure parameters, and detector calibration status.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |
```