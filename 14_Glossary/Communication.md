# Communication

> Module: Glossary
>
> Category: Communication Terminology

---

# Overview

This document defines the standard terminology related to detector communication.

These terms are referenced throughout the DetectorAssistant knowledge base, including detector connection, SDK communication, network troubleshooting, workflow documentation, and error code analysis.

---

# Communication

## Definition

The process of exchanging commands, status information, and image data between the detector and the host computer.

---

# Detector Connection

## Definition

The process of establishing communication between the detector and the host application through the SDK.

---

# Connection

## Definition

An active communication session between the detector and the host computer.

---

# Disconnection

## Definition

Termination of communication between the detector and the host.

## Typical Causes

- Power loss
- Network interruption
- Manual disconnect
- Hardware failure

---

# TCP

## Definition

Transmission Control Protocol.

A reliable connection-oriented communication protocol used for detector command and control.

---

# UDP

## Definition

User Datagram Protocol.

A lightweight communication protocol commonly used for high-speed image transmission.

---

# Socket

## Definition

A software endpoint used for network communication between applications.

---

# Port

## Definition

A logical communication endpoint identified by a port number.

---

# IP Address

## Definition

A unique network address assigned to a detector or computer.

---

# MAC Address

## Definition

A globally unique hardware address assigned to a network interface.

---

# Static IP

## Definition

An IP address manually configured and fixed.

---

# DHCP

## Definition

Dynamic Host Configuration Protocol.

A protocol that automatically assigns IP addresses.

---

# Gateway

## Definition

The network device used to communicate with devices outside the local subnet.

---

# Subnet Mask

## Definition

A value used to determine whether two devices are in the same network segment.

---

# Ping

## Definition

A network diagnostic command used to verify connectivity and response time.

---

# Packet

## Definition

The basic unit of network data transmission.

---

# Packet Loss

## Definition

Failure of one or more packets to reach the destination.

## Typical Effects

- Image loss
- Communication instability
- Acquisition timeout

---

# Packet Sequence Number

## Definition

A number assigned to each packet to maintain transmission order.

---

# Checksum

## Definition

A value used to verify packet integrity during transmission.

---

# Timeout

## Definition

The maximum waiting time for a response before communication is considered failed.

---

# Detector Response Timeout

## Definition

The detector does not respond within the expected timeout period.

---

# Handshake

## Definition

The initialization procedure used before normal communication begins.

---

# Reconnection

## Definition

The process of re-establishing communication after disconnection.

---

# Broadcast

## Definition

A network transmission sent to all devices within the same subnet.

---

# Broadcast Discovery

## Definition

The process of locating detectors by sending broadcast packets.

---

# Heartbeat

## Definition

A periodic communication message used to verify that the detector remains online.

---

# Latency

## Definition

The delay between sending a request and receiving a response.

---

# Bandwidth

## Definition

The maximum amount of data that can be transmitted over a network within a given period.

---

# Throughput

## Definition

The actual amount of useful data successfully transmitted over the network.

---

# Communication Error

## Definition

Any abnormal condition preventing successful data exchange between the detector and host.

---

# Communication Recovery

## Definition

The process of restoring normal communication after a failure.

---

# Related SDK Commands

- Cmd_Connect
- Cmd_Disconnect
- Cmd_Reset

---

# Related SDK Events

- Evt_ConnectProcess
- Evt_GeneralWarn
- Evt_GeneralError
- Evt_TaskResult_Failed

---

# Related Error Codes

- Err_GeneralSocketErr
- Err_DetectorRespTimeout
- Err_CommDeviceNotFound
- Err_CommDeviceOccupied
- Err_CommParamNotMatch
- Err_InvalidPacketNo
- Err_InvalidPacketFormat
- Err_PacketDataCheckFailed
- Err_PacketLost_BufOverflow
- Err_ImgChBreak

---

# Related Modules

- 04_Communication
- 06_Workflow
- 09_DecisionTree
- 11_Case
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |