# Network

> Module: Glossary
>
> Category: Network Terminology

---

# Overview

This document defines the standard terminology related to detector network configuration, Ethernet communication, and network troubleshooting.

These terms are referenced throughout the DetectorAssistant knowledge base, including detector installation, communication troubleshooting, firmware upgrades, remote support, and workflow documentation.

---

# Network

## Definition

A communication infrastructure that enables data exchange between the detector and the host computer.

---

# Ethernet

## Definition

A wired Local Area Network (LAN) technology used for detector communication.

## Characteristics

- High reliability
- Low latency
- Stable bandwidth

---

# LAN (Local Area Network)

## Definition

A network connecting devices within a limited geographical area.

---

# IP Address

## Definition

A unique logical address assigned to each network device.

## Example

192.168.1.100

---

# Static IP

## Definition

A manually assigned IP address that remains unchanged until reconfigured.

## Advantages

- Stable communication
- Easy detector management

---

# Dynamic IP

## Definition

An IP address assigned automatically by a DHCP server.

---

# DHCP

## Definition

Dynamic Host Configuration Protocol.

A network service that automatically assigns IP addresses and related parameters.

---

# Subnet Mask

## Definition

A network parameter used to determine whether two devices belong to the same subnet.

## Example

255.255.255.0

---

# Gateway

## Definition

A network device that forwards traffic between different networks.

---

# DNS

## Definition

Domain Name System.

A service that translates domain names into IP addresses.

---

# MAC Address

## Definition

A globally unique hardware identifier assigned to a network interface.

---

# Host

## Definition

A computer or device connected to the detector network.

---

# Network Adapter

## Definition

The hardware interface that enables a computer to connect to an Ethernet network.

---

# Network Interface Card (NIC)

## Definition

The physical network device providing Ethernet communication capability.

---

# Link Speed

## Definition

The negotiated communication speed between two network devices.

## Common Values

- 100 Mbps
- 1 Gbps
- 2.5 Gbps
- 10 Gbps

---

# Auto Negotiation

## Definition

A mechanism allowing connected devices to automatically determine the optimal communication speed and duplex mode.

---

# Full Duplex

## Definition

A communication mode allowing simultaneous data transmission and reception.

---

# Half Duplex

## Definition

A communication mode where data transmission occurs in only one direction at a time.

---

# Ping

## Definition

A diagnostic tool used to verify whether a detector is reachable over the network.

---

# Round Trip Time (RTT)

## Definition

The time required for a packet to travel to the detector and return.

---

# Latency

## Definition

The delay between transmitting and receiving network data.

---

# Packet Loss

## Definition

The percentage of transmitted packets that fail to reach the destination.

---

# Bandwidth

## Definition

The maximum amount of data that can be transmitted through a network connection within a given period.

---

# Throughput

## Definition

The actual volume of useful data successfully transferred through the network.

---

# Network Congestion

## Definition

A condition in which excessive traffic reduces communication performance.

---

# Broadcast

## Definition

A network transmission sent to every device within the same subnet.

---

# Broadcast Discovery

## Definition

The process of locating detectors by sending broadcast packets.

---

# Firewall

## Definition

Software or hardware used to control network communication based on predefined security rules.

---

# Antivirus Software

## Definition

Security software that may restrict detector communication or SDK operation.

---

# VPN (Virtual Private Network)

## Definition

A secure network tunnel used for remote access.

## Typical Usage

- Remote technical support
- Remote debugging

---

# Switch

## Definition

A network device that forwards Ethernet frames between connected devices.

---

# Router

## Definition

A device connecting different IP networks.

---

# Network Cable

## Definition

An Ethernet cable used to connect the detector and computer.

## Common Types

- Cat5e
- Cat6
- Cat6A
- Cat7

---

# RJ45

## Definition

The standard Ethernet connector used by most detectors.

---

# Jumbo Frame

## Definition

An Ethernet frame larger than the standard 1500-byte MTU.

---

# MTU (Maximum Transmission Unit)

## Definition

The maximum packet size that can be transmitted over a network interface.

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