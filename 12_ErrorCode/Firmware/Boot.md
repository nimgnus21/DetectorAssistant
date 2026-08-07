# Firmware Error Code - Boot

> Module: Firmware
>
> Category: Boot Error Codes

---

# Overview

This document describes firmware boot-related error codes.

These errors occur during detector startup, firmware initialization, bootloader execution, and the establishment of communication between the detector and the SDK.

Boot failures usually prevent the detector from entering the **Ready** state, making subsequent operations such as image acquisition, parameter configuration, and calibration unavailable.

---

# Related Commands

- Cmd_Connect
- Cmd_Reset

---

# Related Events

- Evt_ConnectProcess
- Evt_GeneralError
- Evt_TaskResult_Failed

---

# Error Codes

---

## Err_FPD_General_Detector_Error

### Description

A general detector error occurred during firmware startup or initialization.

### Possible Causes

- Firmware initialization failed.
- Internal hardware self-test failed.
- Detector firmware exception.
- Detector failed to enter the Ready state.

### Recommended Actions

1. Restart the detector.
2. Reconnect the detector.
3. Check Detector.log.
4. Verify firmware version.
5. Contact technical support if the problem persists.

---

## Err_FPD_FirmwareFallback

### Description

The detector automatically rolled back to the previous firmware version during startup.

The SDK reports this event through **Evt_GeneralError** after the detector reconnects.

### Possible Causes

- Firmware verification failed.
- Startup self-test failed.
- Firmware image corrupted.
- Upgrade interrupted.

### Recommended Actions

1. Verify firmware version.
2. Re-upgrade the firmware.
3. Ensure firmware package matches the detector model.
4. Review Detector.log.

---

## Err_DetectorRespTimeout

### Description

The detector failed to respond during the boot or connection process.

### Possible Causes

- Detector startup not completed.
- Firmware initialization still in progress.
- Detector communication abnormal.
- Network interruption.

### Recommended Actions

1. Wait until detector startup completes.
2. Retry the connection.
3. Restart the detector.
4. Verify network communication.

---

# Boot Process

```
Power On

↓

BootLoader

↓

Firmware Initialization

↓

Hardware Self-Test

↓

Network Initialization

↓

SDK Connection

↓

Ready
```

Any interruption during the above sequence may prevent the detector from entering the **Ready** state.

---

# Diagnostic Checklist

Before determining a boot failure, verify:

- Detector power supply is stable.
- Status indicator behaves normally.
- Ethernet link is established.
- Detector responds to Ping.
- Firmware version is correct.
- Detector successfully enters the **Ready** state.
- Detector.log contains no startup exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Connection/DetectorOffline.md
- 09_DecisionTree/Software/DetectorNotFound.md
- 09_DecisionTree/Firmware/VersionMismatch.md

---

# Related Case

- 11_Case/Communication/ConnectionFailed.md
- 11_Case/Firmware/VersionMismatch.md

---

# Related Workflow

- 06_Workflow/PowerOnWorkflow.md
- 06_Workflow/CommunicationWorkflow.md

---

# Related Log

```
Detector.log
```

Boot-related failures should always be analyzed together with Detector.log, firmware version, detector status indicators, and network connection status.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |