# Battery

Version: V2.0

Module: Hardware

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series（Battery Version）
- Other Portable Detector

Related Documents:
- ../02_System/PowerArchitecture.md
- ../02_System/DetectorArchitecture.md
- Power_Board.md
- FPGA.md
- ../04_Software/iDetector.md
- ../07_FailureKnowledge/
- ../09_DecisionTree/

---

# 1. Purpose

Battery（电池）是便携式数字平板探测器的移动供电模块。

负责为探测器提供独立电源，在脱离外部电源环境下维持设备正常工作，并为曝光、图像采集、数据处理及通信提供持续稳定的电能。

Battery 不参与图像采集、图像处理及数据通信。

---

# 2. Scope

适用于采用可充电电池供电的数字平板探测器。

包括：

- Pluto Series（Battery Version）
- Mercu Series（Battery Version）
- 其他便携式产品

固定式产品不适用。

---

# 3. Definition

Battery 是探测器的主要能源之一。

当外部 DC 电源未接入时，Battery 作为唯一供电来源，通过 Power Board 向整机供电。

Battery 同时负责向系统提供电池状态信息，供系统进行剩余电量及供电状态管理。

Reference：

- ../02_System/PowerArchitecture.md

---

# 4. Physical Structure

Battery 系统主要包括：

- Battery Pack
- Battery Connector
- Battery Interface
- Battery Protection Circuit
- Power Output Terminal

系统位置：

```text
Battery

↓

Power Board

↓

FPGA

↓

Detector System
```

---

# 5. Internal Composition

Battery 模块包括：

- Rechargeable Battery Pack
- Battery Connector
- Protection Circuit
- Status Interface

产品资料未说明电芯类型、容量、BMS 芯片及内部拓扑，本知识库不定义具体实现。

---

# 6. Physical Principle

Battery 储存电能。

工作过程中：

Battery 输出直流电源。

Power Board 将输入电源转换为系统所需各路工作电压。

探测器所有模块均通过 Power Board 获取工作电源。

充电时：

外部充电电源为 Battery 补充电能。

Battery 不直接向各功能模块供电。

---

# 7. Working Process

```text
Battery

↓

Power Output

↓

Power Board

↓

Voltage Distribution

↓

FPGA

↓

Detector Initialization

↓

Exposure

↓

Image Acquisition

↓

Communication
```

---

# 8. Timing Relationship

Battery 工作覆盖：

- Startup
- Initialization
- Ready
- Exposure
- Readout
- Communication
- Shutdown

Battery 为整个系统持续提供电能。

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

Battery 不参与图像信号处理。

仅提供供电及状态信息。

Power Flow：

```text
Battery

↓

Power Board

↓

Detector Hardware
```

Reference：

- ../02_System/PowerArchitecture.md

---

# 10. Interface

## Input

- Charging Power（充电状态）

## Output

- DC Power
- Battery Status

## Connected Hardware

- Power Board

---

# 11. Performance Characteristics

Battery 提供：

- 独立供电
- 连续供电
- 可充电
- 移动工作能力
- 电池状态反馈

Battery 不负责：

- 电压转换
- 电源分配
- 图像处理
- 数据通信

具体容量、工作时间及充电时间应以产品规格书为准。

---

# 12. Failure Mode

可能出现的失效模式包括：

- Battery Empty
- Battery Aging
- Battery Capacity Reduction
- Battery Charging Failure
- Battery Output Failure
- Battery Connector Failure
- Battery Protection Triggered
- Battery Communication Failure（如适用）

---

# 13. Failure Mechanism

Battery 异常可能导致：

- 无法开机
- 自动关机
- 曝光过程中掉电
- 图像采集中断
- 网络连接中断
- 校准中断
- 系统频繁重启

Battery 容量下降可能导致设备工作时间明显缩短。

---

# 14. Image Manifestation

Battery 本身不会直接影响图像质量。

供电不足可能表现为：

- 无图像
- 曝光失败
- 图像采集中断
- 图像传输失败
- 校准失败
- 系统异常退出

图像异常需结合 Power Board、FPGA 等模块综合分析。

---

# 15. Diagnostic Method

建议诊断顺序：

1. 检查电池安装状态。
2. 检查电池剩余电量。
3. 检查是否能够正常充电。
4. 检查电池接口连接状态。
5. 确认系统是否识别电池。
6. 检查外部电源工作状态。
7. 检查 Power Board 输入状态。
8. 检查系统日志。
9. 根据 DecisionTree 进一步定位故障。

---

# 16. Related Calibration

Battery 不参与校准算法。

Battery 电量不足可能导致：

- Offset Calibration Failure
- Gain Calibration Failure
- Defect Calibration Failure

建议在电量充足或连接外部电源状态下执行校准。

---

# 17. Related Documents

System：

- PowerArchitecture.md
- DetectorArchitecture.md

Hardware：

- Power_Board.md
- FPGA.md

Software：

- iDetector.md

Knowledge：

- ../07_FailureKnowledge/Power/
- ../09_DecisionTree/BatteryFailure/

---

# 18. Knowledge Graph

```text
Battery
    │
    ▼
Power Board
    │
 ┌──┴────────────────────────────┐
 ▼                               ▼
FPGA                     Readout ASIC
 │                               │
 ▼                               ▼
Image Acquisition      Communication
```

---

# 19. Document Boundary

本文件负责：

- Battery 定义
- 系统供电关系
- 工作流程
- 接口关系
- 常见失效模式
- 故障定位入口

本文件不负责：

- 电池化学原理
- BMS 控制算法
- 充电器设计
- 电池维修
- 电芯拆解
- 电池安全认证

---

# 20. Reference

## Fact

- 产品用户手册中关于电池安装、充电、使用及维护要求。
- 产品培训资料中关于便携式探测器供电方式及工作流程。

## Theory

- Battery 为便携式探测器提供移动电源。
- 系统供电关系引用：

Reference：

- ../02_System/PowerArchitecture.md