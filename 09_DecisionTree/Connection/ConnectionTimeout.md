# Connection Timeout Decision Tree

> Module: Communication
>
> Category: Decision Tree
>
> Version: v1.0
>
> Last Updated: 2026-08-06

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

- 06_Workflow/ConnectionWorkflow.md
- 06_Workflow/ConfigurationWorkflow.md

## Case

- 11_Case/Communication/Timeout.md
- 11_Case/Communication/ConnectionFailed.md
- 11_Case/Communication/NetworkConfiguration.md

## Tools

- 17_Tools/SDKTool/README.md
- 17_Tools/SDKTool/ModeConfiguration.md

## Reference

- 15_Reference/SDKReference.md

## Failure Knowledge

- 07_FailureKnowledge/Communication/

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-06 | Initial release |