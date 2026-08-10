# Error Code

> DetectorAssistant Error Code Knowledge Base

---

# Overview

The ErrorCode module provides a structured reference for detector-related error codes and events encountered during installation, configuration, calibration, firmware upgrade, communication, image acquisition, and routine operation.

The module is an operational entry point, not only a code list. Each documented error category should lead to a concrete diagnostic path and, where available, to the corresponding DecisionTree, SOP, Tool, evidence requirement, and Case.

---

# Scope

This module covers:

- SDK Runtime
- Detector Communication
- Firmware
- Calibration
- Generator Interaction

---

# Current Directory Structure

```text
12_ErrorCode
├── README.md
├── Mercu0606X1CommonError.md
│
├── SDK
│   ├── README.md
│   ├── Initialization.md
│   ├── Acquisition.md
│   ├── Device.md
│   ├── Image.md
│   ├── License.md
│   └── Network.md
│
├── Communication
│   ├── README.md
│   ├── Ethernet.md
│   ├── TCP.md
│   └── UDP.md
│
├── Firmware
│   ├── README.md
│   ├── Boot.md
│   ├── EEPROM.md
│   └── Upgrade.md
│
├── Calibration
│   ├── README.md
│   ├── Offset.md
│   ├── Gain.md
│   └── Defect.md
│
└── Generator
    ├── README.md
    ├── Communication.md
    ├── Configuration.md
    ├── Exposure.md
    ├── GeneratorFault.md
    ├── GeneratorState.md
    ├── Interlock.md
    └── Trigger.md
```

The structure above reflects the current repository. Do not add placeholder paths to this index before the corresponding files exist.

---

# Standard Diagnostic Chain

```text
Exact Error Code / Event
        ↓
Locate ErrorCode Document
        ↓
Confirm Product / SDK / Firmware Context
        ↓
Follow Related DecisionTree
        ↓
Execute Related SOP
        ↓
Use Required Diagnostic Tool
        ↓
Preserve Logs and Evidence
        ↓
Verify Result
        ↓
Check Existing Case
        ↓
Create / Update Case if new verified knowledge exists
```

---

# Required Information for ErrorCode Handling

Before drawing a root-cause conclusion, record:

- Exact error code or event name
- Command or operation that triggered it
- Detector model
- Detector firmware version
- SDK version
- Detector state
- Occurrence time
- Reproduction frequency
- Detector.log and relevant screenshots

An error code alone must not be treated as a confirmed root cause unless the source documentation explicitly defines it as one.

---

# Error Document Standard

Each ErrorCode document should contain, where applicable:

1. Exact error code or event
2. Description
3. Triggering command or state
4. Possible causes
5. Recommended diagnostic actions
6. Required evidence
7. Related DecisionTree
8. Related SOP
9. Related Tool
10. Related Case or `No verified case yet`

Use concrete file links when the target exists. Do not replace a missing target with an invented path.

---

# Category Entry Points

- [SDK](SDK/README.md) — runtime, initialization, device, acquisition, image, license and SDK network errors.
- [Communication](Communication/README.md) — Ethernet, TCP command channel and UDP image transfer errors.
- [Firmware](Firmware/README.md) — boot, persistent parameter and firmware upgrade errors.
- [Calibration](Calibration/README.md) — Offset, Gain and Defect calibration errors.
- [Generator](Generator/README.md) — communication, exposure, trigger, interlock, configuration, state and generator faults.
- [Mercu0606X1 Common Error](Mercu0606X1CommonError.md) — product-specific error reference.

---

# Recommended Usage

When an error occurs:

1. Record the exact error code or event.
2. Locate the corresponding category and file.
3. Record product and version context.
4. Follow the linked DecisionTree before repeating disruptive operations.
5. Execute the linked SOP and Tool procedure.
6. Preserve logs and supporting evidence.
7. Verify the result.
8. Check whether an existing Case already documents the same scenario.
9. If a verified new scenario is discovered, feed it back into the relevant knowledge modules.

---

# Related Modules

- [DecisionTree](../09_DecisionTree/README.md)
- [Workflow](../06_Workflow/README.md)
- [FailureKnowledge](../07_FailureKnowledge/README.md)
- [SOP](../10_SOP/README.md)
- [Case](../11_Case/README.md)
- [Tools](../17_Tools/README.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Corrected actual directory index and added ErrorCode diagnostic-chain standard |
| v1.0 | 2026-08-07 | Initial release |