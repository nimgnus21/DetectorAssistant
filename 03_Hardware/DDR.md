# DDR

Version: V2.0

Module: Hardware

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- ../02_System/DetectorArchitecture.md
- ../02_System/SignalDomain.md
- ../02_System/TimingArchitecture.md
- ../02_System/ImagePipeline.md
- FPGA.md
- ADC.md
- Ethernet_Controller.md
- ../04_Software/Firmware.md
- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/

---

# 1. Purpose

DDR（Double Data Rate SDRAM）是数字平板探测器的数据缓存模块。

负责缓存 FPGA 接收的数字图像数据，为图像处理、校准及网络传输提供高速存储空间。

DDR 不参与图像采集、模拟信号处理及图像校准计算。

---

# 2. Scope

适用于所有数字平板探测器产品。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Definition

DDR 位于 FPGA 外部高速存储器。

在图像采集过程中，FPGA 将 ADC 输出的数据写入 DDR，后续图像处理及网络发送均从 DDR 读取图像数据。

DDR 是图像缓存区，不属于永久存储设备。

---

# 4. Physical Structure

DDR 主要连接：

- FPGA
- Power Board

系统位置：

```text
ADC

↓

FPGA

↓

DDR

↓

FPGA

↓

Ethernet Controller
```

---

# 5. Internal Composition

DDR 在系统中的职责包括：

- Image Buffer
- Frame Cache
- Temporary Storage
- High-Speed Read/Write

培训资料未涉及 DDR 内部 Bank、Row、Column 等存储结构，本知识库不展开芯片内部实现。

---

# 6. Physical Principle

FPGA 在读出过程中持续接收 ADC 输出的数据。

数字图像按照采集顺序写入 DDR。

当图像处理或网络发送需要数据时，FPGA 从 DDR 读取对应图像帧。

整个过程中 DDR 提供高速随机访问能力。

---

# 7. Working Process

```text
ADC Output

↓

FPGA Receive

↓

DDR Write

↓

Frame Buffer

↓

FPGA Read

↓

Image Processing

↓

Communication
```

---

# 8. Timing Relationship

DDR 工作于：

- Readout
- Image Processing
- Communication

曝光阶段：

DDR 不参与数据缓存。

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

输入：

Digital Image Data

输出：

Buffered Image Data

Signal Flow：

```text
Digital Domain

↓

FPGA

↓

DDR

↓

FPGA

↓

Image Pipeline
```

Reference：

- ../02_System/SignalDomain.md

---

# 10. Interface

## Input

- FPGA Write Data

## Output

- FPGA Read Data

## Control

- Memory Clock
- Address Bus
- Data Bus
- Control Bus

## Connected Hardware

- FPGA

---

# 11. Performance Characteristics

DDR 负责：

- 高速缓存
- 连续写入
- 连续读取
- 图像帧缓存
- 临时数据存储

DDR 不负责：

- 图像计算
- 数据分析
- 图像校正

性能参数应以具体产品硬件规格为准。

---

# 12. Failure Mode

可能出现的失效模式包括：

- Memory Initialization Failure
- Memory Read Failure
- Memory Write Failure
- Address Error
- Data Corruption
- Clock Failure
- Memory Overflow
- Memory Access Timeout

---

# 13. Failure Mechanism

DDR 异常可能导致：

- 图像缓存失败
- 图像帧丢失
- 图像数据损坏
- 图像发送异常
- 图像重复
- 图像中断
- 系统运行异常

DDR 失效通常表现为数字数据异常，而不是模拟信号异常。

---

# 14. Image Manifestation

DDR 异常可能表现为：

- 图像不完整
- 图像重复
- 图像帧缺失
- 图像撕裂
- 图像错位
- 图像冻结
- 图像无法发送

最终表现需结合 FPGA 及 Communication 模块综合分析。

---

# 15. Diagnostic Method

建议诊断顺序：

1. 确认 FPGA 工作正常。
2. 检查 DDR 初始化状态。
3. 检查 Memory Clock。
4. 检查 DDR 写入状态。
5. 检查 DDR 读取状态。
6. 检查图像缓存是否完整。
7. 检查通信输出是否正常。
8. 结合系统日志及故障树综合分析。

---

# 16. Related Calibration

DDR 不参与校准算法。

DDR 为 Calibration 提供：

- 原始图像缓存
- 校准图像缓存
- 中间数据缓存

DDR 异常可能导致校准流程中断或校准图像异常。

Reference：

- ../05_Calibration/

---

# 17. Related Documents

System：

- DetectorArchitecture.md
- SignalDomain.md
- TimingArchitecture.md
- ImagePipeline.md

Hardware：

- FPGA.md
- ADC.md
- Ethernet_Controller.md

Software：

- Firmware.md

Knowledge：

- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/
- ../09_DecisionTree/

---

# 18. Knowledge Graph

```text
ADC
 │
 ▼
FPGA
 │
 ▼
DDR
 │
 ▼
FPGA
 │
 ├────────► Image Pipeline
 └────────► Communication
```

---

# 19. Document Boundary

本文件负责：

- DDR 定义
- 系统位置
- 数据缓存职责
- 工作流程
- 时序关系
- 接口关系
- 常见失效模式
- 图像影响
- 故障定位入口

本文件不负责：

- DDR 芯片设计
- 存储控制器实现
- FPGA Memory Controller
- 图像算法
- 芯片维修

---

# 20. Reference

## Fact

- 《探测器工作原理1.1》：数字图像采集流程及 FPGA 后级数据处理架构。

## Theory

- 培训资料关于数字图像缓存、数据组织及图像输出流程。