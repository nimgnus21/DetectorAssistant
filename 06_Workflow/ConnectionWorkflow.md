# ConnectionWorkflow

Version: V2.0

Module: Workflow

Status: Released

Source Level:
- Engineering
- System

Applicable Product:
- Wired Detector
- Wireless Detector

Related Documents:
- DetectorLifecycle.md
- InitializationWorkflow.md
- ExposureWorkflow.md
- ../02_System/Communication.md
- ../03_Hardware/WiFi_Module.md
- ../04_Software/README.md
- ../07_FailureKnowledge/CommunicationFailure.md
- README.md

---

# 1. Purpose

Connection Workflow 定义数字平板探测器（Flat Panel Detector，FPD）完成 Initialization 后，与 Host（工作站/SDK）建立通信连接的标准流程。

本流程负责网络建立、Detector 连接、SDK 建立会话、Panel 参数同步及 Detector Ready 状态建立，为后续 Exposure Workflow 提供可靠的运行环境。

---

# 2. Scope

适用于：

- Gigabit Ethernet Detector
- Wireless Detector
- SDK Communication
- Clinical Workstation
- Factory Test Software
- Service Tool

---

# 3. Workflow Objectives

Connection Workflow 的主要目标包括：

- 建立网络连接
- 建立 SDK 会话
- 获取 Detector 信息
- 同步 Detector 参数
- 建立 Heartbeat
- 进入 Ready 状态

---

# 4. Workflow Overview

```text
Initialization Complete

↓

Communication Module Ready

↓

Network Initialization

↓

Detector Discovery

↓

SDK Connection

↓

Detector Connection

↓

Detector Information

↓

Panel Configuration

↓

Heartbeat

↓

Detector Ready

↓

Exposure Workflow
```

---

# 5. Workflow Inputs

输入包括：

- Initialization Complete
- Communication Module Ready
- Ethernet Link Up（有线）
- Wi-Fi Ready（无线）
- Host SDK Running
- Detector Firmware Running

---

# 6. Communication Architecture

Connection Workflow 包括三个层级。

```text
Physical Layer

↓

Network Layer

↓

Application Layer
```

### Physical Layer

负责：

- Ethernet
- Wi-Fi

---

### Network Layer

负责：

- IP
- TCP
- UDP（设备发现）

---

### Application Layer

负责：

- SDK
- Detector Service
- Configuration
- Image Acquisition Command

---

# 7. Communication Modes

根据产品类型支持不同通信模式。

## Ethernet Mode

特点：

- Gigabit Ethernet
- 固定连接
- 高稳定性
- 医院固定安装

---

## Wi-Fi Client Mode

特点：

- 接入医院无线网络
- DHCP 或 Static IP
- 通过 Host 建立连接

---

## Wi-Fi AP Mode

特点：

- Detector 建立热点
- Host 主动连接 Detector
- 现场维修及测试常用

---

# 8. Network Initialization

建立网络环境。

包括：

- Link Detection
- PHY Initialization
- IP Configuration
- Gateway Configuration
- DNS（如适用）

无线产品包括：

- SSID
- Password
- Channel
- Signal Strength

输出：

Network Ready

---

# 9. Detector Discovery

Host 搜索 Detector。

包括：

- Broadcast Discovery
- Detector Enumeration
- Device List Refresh

获得：

- Detector Name
- Serial Number
- IP Address
- MAC Address

输出：

Detector Found

---

# 10. SDK Connection

SDK 建立通信。

包括：

- SDK Initialize
- Open SDK
- Enumerate Detector
- Connect Detector
- Open Session

验证：

- Firmware Version
- Protocol Version
- Connection Status

输出：

SDK Connected

---

# 11. Detector Connection

建立 Detector Session。

包括：

- Session Create
- Connection Verify
- Communication Channel Open
- Command Channel Ready

输出：

Detector Connected

---

# 12. Detector Information

读取设备信息。

包括：

- Detector Model
- Detector ID
- Serial Number
- Hardware Version
- Firmware Version
- FPGA Version
- ASIC Version
- Battery Information（无线）
- Temperature Status

输出：

Detector Information Loaded

---

# 13. Panel Configuration

同步 Detector 配置。

包括：

## Communication Parameter

- IP
- Port
- Timeout

---

## Exposure Parameter

- Trigger Mode
- Exposure Mode

---

## Detector Parameter

- Working Mode
- Binning
- ROI

---

## Calibration

加载：

- Offset Template
- Gain Template
- Defect Template

---

输出：

Panel Configuration Complete

---

# 14. Heartbeat

建立在线监测。

包括：

- Heartbeat Packet
- Status Update
- Connection Monitor
- Auto Reconnect

主要作用：

- 判断 Detector Online
- 判断连接是否中断
- 保持 SDK Session

输出：

Detector Online

---

# 15. Workflow Outputs

Connection Workflow 输出：

- Network Ready
- SDK Connected
- Detector Connected
- Detector Configuration Loaded
- Calibration Loaded
- Detector Ready

系统进入：

Exposure Workflow

---

# 16. State Transition

```text
INITIALIZATION COMPLETE

↓

NETWORK READY

↓

DETECTOR FOUND

↓

SDK CONNECTED

↓

SESSION CREATED

↓

CONFIGURATION LOADED

↓

HEARTBEAT

↓

READY
```

---

# 17. Timing Relationship

```text
PowerOnWorkflow

↓

InitializationWorkflow

↓

ConnectionWorkflow

├── Network Initialization
├── Detector Discovery
├── SDK Connection
├── Detector Connection
├── Panel Configuration
└── Heartbeat

↓

ExposureWorkflow
```

---

# 18. Common Connection Failure

| Failure | Description |
|----------|-------------|
| Link Down | 网线断开 |
| Wi-Fi Not Connected | 无线连接失败 |
| Detector Not Found | 未发现 Detector |
| SDK Initialization Failed | SDK 初始化失败 |
| Connect Timeout | 建立连接超时 |
| Session Failed | Session 创建失败 |
| Version Mismatch | 固件/协议版本不一致 |
| Configuration Download Failed | 参数同步失败 |
| Heartbeat Lost | 心跳丢失 |
| Detector Offline | Detector 离线 |

详细处理参见：

- WorkflowTroubleshooting.md
- CommunicationFailure.md

---

# 19. Engineering Notes

工程建议：

- 初始化完成后再建立连接。
- 参数同步完成前禁止曝光。
- Heartbeat 应持续监测连接状态。
- 通信异常应记录错误代码及日志。
- 自动重连不应影响 Detector 内部运行状态。

---

# 20. Relationship with Other Modules

## Initialization Workflow

提供：

- Hardware Ready
- Firmware Ready
- Calibration Ready

---

## Hardware

提供：

- Ethernet Controller
- Wi-Fi Module

---

## Software

负责：

- SDK
- Communication Service
- Network Service

---

## Exposure Workflow

Connection 完成后进入 Exposure Workflow。

---

# 21. Document Boundary

本文件负责：

- 网络初始化
- Detector 发现
- SDK 建立连接
- Session 建立
- Detector 参数同步
- Heartbeat 建立
- Detector Ready

本文件不负责：

- FPGA 初始化
- ASIC 初始化
- 曝光控制
- 图像采集
- 图像校正
- 图像处理

---

# 22. Knowledge Graph

```text
Initialization Complete

↓

Network Initialization

↓

Detector Discovery

↓

SDK Connection

↓

Detector Connection

↓

Detector Information

↓

Panel Configuration

↓

Heartbeat

↓

Detector Ready

↓

Exposure Workflow
```

---

# 23. Summary

Connection Workflow 定义 Detector 完成初始化后建立完整通信链路的全过程，包括网络初始化、设备发现、SDK 会话建立、Detector 信息读取、Panel 参数同步及 Heartbeat 管理。完成本流程后，Detector 进入 Ready 状态，可响应 Host 控制并执行后续曝光及图像采集流程，是连接系统初始化与图像采集的重要桥梁。