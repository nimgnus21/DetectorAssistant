# Network Failure Decision Tree

> Module: Communication
>
> Category: Decision Tree
>
> Version: v1.1
>
> Last Updated: 2026-08-10

---

# Symptom

The detector communication is unstable or unavailable due to network-related issues.

Typical symptoms include:

- Detector cannot be discovered.
- Ping request fails or is unstable.
- Frequent communication interruption.
- Image transmission timeout.
- Detector disconnects unexpectedly.

---

# Diagnostic Flow

```
                   Network Failure
                          │
                Physical Connection OK?
                          │
               ┌──────────┴──────────┐
               │                     │
              NO                    YES
               │                     │
      Check Ethernet Cable           ▼
      Check RJ45 Connector     Link LED ON?
      Check Switch                   │
                         ┌───────────┴───────────┐
                         │                       │
                        NO                      YES
                         │                       │
                 Check Port Status        Continue
                 Replace Cable                 │
                                               ▼
                              Can Ping Detector?
                                               │
                                  ┌────────────┴────────────┐
                                  │                         │
                                 NO                        YES
                                  │                         │
                        Verify Network Settings      Continue
                        • Detector IP
                        • PC IP
                        • Subnet Mask
                        • Gateway
                                               │
                                               ▼
                            Same Network Segment?
                                               │
                                  ┌────────────┴────────────┐
                                  │                         │
                                 NO                        YES
                                  │                         │
                          Modify IP Address         Continue
                                               │
                                               ▼
                         Firewall / Antivirus Blocking?
                                               │
                                  ┌────────────┴────────────┐
                                  │                         │
                                 YES                       NO
                                  │                         │
                          Disable or Configure      Continue
                                               │
                                               ▼
                             Jumbo Frame Correct?
                                               │
                                  ┌────────────┴────────────┐
                                  │                         │
                                 NO                        YES
                                  │                         │
                         Configure Network Card     Continue
                                               │
                                               ▼
                             Communication Stable?
                                               │
                                  ┌────────────┴────────────┐
                                  │                         │
                                 YES                       NO
                                  │                         │
                          Problem Solved          Escalate
```

---

# Quick Checklist

Verify the following items:

- □ Ethernet cable
- □ Network switch
- □ Link LED
- □ Detector IP address
- □ Host IP address
- □ Subnet mask
- □ Firewall configuration
- □ Jumbo Frame setting
- □ Network adapter driver
- □ Ping test

---

# Possible Root Causes

## Physical Layer

- Damaged Ethernet cable
- Loose RJ45 connector
- Switch failure
- NIC failure

---

## Network Configuration

- Incorrect IP address
- Incorrect subnet mask
- Different network segment
- IP conflict

---

## Operating System

- Windows Firewall
- Antivirus software
- Incorrect network profile
- Driver problem

---

## Network Performance

- Jumbo Frame mismatch
- High packet loss
- Unstable switch
- Network congestion

---

# Recommended Actions

Priority 1

- Verify physical network connection.
- Replace Ethernet cable if necessary.
- Test another switch port.

Priority 2

- Verify detector and host IP configuration.
- Confirm both devices are on the same subnet.

Priority 3

- Disable firewall temporarily for testing.
- Verify Jumbo Frame configuration.
- Update NIC driver if required.

Priority 4

- Compare results using another PC.
- Verify communication using the official SDK Demo.

---

# Escalation Criteria

Escalate when:

- Communication remains unstable after network verification.
- Multiple network environments show the same behavior.
- Official SDK Demo also fails.
- Hardware communication fault is suspected.

---

# Related Documents

## Workflow

- [Network Configuration](../../10_SOP/NetworkConfiguration.md)
- [Connection Workflow](../../06_Workflow/ConnectionWorkflow.md)

## Case

- [Network Configuration Case](../../11_Case/Communication/NetworkConfiguration.md)
- [Connection Failed Case](../../11_Case/Communication/ConnectionFailed.md)
- [Timeout Case](../../11_Case/Communication/Timeout.md)

## Tools

- [Ping](../../17_Tools/Ping/README.md)
- [Wireshark](../../17_Tools/Wireshark/README.md)
- [SDK Tool README](../../17_Tools/SDKTool/README.md)

## Failure Knowledge

- [Failure Analysis Method](../../07_FailureKnowledge/FailureAnalysisMethod.md)
- [Failure Classification](../../07_FailureKnowledge/FailureClassification.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Repaired obsolete Workflow, Reference and FailureKnowledge paths; added Ping and Wireshark evidence tools |
| v1.0 | 2026-08-06 | Initial release |