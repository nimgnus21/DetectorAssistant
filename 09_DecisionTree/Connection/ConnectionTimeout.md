# Connection Timeout Decision Tree

> Module: Communication
>
> Category: Decision Tree
>
> Version: v1.1
>
> Last Updated: 2026-08-10

---

# Symptom

The detector can be discovered successfully, but the connection process times out or fails.

Typical symptoms include:

- Connection Timeout
- Connection Failed
- SDK returns timeout error.
- Detector status remains Connecting.
- Detector disconnects during initialization.

---

# Diagnostic Flow

```
                 Connection Timeout
                         │
          Can detector be discovered?
                         │
              ┌──────────┴──────────┐
              │                     │
             NO                    YES
              │                     │
      Go to DetectorOffline         │
                                    ▼
                       Is detector Ping reachable?
                                    │
                        ┌───────────┴───────────┐
                        │                       │
                       NO                      YES
                        │                       │
                  Check Network           Continue
                  • IP Address
                  • Subnet Mask
                  • Switch
                  • Firewall
                                    │
                                    ▼
                        SDK Demo Connection OK?
                                    │
                        ┌───────────┴───────────┐
                        │                       │
                       NO                      YES
                        │                       │
                  Check SDK              Continue
                  • SDK Version
                  • DLL Files
                  • License
                                    │
                                    ▼
                    Firmware Compatible?
                                    │
                        ┌───────────┴───────────┐
                        │                       │
                       NO                      YES
                        │                       │
                  Upgrade Firmware       Continue
                                    │
                                    ▼
                 Detector Parameters Normal?
                                    │
                        ┌───────────┴───────────┐
                        │                       │
                       NO                      YES
                        │                       │
                 Parameter Recovery      Continue
                                    │
                                    ▼
                    Connection Successful?
                                    │
                        ┌───────────┴───────────┐
                        │                       │
                      YES                    NO
                        │                       │
                 Problem Solved        Escalate to Engineering
```

---

# Quick Checklist

Before escalation, verify:

- □ Detector can be discovered.
- □ Detector responds to Ping.
- □ IP configuration is correct.
- □ Firewall is disabled or configured.
- □ SDK version matches firmware.
- □ Required DLL files are present.
- □ License is valid.
- □ Detector firmware is compatible.
- □ Detector parameters are intact.

---

# Possible Root Causes

## Network

- Incorrect IP configuration
- Firewall blocking communication
- Switch instability
- Network latency

---

## SDK

- SDK version mismatch
- Missing runtime library
- Incorrect SDK configuration

---

## Firmware

- Firmware version mismatch
- Firmware upgrade incomplete
- Detector parameter corruption

---

## Detector

- Internal communication abnormal
- Detector startup incomplete

---

# Recommended Actions

Priority 1

- Verify detector discovery.
- Verify Ping communication.
- Verify network configuration.

Priority 2

- Test using the official SDK Demo.
- Compare with another PC.

Priority 3

- Verify firmware compatibility.
- Perform Parameter Recovery if required.

Priority 4

- Upgrade firmware if version mismatch is confirmed.

---

# Escalation Criteria

Escalate when:

- Timeout occurs on multiple computers.
- Official SDK Demo also fails.
- Firmware recovery is unsuccessful.
- Detector remains inaccessible after complete verification.
- Internal hardware fault is suspected.

---

# Related Documents

## Workflow

- [Connection Workflow](../../06_Workflow/ConnectionWorkflow.md)
- [Configuration Workflow](../../06_Workflow/ConfigurationWorkflow.md)

## Case

- [Timeout Case](../../11_Case/Communication/Timeout.md)
- [Connection Failed Case](../../11_Case/Communication/ConnectionFailed.md)
- [Network Configuration Case](../../11_Case/Communication/NetworkConfiguration.md)

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