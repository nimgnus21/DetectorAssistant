# SDK Error Code - License

> Module: SDK
>
> Category: License Error Codes

---

# Overview

This document describes SDK license-related error codes.

The current SDK Programming Reference does **not** define dedicated License error codes.

However, several existing SDK error codes may occur during license verification, authorization loading, or license-dependent operations.

---

# Related Commands

No dedicated License commands are defined in the current SDK Programming Reference.

---

# Related Events

- Evt_GeneralError
- Evt_TaskResult_Failed

---

# Applicable Error Codes

---

## Err_AccessDenied

### Description

The requested operation is not permitted.

During license verification, this error may indicate that the current operation is not authorized.

### Possible Causes

- License authorization failed.
- Current feature is not licensed.
- Permission denied.
- SDK authorization is invalid.

### Recommended Actions

1. Verify the installed license.
2. Confirm the license has not expired.
3. Verify the current detector supports the requested function.
4. Restart the application after updating the license.

---

## Err_NotImplemented

### Description

The requested function is not implemented.

Some advanced SDK functions require firmware or license support.

### Possible Causes

- Current SDK version does not support the feature.
- Detector firmware does not support the feature.
- Licensed function unavailable.

### Recommended Actions

1. Verify SDK version.
2. Verify firmware version.
3. Confirm feature availability.
4. Contact the supplier if feature licensing is required.

---

## Err_PreCondition

### Description

The required preconditions have not been satisfied.

Some licensed functions may require successful detector initialization or specific runtime conditions before execution.

### Possible Causes

- Detector not initialized.
- License-dependent initialization not completed.
- Required configuration missing.

### Recommended Actions

1. Complete SDK initialization.
2. Verify detector status.
3. Retry after initialization.

---

# License Related Notes

According to the current SDK Programming Reference:

- No dedicated License command is defined.
- No dedicated License event is defined.
- No dedicated License error code is defined.

If future SDK versions introduce license management APIs or authorization error codes, this document should be updated accordingly.

---

# Field Experience

In field service, image locking or unavailable acquisition functions may be related to license problems.

Typical troubleshooting steps include:

1. Verify the current license file.
2. Replace the license file if necessary.
3. Restart the SDK.
4. Reconnect the detector.
5. Verify normal image acquisition.

---

# Diagnostic Checklist

Verify the following items:

- Correct license file installed.
- License file not corrupted.
- License file matches the detector.
- Detector initialized successfully.
- SDK version is compatible.
- Detector.log contains no authorization-related exceptions.

---

# Related DecisionTree

- 09_DecisionTree/Software/LicenseFailure.md
- 09_DecisionTree/Software/SDKInitializationFailed.md

---

# Related Case

- 11_Case/Firmware/ParameterRecovery.md

---

# Related Log

```
Detector.log
```

License-related problems should always be analyzed together with Detector.log, SDK version, detector firmware version, and the installed license file.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |