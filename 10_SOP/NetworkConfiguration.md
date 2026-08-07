# Network Configuration

> Module: Standard Operating Procedure
>
> SOP ID: SOP-002
>
> Category: Network Configuration

---

# Scope

This SOP describes the standard procedure for configuring and verifying network communication between the detector and the host computer.

This procedure applies to:

- Initial detector installation
- Detector replacement
- IP address modification
- Communication troubleshooting
- Network recovery after configuration changes

---

# Objective

Ensure stable and reliable Ethernet communication between the detector and the host computer.

---

# Responsibility

| Role | Responsibility |
|------|----------------|
| FAE | Configure and verify network communication |
| Technical Support Engineer | Assist with abnormal network issues |
| Customer | Provide network environment if required |

---

# Preconditions

Before configuration, confirm:

- Detector is powered on.
- Network adapter is functioning properly.
- Ethernet cable is connected securely.
- SDK is installed.
- Detector model is confirmed.
- Network configuration information is available.

---

# Required Tools

Hardware

- Detector
- Host Computer
- Ethernet Cable
- Network Switch (if required)

Software

- SDK Tool
- Windows Network Configuration
- Ping
- DTDI Tool (if required)

---

# Required Files

- Detector Configuration File (if applicable)
- Detector.log (for troubleshooting)

---

# Safety Precautions

- Do not disconnect the Ethernet cable during communication.
- Avoid duplicate IP addresses on the same subnet.
- Record the original network configuration before making changes.

---

# Procedure

## Step 1 – Verify Physical Connection

### Input

Detector and host computer.

### Process

- Verify Ethernet cable connection.
- Check network adapter LEDs.
- Verify detector power status.

### Output

Physical connection confirmed.

### Acceptance Criteria

- Ethernet cable connected.
- Link LEDs active.

### Exception Handling

Check:

- Ethernet cable
- Network adapter
- Detector power

---

## Step 2 – Configure Host Network

### Input

Host computer.

### Process

- Open network adapter settings.
- Configure IP address.
- Configure subnet mask.
- Configure gateway if required.

### Output

Host network configured.

### Acceptance Criteria

Configuration completed successfully.

### Exception Handling

Verify network adapter configuration.

---

## Step 3 – Verify Detector Network

### Input

Detector.

### Process

- Read detector IP.
- Verify subnet mask.
- Verify gateway (if applicable).

### Output

Detector configuration confirmed.

### Acceptance Criteria

Detector parameters are correct.

### Exception Handling

Correct detector configuration before proceeding.

---

## Step 4 – Verify Same Subnet

### Input

Host IP and detector IP.

### Process

- Compare IP addresses.
- Compare subnet masks.

### Output

Network topology verified.

### Acceptance Criteria

Host and detector are located in the same subnet.

### Exception Handling

Modify IP configuration.

---

## Step 5 – Perform Ping Test

### Input

Detector IP.

### Process

Execute:

```text
ping <Detector IP>
```

Observe:

- Response
- Packet loss
- Latency

### Output

Connectivity verified.

### Acceptance Criteria

- Successful replies
- 0% packet loss

### Exception Handling

Refer to:

- DecisionTree/Connection
- ErrorCode/Communication

---

## Step 6 – Connect Detector

### Input

Configured network.

### Process

- Launch SDK application.
- Execute detector connection.
- Wait for Ready state.

### Output

Detector connected.

### Acceptance Criteria

Detector status becomes Ready.

### Exception Handling

Refer to:

- DecisionTree/Connection
- ErrorCode/Communication

---

## Step 7 – Verify Image Communication

### Input

Connected detector.

### Process

- Start acquisition.
- Perform exposure.
- Receive image.

### Output

Image received successfully.

### Acceptance Criteria

- Image acquisition successful.
- No timeout.
- No communication interruption.

### Exception Handling

Refer to:

- DecisionTree/Image
- ErrorCode/Image

---

# Acceptance Checklist

- Ethernet cable connected.
- Host IP configured.
- Detector IP verified.
- Same subnet confirmed.
- Ping successful.
- SDK connection successful.
- Detector status is Ready.
- Image transmission verified.

---

# Records

Record:

- Detector Model
- Detector Serial Number
- Detector IP Address
- Host IP Address
- Subnet Mask
- Gateway
- SDK Version
- Detector Firmware Version
- Test Result
- Detector.log

---

# Exception Matrix

| Symptom | Possible Cause | Action |
|----------|----------------|--------|
| Ping failed | Wrong IP | Verify network configuration |
| Detector not found | Different subnet | Reconfigure IP |
| Connection timeout | Firewall or cable | Check firewall and Ethernet cable |
| Packet loss | Network instability | Replace cable or switch |
| Image timeout | Communication interrupted | Refer to DecisionTree/Image |

---

# Related Documents

- SOP/DetectorInstallation
- 04_Communication
- 06_Workflow/CommunicationWorkflow
- 09_DecisionTree/Connection
- 11_Case/Communication
- 12_ErrorCode/Communication
- 14_Glossary/Communication
- 14_Glossary/Network

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |