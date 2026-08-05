# Communication

Version: V2.0

Module: System

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- DetectorArchitecture.md
- SignalDomain.md
- TimingArchitecture.md
- ImagePipeline.md
- ../03_Hardware/FPGA/README.md
- ../03_Hardware/Ethernet_Controller/README.md
- ../03_Hardware/WiFi_Module/README.md
- ../04_Software/SDK.md
- ../04_Software/iDetector4.md
- ../06_Workflow/Connection.md

---

# 1. Purpose

Communication 定义数字平板探测器与外部设备之间的数据通信架构。

本文件描述通信对象、通信路径、通信阶段及模块之间的关系。

本文件不描述网络协议实现、驱动程序、SDK 接口及软件操作。

---

# 2. Scope

适用于所有数字平板探测器产品。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

适用于：

- 网络连接
- 图像传输
- SDK 通信
- 工作站通信
- 售前网络部署
- 售后通信故障分析

---

# 3. Core Concept

Communication Architecture 用于建立探测器与工作站之间的数据传输链路。

图像数据完成处理后，通过通信模块发送至上位机软件。

通信层负责数据传输，不负责图像生成和图像处理。

---

# 4. Communication Architecture

```text
Detector

↓

Communication Interface

↓

Physical Network

↓

Workstation

↓

SDK

↓

Application Software

↓

Image Display
```

---

# 5. Communication Components

| Component | Function |
|-----------|----------|
| FPGA | 输出数字图像数据 |
| Communication Interface | 数据发送接口 |
| Ethernet Controller | 网络数据传输 |
| WiFi Module（适用型号） | 无线数据传输 |
| Physical Network | 建立通信链路 |
| Workstation | 接收图像数据 |
| SDK | 数据接口 |
| Application Software | 图像显示与控制 |

---

# 6. Communication Flow

```text
Image Output

↓

FPGA

↓

Communication Interface

↓

Ethernet / WiFi

↓

Workstation

↓

SDK

↓

Application Software

↓

Image Display
```

---

# 7. Communication Stage

| Stage | Input | Output |
|--------|-------|--------|
| Image Output | Image Frame | Digital Image |
| Data Packaging | Digital Image | Transfer Data |
| Physical Transmission | Transfer Data | Network Data |
| Workstation Reception | Network Data | Received Data |
| SDK Processing | Received Data | Image Object |
| Application Display | Image Object | Display Image |

---

# 8. Communication Boundary

Communication 起始于 FPGA 输出数字图像。

Communication 结束于应用软件完成图像接收。

图像采集、图像校正及图像生成属于其他系统模块。

Reference：

- SignalDomain.md
- ImagePipeline.md

---

# 9. Communication Relationship

## Relationship With SignalDomain

Communication Domain 为 SignalDomain 的最终输出阶段。

SignalDomain 负责数字数据生成。

Communication 负责数字数据传输。

Reference：

SignalDomain.md

---

## Relationship With TimingArchitecture

Communication 在图像处理完成后开始。

通信结束后，一个采集周期完成。

Reference：

TimingArchitecture.md

---

## Relationship With ImagePipeline

ImagePipeline 输出最终图像。

Communication 将图像发送至工作站。

Reference：

ImagePipeline.md

---

## Relationship With Software

SDK 建立探测器与应用软件之间的数据接口。

应用软件负责：

- 图像显示
- 图像保存
- 图像浏览
- 用户操作

Reference：

../04_Software/

---

## Relationship With Workflow

Communication 属于系统连接流程的重要组成部分。

包括：

- 网络连接
- 设备发现
- 建立连接
- 图像接收
- 连接释放

Reference：

../06_Workflow/

---

# 10. Communication Topology

## Wired Communication

```text
Detector

↓

Ethernet Cable

↓

Network Interface

↓

Workstation
```

适用于：

- 固定安装
- 高稳定性环境
- 高数据吞吐需求

---

## Wireless Communication

```text
Detector

)))

WiFi

)))

Wireless Network

↓

Workstation
```

适用于支持无线通信的产品型号。

具体型号及配置要求参考产品资料。

---

# 11. Communication Characteristics

| Item | Description |
|------|-------------|
| Communication Object | Image Data |
| Communication Direction | Detector → Workstation |
| Data Unit | Image Frame |
| Communication Trigger | Image Processing Completed |
| Communication End | Image Successfully Received |

---

# 12. Engineering Characteristics

Communication 模块负责图像数据传输。

通信模块不参与：

- X-Ray 信号采集
- 图像校正
- 图像重建
- 校准计算

通信链路应保持稳定、连续。

通信异常不会改变图像处理流程，但可能导致图像无法正常接收。

---

# 13. Failure Mapping

| Communication Stage | Possible Failure | Related Knowledge |
|---------------------|------------------|-------------------|
| Physical Connection | Cable Disconnected | FailureKnowledge |
| Network Establishment | Connection Failed | FailureKnowledge |
| Data Transmission | Packet Loss | FailureKnowledge |
| Workstation Reception | Receive Timeout | FailureKnowledge |
| SDK Communication | SDK Initialization Failed | Software |
| Application | Image Not Displayed | Software |

---

# 14. Knowledge Relationship

```text
DetectorArchitecture

↓

SignalDomain

↓

TimingArchitecture

↓

ImagePipeline

↓

Communication

├────────► Workflow

├────────► Software

├────────► FailureKnowledge

├────────► DecisionTree

└────────► SOP
```

---

# 15. Document Boundary

本文件负责：

- 通信架构
- 通信流程
- 通信对象
- 通信阶段
- 通信关系

本文件不负责：

- 网络协议实现
- SDK API
- IP 地址配置
- 网络参数设置
- 软件操作步骤
- 通信故障排查流程

---

# 16. Reference

## Fact

- 用户手册中关于设备连接、网络连接、软件连接及图像传输流程。
- 产品规格说明书中关于通信接口及支持方式。

## Theory

- 数字平板探测器培训资料中关于图像传输、工作站通信及系统通信架构。

## Engineering

对应知识在以下模块展开：

- 03_Hardware/Ethernet_Controller
- 03_Hardware/WiFi_Module
- 04_Software/SDK
- 04_Software/iDetector4
- 06_Workflow/Connection
- 07_FailureKnowledge/Network
- 09_DecisionTree/NetworkConnection