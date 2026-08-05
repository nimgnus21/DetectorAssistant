# Ethernet Controller

Version: V2.0

Module: Hardware

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series

Related Documents:
- ../02_System/DetectorArchitecture.md
- ../02_System/Communication.md
- ../02_System/ImagePipeline.md
- FPGA.md
- DDR.md
- ../04_Software/iDetector.md
- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/

---

# 1. Purpose

Ethernet Controller 是数字平板探测器有线网络通信控制模块。

负责建立探测器与主机之间的以太网通信，实现图像数据、设备状态及控制指令的可靠传输。

Ethernet Controller 不参与图像采集、图像校准及图像处理。

---

# 2. Scope

适用于采用 Gigabit Ethernet 通信接口的数字平板探测器。

包括：

- Pluto Series
- Mercu Series

---

# 3. Definition

Ethernet Controller 位于 FPGA 与 RJ45 网络接口之间。

FPGA 将待发送的数据交由 Ethernet Controller，Ethernet Controller 按照以太网协议完成数据封装、发送及接收。

Communication 模块建立于 Ethernet Controller 之上。

Reference：

- ../02_System/Communication.md

---

# 4. Physical Structure

主要连接：

- FPGA
- PHY
- RJ45 Connector
- Ethernet Cable
- Host Computer

系统位置：

```text
FPGA

↓

Ethernet Controller

↓

PHY

↓

RJ45

↓

Ethernet

↓

Host PC
```

---

# 5. Internal Composition

Ethernet Controller 包括：

- MAC Interface
- PHY Interface
- Packet Buffer
- Link Management
- Communication Control

培训资料未涉及芯片内部实现，本知识库不展开 MAC、DMA 等内部架构。

---

# 6. Physical Principle

FPGA 将图像数据发送至 Ethernet Controller。

Ethernet Controller 将数字数据封装为以太网数据帧。

PHY 完成电信号转换。

数据经 RJ45 接口通过网线发送至主机。

接收方向流程相反。

---

# 7. Working Process

```text
Image Ready

↓

FPGA

↓

Ethernet Controller

↓

Packet Generation

↓

PHY

↓

RJ45

↓

Ethernet Cable

↓

Host Computer

↓

iDetector
```

---

# 8. Timing Relationship

Ethernet Controller 工作于：

- Detector Initialization
- Communication
- Image Transfer

曝光及读出阶段不参与图像采集，仅负责数据传输。

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

输入：

- Digital Image Data
- Control Command

输出：

- Ethernet Frame

Signal Flow：

```text
FPGA

↓

Ethernet Controller

↓

Ethernet Frame

↓

Host
```

Reference：

- ../02_System/SignalDomain.md

---

# 10. Interface

## Input

- FPGA Data
- Configuration
- Clock

## Output

- Ethernet Packet

## External Interface

- RJ45

## Connected Hardware

- FPGA
- PHY
- Network Cable
- Host Computer

---

# 11. Performance Characteristics

负责：

- 图像传输
- 指令通信
- 状态反馈
- 网络连接

支持：

- Full Duplex
- Continuous Image Transfer
- Network Link Detection

具体传输速率及接口规格以产品规格书为准。

---

# 12. Failure Mode

可能出现：

- Link Down
- PHY Failure
- Packet Loss
- Communication Timeout
- Cable Disconnect
- MAC Failure
- Interface Failure

---

# 13. Failure Mechanism

可能导致：

- 无法建立连接
- iDetector 无法发现探测器
- 图像发送失败
- 图像传输中断
- 网络掉线
- 数据丢包
- 通信异常

---

# 14. Image Manifestation

通信异常通常不会改变图像内容。

可能表现为：

- 无图像接收
- 图像接收超时
- 图像发送失败
- 图像中断
- 连续曝光失败

---

# 15. Diagnostic Method

建议诊断顺序：

1. 检查探测器供电状态。
2. 检查 RJ45 接口。
3. 检查网线连接状态。
4. 检查 Link LED。
5. 检查主机网卡配置。
6. 检查 IP 配置。
7. 检查 iDetector 是否识别设备。
8. 检查通信日志。
9. 必要时进行 Ping 测试。
10. 根据 DecisionTree 定位故障。

---

# 16. Related Calibration

Ethernet Controller 不参与校准算法。

通信异常可能导致：

- 校准数据无法上传
- 校准命令无法执行
- 校准结果无法保存

---

# 17. Related Documents

System：

- DetectorArchitecture.md
- Communication.md
- ImagePipeline.md

Hardware：

- FPGA.md
- DDR.md

Software：

- iDetector.md

Knowledge：

- ../07_FailureKnowledge/Communication/
- ../08_ImageDiagnosis/
- ../09_DecisionTree/Communication/

---

# 18. Knowledge Graph

```text
FPGA
 │
 ▼
Ethernet Controller
 │
 ▼
PHY
 │
 ▼
RJ45
 │
 ▼
Ethernet Cable
 │
 ▼
Host PC
 │
 ▼
iDetector
```

---

# 19. Document Boundary

本文件负责：

- Ethernet Controller 定义
- 网络通信流程
- 数据传输路径
- 接口关系
- 常见失效模式
- 网络故障定位入口

本文件不负责：

- TCP/IP 协议实现
- Windows 网络配置
- iDetector 软件实现
- 网卡驱动
- PHY 芯片维修

---

# 20. Reference

## Fact

- 产品用户手册中关于探测器有线网络连接、RJ45 接口及主机通信流程。

## Theory

- 培训资料关于探测器图像传输流程及 FPGA 到主机的数据通信架构。