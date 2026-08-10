# Detector Offline Decision Tree

> Module: Communication
>
> Category: Decision Tree
>
> Version: v1.1
>
> Last Updated: 2026-08-10

---

# Symptom

The detector cannot be discovered or connected by the host computer.

Typical symptoms include:

- Detector is not listed in the SDK Demo.
- Detector status is **Offline**.
- Connection attempt fails.
- No response from the detector.
- Ping test fails.

---

# Diagnostic Flow

```
                    Detector Offline
                           │
             ┌─────────────┴─────────────┐
             │                           │
      Power Indicator ON?           Power Indicator OFF
             │                           │
            YES                         Check:
             │                     • Power Adapter
             │                     • Power Cable
             │                     • Power Switch
             │
             ▼
      Ethernet Link LED ON?
             │
      ┌──────┴──────┐
      │             │
     YES            NO
      │             │
      │        Check:
      │        • Network Cable
      │        • RJ45 Connector
      │        • Ethernet Port
      │        • Network Switch
      │
      ▼
      Can Ping Detector?
      │
 ┌────┴────┐
 │         │
YES        NO
 │         │
 │    Check:
 │    • IP Address
 │    • Subnet Mask
 │    • Firewall
 │    • Network Segment
 │
 ▼
SDK Demo Detects Device?
 │
 ┌────┴────┐
 │         │
YES        NO
 │         │
 │    Check:
 │    • SDK Version
 │    • Detector Driver
 │    • License
 │
 ▼
Connection Successful?
 │
 ┌────┴────┐
 │         │
YES        NO
 │         │
 │    Check:
 │    • Firmware Version
 │    • Detector Configuration
 │    • Parameter Recovery
 │
 ▼
Problem Resolved
```

---

# Quick Checklist

Before escalating the issue, verify:

- □ Detector power is normal.
- □ Power LED is on.
- □ Ethernet Link LED is on.
- □ Network cable is connected correctly.
- □ Detector can be pinged.
- □ Host IP configuration is correct.
- □ Firewall is disabled or configured correctly.
- □ SDK Demo detects the detector.
- □ SDK version matches the firmware.
- □ Detector firmware version is compatible.

---

# Possible Root Causes

## Hardware

- Power failure
- Ethernet interface failure
- Detector hardware fault

---

## Network

- Incorrect IP configuration
- Network cable failure
- Switch failure
- Firewall blocking communication

---

## Software

- SDK version mismatch
- Driver installation problem
- License issue

---

## Firmware

- Firmware version mismatch
- Parameter corruption
- Upgrade failure

---

# Recommended Actions

Priority 1

- Verify detector power.
- Verify Ethernet connection.
- Verify IP configuration.

Priority 2

- Test communication using the official SDK Demo.
- Compare with a known-good detector.

Priority 3

- Verify firmware compatibility.
- Perform parameter recovery if required.

Priority 4

- Escalate to engineering support if all previous checks fail.

---

# Escalation Criteria

Escalate when:

- Detector cannot be pinged after network verification.
- Detector is not detected by the official SDK Demo.
- Firmware recovery fails.
- Multiple verified host computers show the same behavior.
- Hardware failure is suspected.

---

# Related Documents

## Workflow

- [Connection Workflow](../../06_Workflow/ConnectionWorkflow.md)
- [Configuration Workflow](../../06_Workflow/ConfigurationWorkflow.md)

## Case

- [Connection Failed Case](../../11_Case/Communication/ConnectionFailed.md)
- [Network Configuration Case](../../11_Case/Communication/NetworkConfiguration.md)
- [Timeout Case](../../11_Case/Communication/Timeout.md)

## Tools

- [SDK Tool README](../../17_Tools/SDKTool/README.md)
- [Mode Configuration](../../17_Tools/SDKTool/ModeConfiguration.md)
- [Ping](../../17_Tools/Ping/README.md)

## Failure Knowledge

- [Failure Analysis Method](../../07_FailureKnowledge/FailureAnalysisMethod.md)
- [Failure Classification](../../07_FailureKnowledge/FailureClassification.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Repaired obsolete Reference and FailureKnowledge paths; converted valid related documents to Markdown links |
| v1.0 | 2026-08-06 | Initial release |