# Communication Error Code

> Module: Communication
>
> Category: Error Code Reference

---

# Overview

This module documents communication-related error codes encountered during detector connection, command transmission, and image data transfer.

Communication failures are typically caused by network configuration issues, communication device abnormalities, packet transmission errors, or unstable network environments.

This module is intended to assist FAE engineers and software developers in locating communication failures quickly and selecting the appropriate troubleshooting workflow.

---

# Scope

This module applies to:

- Ethernet communication
- TCP command communication
- UDP image transmission
- Network configuration
- Detector connection
- Packet transmission
- Image transfer

---

# Document Structure

```
Communication
├── README.md
├── Ethernet.md
├── TCP.md
└── UDP.md
```

---

# Category Description

## Ethernet

Physical network connection and communication device related errors.

Typical issues include:

- Network adapter
- IP configuration
- Communication device
- Detector discovery
- Connection establishment

---

## TCP

Detector command channel communication.

Typical issues include:

- Socket connection
- Detector response timeout
- Connection interruption
- Detector online status

---

## UDP

Detector image transmission channel.

Typical issues include:

- Packet loss
- Packet validation
- Buffer overflow
- Frame loss
- Image transmission

---

# Communication Workflow

```
Power On

↓

Detector Connected

↓

Cmd_Connect

↓

TCP Connection Established

↓

Detector Ready

↓

Cmd_StartAcq

↓

UDP Image Transmission

↓

Evt_Image
```

---

# Common Symptoms

| Symptom | Possible Module |
|----------|-----------------|
| Cannot connect detector | Ethernet / TCP |
| Detector offline | Ethernet |
| Connection timeout | TCP |
| Image timeout | UDP |
| Packet loss | UDP |
| Frame loss | UDP |
| Network interruption | Ethernet / TCP |
| Image transmission abnormal | UDP |

---

# Recommended Troubleshooting Procedure

When communication-related errors occur, perform the following checks:

1. Verify detector power status.
2. Verify Ethernet cable connection.
3. Verify detector IP configuration.
4. Verify PC network configuration.
5. Confirm the detector can be reached using Ping.
6. Check Detector.log.
7. Review the corresponding Communication error document.
8. Follow the related DecisionTree.
9. Escalate if the issue cannot be reproduced or resolved.

---

# Related Modules

## DecisionTree

```
09_DecisionTree/Connection
```

---

## Workflow

```
06_Workflow/CommunicationWorkflow.md
```

---

## FailureKnowledge

```
07_FailureKnowledge/SystemFailure
```

---

## Case

```
11_Case/Communication
```

---

# Related Log

```
Detector.log
```

Communication issues should always be analyzed together with:

- Detector.log
- Detector IP
- PC IP
- Network topology
- Detector firmware version
- SDK version

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |