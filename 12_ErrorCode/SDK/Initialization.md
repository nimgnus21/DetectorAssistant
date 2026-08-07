# SDK Error Code - Initialization

> Module: SDK  
> Category: Initialization Error Codes

---

# Overview

This document describes SDK initialization-related error codes.

These errors typically occur during SDK startup, detector object creation, environment initialization, parameter validation, command precondition verification, and SDK runtime state management.

---

# Related Commands

- Cmd_SetLogLevel
- Cmd_Connect
- Cmd_Disconnect
- Cmd_Reset

---

# Related Events

- Evt_GeneralError
- Evt_TaskResult_Failed
- Evt_TaskResult_Succeed

---

# Error Codes

---

## Err_OK

### Description

Operation completed successfully.

### Possible Causes

- The command was executed successfully.
- No error occurred.

### Recommended Actions

No action required.

---

## Err_TaskPending

### Description

A previous task is still executing.

### Possible Causes

- Previous command has not completed.
- Detector is executing another task.
- SDK task queue is occupied.

### Recommended Actions

- Wait for the current task to finish.
- Wait for **Evt_TaskResult_Succeed** or **Evt_TaskResult_Failed**.
- Avoid sending duplicate commands.

---

## Err_Unknown

### Description

Unknown internal error.

### Possible Causes

- Unexpected SDK exception.
- Unexpected detector response.
- Internal software failure.

### Recommended Actions

- Check **Detector.log**.
- Restart the application.
- Reconnect the detector.
- Contact technical support if the issue persists.

---

## Err_DuplicatedCreation

### Description

Failed to create the detector object or working directory because it already exists.

### Possible Causes

- Detector object has already been created.
- SDK initialized multiple times.
- Working directory already exists.

### Recommended Actions

- Prevent duplicate SDK initialization.
- Release the previous detector object before creating a new one.
- Verify application initialization logic.

---

## Err_StateErr

### Description

Current detector state does not allow the requested operation.

### Possible Causes

- Detector is not in the required state.
- Detector is Busy.
- Operation sequence is incorrect.

### Recommended Actions

- Verify current detector state.
- Wait until the detector returns to **Ready**.
- Retry the operation.

---

## Err_NotInitialized

### Description

SDK or detector has not been initialized.

### Possible Causes

- SDK initialization failed.
- Cmd_Connect has not been executed.
- Detector object has not been created.

### Recommended Actions

- Initialize the SDK.
- Create the detector object.
- Execute Cmd_Connect before other commands.

---

## Err_NotImplemented

### Description

The requested function is not implemented.

### Possible Causes

- Current SDK version does not support the command.
- Detector firmware does not support the feature.

### Recommended Actions

- Verify SDK version.
- Verify firmware version.
- Use supported APIs only.

---

## Err_AccessDenied

### Description

Interface operation is not permitted.

### Possible Causes

- Current detector state prohibits the operation.
- Command execution permission denied.
- Detector is occupied by another task.

### Recommended Actions

- Verify detector status.
- Wait until current task completes.
- Retry the operation.

---

## Err_InvalidParamCount

### Description

Invalid number of parameters.

### Possible Causes

- Missing required parameters.
- Too many parameters supplied.

### Recommended Actions

- Verify API parameter count.
- Follow the SDK Programming Guide.

---

## Err_InvalidParamType

### Description

Invalid parameter type.

### Possible Causes

- Incorrect data type supplied.
- Unsupported parameter type.

### Recommended Actions

- Verify parameter type definition.
- Use the correct SDK data type.

---

## Err_InvalidParamValue

### Description

Invalid parameter value.

### Possible Causes

- Parameter exceeds valid range.
- Invalid enumeration value.
- Invalid configuration value.

### Recommended Actions

- Verify parameter range.
- Use valid enumeration values.
- Check SDK Programming Guide.

---

## Err_PreCondition

### Description

The command precondition has not been satisfied.

### Possible Causes

- Required initialization has not completed.
- Detector is not in the required state.
- Mandatory parameters have not been configured.

### Recommended Actions

- Complete prerequisite operations.
- Verify command execution sequence.
- Retry after initialization.

---

# Diagnostic Checklist

When initialization-related errors occur, verify the following:

- SDK initialized successfully.
- Detector object created successfully.
- Detector state is **Ready**.
- No previous task is pending.
- Required parameters are configured correctly.
- Detector.log is generated normally.

---

# Related DecisionTree

- 09_DecisionTree/Software/SDKInitializationFailed.md
- 09_DecisionTree/Software/SDKException.md
- 09_DecisionTree/Software/DetectorBusy.md

---

# Related Case

- 11_Case/Communication/ConnectionFailed.md

---

# Related Log

```
Detector.log
```

Initialization-related problems should always be analyzed together with the SDK runtime log.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |