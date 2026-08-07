# SDK Exception Decision Tree

> Module: Software
>
> Category: Decision Tree
>
> Version: v4.0
>
> Last Updated: 2026-08-06

---

# Purpose

This decision tree is used when the SDK throws an exception, crashes, or terminates unexpectedly during execution.

Unlike API errors, SDK exceptions usually indicate abnormal execution inside the SDK, application runtime, operating system, or dependent libraries.

Typical execution sequence:

Application

↓

Load SDK DLL

↓

Initialize SDK

↓

Call SDK API

↓

Internal SDK Processing

↓

Operating System

↓

Return Result

If an exception occurs at any stage, isolate the execution layer before continuing.

---

# Symptom

The SDK terminates unexpectedly during execution.

Typical symptoms include:

- SDK Crash
- Unhandled Exception
- Access Violation
- Stack Overflow
- Null Pointer Exception
- Illegal Memory Access
- DLL Exception
- Application Closed Unexpectedly

---

# Symptom Classification

Identify the observed exception.

□ DLL Load Exception

□ Initialization Exception

□ Acquisition Exception

□ Callback Exception

□ Memory Exception

□ Access Violation

□ Application Crash

□ Unknown Exception

---

# Exception Execution Pipeline

```
Application
      │
      ▼
SDK DLL
      │
      ▼
SDK Runtime
      │
      ▼
Memory Allocation
      │
      ▼
Detector Communication
      │
      ▼
Image Processing
      │
      ▼
Callback
      │
      ▼
Return
```

Verification Status

```
Application        □

SDK DLL            □

Runtime            □

Memory             □

Communication      □

Callback           □

Exception Log      □
```

---

# Diagnostic Flow

```
                 SDK Exception
                       │
              DLL Loaded Normally?
                       │
         ┌─────────────┴─────────────┐
         │                           │
        NO                          YES
         │                           │
 Verify DLL Installation      Continue
                                      │
                                      ▼
             SDK Demo Crashes?
                                      │
          ┌───────────────────────────┴──────────────────────────┐
          │                                                      │
         YES                                                    NO
          │                                                      │
SDK / Runtime Investigation                          Application Investigation
                                                              │
                                                              ▼
                 Exception Reproducible?
                                                              │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
     Environment / Timing                     Continue
                                                 │
                                                 ▼
             Exception During Callback?
                                                 │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                YES                                       NO
                 │                                         │
      Callback Investigation                   Continue
                                                 │
                                                 ▼
           Access Violation?
                                                 │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                YES                                       NO
                 │                                         │
       Memory Investigation                     Continue
                                                 │
                                                 ▼
        Communication Related?
                                                 │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                YES                                       NO
                 │                                         │
Network Investigation                       SDK Internal Investigation
```

---

# Exception Classification

| Exception | Possible Cause | Next Decision Tree |
|-----------|----------------|--------------------|
| Access Violation | Invalid pointer / released object | APIError.md |
| Null Pointer | Invalid initialization | SDKInitializationFailed.md |
| Callback Crash | Callback implementation | CallbackFailure.md |
| Acquisition Crash | Image acquisition | AcquisitionTimeout.md |
| Communication Exception | Network interruption | DetectorOffline.md |
| DLL Load Failure | Missing dependency | SDKInitializationFailed.md |
| Stack Overflow | Recursive call / application bug | Application Debug |
| Heap Corruption | Memory overwrite | SDK Investigation |

---

# Diagnosis Hint

SDK exceptions are generally caused by one of the following:

1. Invalid API usage
2. Incorrect callback implementation
3. Invalid memory access
4. DLL dependency problems
5. Runtime library mismatch
6. Multi-thread synchronization issues
7. SDK internal defects

Before escalating, determine whether the issue is reproducible with the official SDK Demo.

---

# Software Hint

Most likely affected modules

★★★★★ SDK Runtime

★★★★★ Application

★★★★★ Callback

★★★★☆ Memory Management

★★★★☆ Runtime Library

★★★☆☆ Communication

★★★☆☆ Detector

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| SDK Demo | Reproduce exception | No crash |
| Visual Studio Debugger | Capture exception | Call stack available |
| Event Viewer | Windows crash log | Exception recorded |
| Dependency Walker | DLL dependency check | No missing DLL |
| Process Explorer | Monitor runtime modules | Normal execution |
| SDK Log | Verify execution flow | Complete API sequence |

---

# Expected Result

### SDK Demo

Expected Result

- SDK Demo runs normally.
- No unexpected termination.

---

### Exception

Expected Result

- No unhandled exception.
- No access violation.

---

### Memory

Expected Result

- Stable memory usage.
- No memory corruption.

---

### Callback

Expected Result

- Callback executes successfully.
- Returns normally.

---

# Quick Checklist

Verify

□ SDK Version

□ Runtime Library Installed

□ DLL Dependency

□ Exception Type

□ Exception Address

□ Call Stack

□ SDK Demo

□ Windows Event Log

□ Memory Usage

□ Callback Function

---

# Required Evidence

Collect before escalation

- Detector Model
- Detector SN
- SDK Version
- Firmware Version
- Windows Version
- Exception Code
- Exception Address
- Call Stack
- Dump File (if available)
- SDK Log
- Windows Event Log
- Application Log

---

# Possible Root Causes

## SDK

- Internal SDK defect
- Runtime library mismatch
- DLL dependency missing

---

## Application

- Invalid API sequence
- Incorrect callback implementation
- Multi-thread synchronization issue

---

## Memory

- Invalid pointer
- Heap corruption
- Buffer overflow

---

## Communication

- Unexpected disconnection
- Invalid response

---

## Operating System

- Missing Visual C++ Runtime
- Security software interference
- Windows compatibility issue

---

# Recommended Actions

Priority 1

- Reproduce using the official SDK Demo.

Priority 2

- Collect exception code and call stack.

Priority 3

- Verify runtime libraries and DLL dependencies.

Priority 4

- Verify callback implementation and API sequence.

Priority 5

- Generate a crash dump if reproducible.

Priority 6

- Escalate with complete diagnostic information.

---

# Escalation Criteria

Escalate when:

- SDK Demo reproduces the same exception.
- Exception is reproducible.
- Call stack has been collected.
- Runtime environment has been verified.
- DLL dependencies are complete.
- Application logic has been ruled out.

---

# Related Documents

## Software

- 09_DecisionTree/Software/SDKInitializationFailed.md
- 09_DecisionTree/Software/APIError.md
- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Software/DetectorNotFound.md

## Connection

- 09_DecisionTree/Connection/DetectorOffline.md

## Firmware

- 09_DecisionTree/Firmware/VersionMismatch.md

## Reference

- 15_Reference/SDKReference.md

## Tools

- 17_Tools/SDKDemo.md
- 17_Tools/VisualStudio.md
- 17_Tools/DependencyWalker.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v4.0 | 2026-08-06 | Initial release |