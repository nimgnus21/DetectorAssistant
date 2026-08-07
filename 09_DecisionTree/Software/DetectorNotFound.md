# Detector Not Found Decision Tree

> Module: Software
>
> Category: Decision Tree
>
> Version: v4.0
>
> Last Updated: 2026-08-06

---

# Purpose

This decision tree is used when the SDK initializes successfully but cannot detect any detector.

Typical discovery sequence:

SDK Initialized

↓

Enumerate Detector

↓

Broadcast Discovery

↓

Network Communication

↓

Detector Response

↓

Detector Information

↓

Detector Available

Failure at any stage should be isolated before proceeding.

---

# Symptom

The SDK starts successfully, but no detector is found.

Typical symptoms include:

- No Detector Found
- Detector Count = 0
- Enumerate Detector Failed
- No Available Detector
- Detector List Empty
- Detector Discovery Timeout

---

# Symptom Classification

Identify the observed behavior.

□ Detector never appears

□ Detector appears occasionally

□ Detector disappears after startup

□ Detector found on another PC

□ Detector LED normal

□ Detector LED abnormal

□ Ethernet disconnected

□ Unknown

---

# Detector Discovery Pipeline

```
Application
      │
      ▼
SDK
      │
      ▼
Broadcast Discovery
      │
      ▼
Ethernet
      │
      ▼
Switch
      │
      ▼
Detector
      │
      ▼
Detector Response
      │
      ▼
Detector Available
```

Verification Status

```
Application        □

SDK                □

Broadcast          □

Ethernet           □

Switch             □

Detector           □

Response           □

Available          □
```

---

# Diagnostic Flow

```
                 Detector Not Found
                         │
               SDK Initialized?
                         │
            ┌────────────┴────────────┐
            │                         │
           NO                        YES
            │                         │
 SDKInitializationFailed      Continue
                                      │
                                      ▼
                 Detector Powered On?
                                      │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
          Check Power Supply                     Continue
                                                   │
                                                   ▼
                Ethernet Connected?
                                                   │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
           Check Cable / Switch                  Continue
                                                   │
                                                   ▼
                  Ping Detector?
                                                   │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
         Check IP Configuration                  Continue
                                                   │
                                                   ▼
             Detector Utility Detects?
                                                   │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
        Firmware / Network                  Continue
                                                   │
                                                   ▼
            SDK Demo Detects Detector?
                                                   │
                 ┌────────────────────┴────────────────────┐
                 │                                         │
                NO                                        YES
                 │                                         │
           SDK Investigation              Customer Application
```

---

# Diagnosis Hint

Detector discovery failures are usually related to communication rather than image acquisition.

Typical investigation order:

1. Detector power
2. Ethernet link
3. IP configuration
4. Network broadcast
5. Firewall
6. SDK compatibility
7. Firmware compatibility

Always verify network connectivity before replacing hardware.

---

# Software Hint

Possible affected modules

★★★★★ Network Configuration

★★★★★ SDK Discovery

★★★★★ Detector Firmware

★★★★☆ Windows Firewall

★★★★☆ Ethernet Driver

★★★☆☆ Switch

★★★☆☆ Detector

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| SDK Demo | Detect detector | Detector listed |
| Detector Utility | Read detector information | Detector identified |
| Ping | Verify communication | Stable response |
| ipconfig | Verify PC IP address | Correct subnet |
| arp -a | Verify ARP table | Detector MAC present |
| Wireshark | Verify broadcast packets | Discovery packet exchanged |

---

# Expected Result

### Power

Expected Result

- Detector powered on.
- Status LED normal.

---

### Ethernet

Expected Result

- Link LED active.
- Cable connected.
- Switch operating normally.

---

### Network

Expected Result

- PC and detector in the same subnet.
- Ping successful.
- ARP entry created.

---

### SDK Demo

Expected Result

- Detector appears in the detector list.
- Detector information can be read.

---

### Detector Utility

Expected Result

- Detector model and serial number displayed correctly.

---

# Quick Checklist

Verify

□ Detector Power

□ Ethernet Cable

□ Link LED

□ Switch Status

□ PC IP Address

□ Detector IP Address

□ Ping

□ Firewall Disabled (for testing)

□ SDK Demo

□ Detector Utility

---

# Required Evidence

Collect before escalation

- Detector Model
- Detector SN
- Detector IP Address
- PC IP Address
- SDK Version
- Firmware Version
- Ping Result
- ipconfig Output
- arp -a Output
- Wireshark Capture (if available)
- SDK Log
- Detector Status Screenshot

---

# Possible Root Causes

## Network

- Incorrect IP configuration
- Different subnet
- Ethernet cable failure
- Switch failure
- Broadcast blocked

---

## Detector

- Detector not powered
- Detector firmware abnormal
- Detector boot failure

---

## SDK

- Discovery service failure
- SDK version incompatible

---

## Windows

- Firewall blocking UDP broadcast
- Antivirus interference
- Network adapter disabled

---

## Firmware

- Firmware incompatible with SDK
- Discovery protocol mismatch

---

# Recommended Actions

Priority 1

- Verify detector power.
- Verify Ethernet link.

Priority 2

- Verify IP configuration.
- Test Ping and ARP.

Priority 3

- Verify SDK Demo.
- Verify Detector Utility.

Priority 4

- Verify firewall and antivirus.

Priority 5

- Escalate after communication and firmware have been verified.

---

# Escalation Criteria

Escalate when:

- Detector cannot be discovered by SDK Demo.
- Detector Utility cannot detect the detector.
- Ping succeeds but SDK discovery still fails.
- Firmware version is verified.
- Multiple PCs reproduce the same issue.

---

# Related Documents

## Software

- 09_DecisionTree/Software/SDKInitializationFailed.md
- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Software/APIError.md

## Connection

- 09_DecisionTree/Connection/DetectorOffline.md

## Firmware

- 09_DecisionTree/Firmware/VersionMismatch.md

## Workflow

- 06_Workflow/NetworkWorkflow.md
- 06_Workflow/SoftwareWorkflow.md

## Reference

- 15_Reference/SDKReference.md
- 15_Reference/NetworkReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v4.0 | 2026-08-06 | Initial release |