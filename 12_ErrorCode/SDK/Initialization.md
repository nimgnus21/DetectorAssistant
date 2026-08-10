# SDK Error Code - Initialization

> Module: SDK
>
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

# Related Events

- Evt_GeneralError
- Evt_TaskResult_Failed
- Evt_TaskResult_Succeed

---

# Diagnostic Rule

For every initialization error, first record the exact command, detector state, SDK version, firmware version and Detector.log timestamp. The error code indicates the failing condition; it does not by itself prove a unique root cause.

---

# Error Codes

## Err_OK

### Description

Operation completed successfully.

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

### Diagnostic Chain

- DecisionTree: [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md)
- SOP: [Workflow Troubleshooting](../../06_Workflow/WorkflowTroubleshooting.md)
- Tool: [iDetector Quick Troubleshooting](../../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)
- Evidence: Detector.log, triggering command, detector state and task timing.

---

## Err_Unknown

### Description

Unknown internal error.

### Possible Causes

- Unexpected SDK exception.
- Unexpected detector response.
- Internal software failure.

### Recommended Actions

- Preserve Detector.log before restart.
- Restart the application.
- Reconnect the detector.
- Escalate with version information if the issue persists.

### Diagnostic Chain

- DecisionTree: [SDK Exception](../../09_DecisionTree/Software/SDKException.md)
- SOP: [Workflow Troubleshooting](../../06_Workflow/WorkflowTroubleshooting.md)
- Tool: [Log Viewer](../../17_Tools/Log%20Viewer/README.md)
- Evidence: Detector.log and exact reproduction steps.

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

### Diagnostic Chain

- DecisionTree: [SDK Initialization Failed](../../09_DecisionTree/Software/SDKInitializationFailed.md)
- SOP: [Workflow Troubleshooting](../../06_Workflow/WorkflowTroubleshooting.md)
- Tool: [iDetector Quick Troubleshooting](../../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)

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
- Retry the operation only after state recovery.

### Diagnostic Chain

- DecisionTree: [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md)
- Tool: [iDetector Quick Troubleshooting](../../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)
- Evidence: state before command and preceding command sequence.

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
- Execute Cmd_Connect before dependent commands.

### Diagnostic Chain

- DecisionTree: [SDK Initialization Failed](../../09_DecisionTree/Software/SDKInitializationFailed.md)
- Workflow: [Communication Workflow](../../06_Workflow/CommunicationWorkflow.md)
- Tool: [iDetector Quick Troubleshooting](../../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)

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

### Evidence

- Exact API or command.
- SDK version.
- Firmware version.
- Detector model.

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
- Retry only after the blocking condition is removed.

### Diagnostic Chain

- DecisionTree: [DetectorBusy](../../09_DecisionTree/Software/DetectorBusy.md)
- Tool: [iDetector Quick Troubleshooting](../../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)

---

## Err_InvalidParamCount

### Description

Invalid number of parameters.

### Recommended Actions

- Verify API parameter count.
- Follow the SDK Programming Guide.

### Evidence

- API name.
- Parameter list.
- SDK version.

---

## Err_InvalidParamType

### Description

Invalid parameter type.

### Recommended Actions

- Verify parameter type definition.
- Use the correct SDK data type.

### Evidence

- API name.
- Expected type.
- Actual type.
- SDK version.

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

### Evidence

- API name.
- Parameter name and value.
- Expected valid range.

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
- Retry after initialization and state verification.

### Diagnostic Chain

- DecisionTree: [SDK Initialization Failed](../../09_DecisionTree/Software/SDKInitializationFailed.md)
- Tool: [iDetector Quick Troubleshooting](../../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)
- Evidence: complete command sequence and detector state transition.

---

# Diagnostic Checklist

- SDK initialized successfully.
- Detector object created successfully.
- Detector state is **Ready**.
- No previous task is pending.
- Required parameters are configured correctly.
- Detector.log is generated normally.

---

# Related Case

- [Connection Failed](../../11_Case/Communication/ConnectionFailed.md)
- No verified initialization-specific case should be inferred from this document if no matching case exists.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added concrete diagnostic-chain links and evidence requirements |
| v1.0 | 2026-08-07 | Initial release |