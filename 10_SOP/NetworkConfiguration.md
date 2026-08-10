# Network Configuration

> Module: Standard Operating Procedure
>
> SOP ID: SOP-002
>
> Category: Network Configuration
>
> Version: v1.1

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

Software / Diagnostics

- [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)
- Windows Network Configuration
- [Ping](../17_Tools/Ping/)
- [Wireshark](../17_Tools/Wireshark/)（需要分析丢包或异常网络流量时）
- [Log Viewer](../17_Tools/LogViewer/)（需要关联连接失败时间点时）
- [DTDI Tool](../17_Tools/SDKTool/DTDITool.md)（适用产品）

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

Execute the [Ping](../17_Tools/Ping/) test and observe:

- Response
- Packet loss
- Latency

### Output

Connectivity verified.

### Acceptance Criteria

- Successful replies
- 0% packet loss during the verification window

### Exception Handling

- Connection failure → [Connection DecisionTree](../09_DecisionTree/Connection/)
- General inability to connect → [Unable To Connect](../07_FailureKnowledge/ConnectionFailure/UnableToConnect.md)
- Suspected intermittent packet loss → [Packet Loss](../07_FailureKnowledge/ImageFailure/PacketLoss.md) and capture evidence with [Wireshark](../17_Tools/Wireshark/)

---

## Step 6 – Connect Detector

### Input

Configured network.

### Process

- Launch the [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md).
- Execute detector connection.
- Wait for Ready state.

### Output

Detector connected.

### Acceptance Criteria

Detector status becomes Ready.

### Exception Handling

Preserve `Detector.log`, inspect with [Log Viewer](../17_Tools/LogViewer/) when needed, then refer to the [Connection DecisionTree](../09_DecisionTree/Connection/).

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

- Image-side failure → [Image DecisionTree](../09_DecisionTree/Image/)
- Data-loss artifact → [Packet Loss](../07_FailureKnowledge/ImageFailure/PacketLoss.md)

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
- If abnormal, logs or network evidence retained.

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
- Packet capture when applicable

---

# Exception Matrix

| Symptom | Possible Cause / Direction | Action |
|----------|----------------------------|--------|
| Ping failed | IP or physical connection | Verify network configuration and physical connection |
| Detector not found | Subnet / SDK / connection state | Run Connection DecisionTree and SDK check |
| Connection timeout | Network or communication interruption | Preserve log and verify connection path |
| Packet loss | Network instability | Verify with Ping; use Wireshark when evidence is needed |
| Image timeout | Communication or image-side interruption | Refer to Image DecisionTree and Packet Loss knowledge |

---

# Related Documents

- [Detector Installation SOP](DetectorInstallation.md)
- [Communication Workflow](../06_Workflow/CommunicationWorkflow.md)
- [Connection Workflow](../06_Workflow/ConnectionWorkflow.md)
- [Connection DecisionTree](../09_DecisionTree/Connection/)
- [Image DecisionTree](../09_DecisionTree/Image/)
- [Unable To Connect](../07_FailureKnowledge/ConnectionFailure/UnableToConnect.md)
- [Packet Loss](../07_FailureKnowledge/ImageFailure/PacketLoss.md)
- [Ping](../17_Tools/Ping/)
- [Wireshark](../17_Tools/Wireshark/)
- [Log Viewer](../17_Tools/LogViewer/)
- [Software Index](../00_Project/Index/SoftwareIndex.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added direct diagnostics, DecisionTree and failure knowledge links |
| v1.0 | 2026-08-07 | Initial release |