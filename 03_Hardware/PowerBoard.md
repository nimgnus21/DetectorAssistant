# Power_Board

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
- ../02_System/PowerArchitecture.md
- ../02_System/DetectorArchitecture.md
- ../02_System/TimingArchitecture.md
- Battery.md
- FPGA.md
- Gate_Driver.md
- Readout_ASIC.md
- Ethernet_Controller.md
- ../07_FailureKnowledge/
- ../09_DecisionTree/

---

# 1. Purpose

Power Board（电源板）是数字平板探测器电源系统的核心硬件模块。

负责将外部输入电源或电池电源转换为系统各功能模块所需的工作电压，并完成电源分配、上电控制及供电管理，为整个探测器提供稳定、可靠的电能。

Power Board 不参与图像采集、图像处理及网络通信。

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

Power Board 位于整机供电链路中心。

系统所有功能模块均通过 Power Board 获取工作电源。

Power Board 根据系统工作状态，为不同模块提供对应电压，并保证各电源域稳定运行。

Reference：

- ../02_System/PowerArchitecture.md

---

# 4. Physical Structure

Power Board 位于探测器内部供电系统。

主要连接对象：

- External Power
- Battery（适用型号）
- FPGA
- Gate Driver
- Readout ASIC
- ADC
- DDR
- Ethernet Controller
- WiFi Module（适用型号）

系统位置：

```text
External Power / Battery

↓

Power Board

├────────► FPGA

├────────► Gate Driver

├────────► Readout ASIC

├────────► ADC

├────────► DDR

├────────► Ethernet Controller

└────────► WiFi Module
```

---

# 5. Internal Composition

Power Board 包括以下功能单元：

- Power Input
- Power Conversion
- Voltage Distribution
- Power Monitoring
- Protection Circuit
- Output Interface

培训资料及用户手册未描述具体电路拓扑，因此本知识库不定义 DC/DC、LDO、MOSFET 等器件级实现。

---

# 6. Physical Principle

系统上电后：

Power Board 接收外部电源或电池供电。

根据系统要求完成电压转换。

向不同模块输出对应工作电压。

各模块获得稳定供电后进入初始化状态。

整个工作过程中，Power Board 持续维持供电稳定。

---

# 7. Working Process

```text
External Power / Battery

↓

Power Input

↓

Power Conversion

↓

Voltage Distribution

↓

Module Power On

↓

System Initialization

↓

Detector Ready

↓

Exposure

↓

Image Readout

↓

Communication
```

---

# 8. Timing Relationship

Power Board 工作覆盖整个系统生命周期。

主要阶段：

- Power On
- Initialization
- Ready
- Exposure
- Readout
- Communication
- Shutdown

Power Board 是所有模块工作的前提。

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

Power Board 不参与图像信号传输。

仅提供供电。

Power Flow：

```text
Power Source

↓

Power Board

↓

Hardware Modules
```

Reference：

- ../02_System/PowerArchitecture.md

---

# 10. Interface

## Input

- External DC Power
- Battery Input（适用型号）

## Output

- Analog Power
- Digital Power
- Communication Power
- Control Power

## Connected Hardware

- FPGA
- Gate Driver
- Readout ASIC
- ADC
- DDR
- Ethernet Controller
- WiFi Module
- Battery

---

# 11. Performance Characteristics

Power Board 负责：

- 电压转换
- 电源分配
- 持续供电
- 电源监测
- 系统供电管理
- 电源保护

Power Board 不负责：

- 图像处理
- 图像采集
- 数据通信

具体输出电压及功率参数应以产品硬件设计资料为准。

---

# 12. Failure Mode

可能出现的失效模式包括：

- No Power Output
- Low Output Voltage
- High Output Voltage
- Voltage Ripple Abnormal
- Output Instability
- Power Sequence Failure
- Protection Triggered
- Power Connector Failure

---

# 13. Failure Mechanism

Power Board 异常可能导致：

- 系统无法启动
- FPGA 初始化失败
- Readout ASIC 无法工作
- Gate Driver 无法输出
- 网络模块无法初始化
- 曝光失败
- 图像采集失败
- 校准失败
- 通信失败

由于所有模块均依赖 Power Board，因此其故障通常表现为系统级异常。

---

# 14. Image Manifestation

Power Board 本身不会直接改变图像内容。

供电异常可能导致：

- 无图像
- 黑屏
- 图像中断
- 图像随机异常
- 曝光失败
- 校准失败
- 系统频繁重启

图像表现需结合具体供电异常模块进行分析。

---

# 15. Diagnostic Method

建议诊断顺序：

1. 确认外部电源正常。
2. 检查电源接口连接状态。
3. 检查电池状态（适用型号）。
4. 确认系统能够正常启动。
5. 检查各供电域输出状态。
6. 确认 FPGA 是否正常初始化。
7. 确认 Readout ASIC、Gate Driver 是否正常工作。
8. 检查系统日志。
9. 根据 DecisionTree 进一步定位故障。

---

# 16. Related Calibration

Power Board 不执行校准算法。

供电异常可能导致：

- Offset Calibration Failure
- Gain Calibration Failure
- Defect Calibration Failure

Power Board 是校准正常执行的基础条件。

Reference：

- ../05_Calibration/

---

# 17. Related Documents

System：

- PowerArchitecture.md
- DetectorArchitecture.md
- TimingArchitecture.md

Hardware：

- Battery.md
- FPGA.md
- Gate_Driver.md
- Readout_ASIC.md
- Ethernet_Controller.md

Knowledge：

- ../07_FailureKnowledge/Power/
- ../09_DecisionTree/PowerFailure/

---

# 18. Knowledge Graph

```text
External Power
        │
        ▼
Battery
        │
        ▼
Power Board
        │
 ┌──────┼───────────────┐
 │      │               │
 ▼      ▼               ▼
FPGA  Readout ASIC  Ethernet Controller
 │
 ▼
Gate Driver
 │
 ▼
TFT Array
```

---

# 19. Document Boundary

本文件负责：

- Power Board 定义
- 系统供电位置
- 电源分配关系
- 工作流程
- 电源接口
- 常见失效模式
- 故障定位入口

本文件不负责：

- 电源电路设计
- DC/DC 电路原理
- LDO 工作原理
- MOSFET 驱动设计
- PCB 布局
- 元器件级维修

---

# 20. Reference

## Fact

- 产品培训资料中关于探测器供电架构及系统启动流程。

- 产品用户手册中关于电源输入、设备启动及供电要求。

## Theory

- 系统供电架构及各功能模块供电关系。

Reference：

- ../02_System/PowerArchitecture.md