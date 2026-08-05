# FPGA

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
- Readout_ASIC.md
- ADC.md
- DDR.md
- Ethernet_Controller.md
- ../04_Software/Firmware.md
- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/

---

# 1. Purpose

FPGA（Field Programmable Gate Array）是数字平板探测器数字控制核心。

负责协调整机工作时序，接收 ADC 输出的数字像素数据，完成数据缓存、逻辑控制及图像输出，并协调各硬件模块完成一次完整图像采集流程。

FPGA 不负责 X-Ray 信号转换及模拟信号处理。

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

FPGA 位于数字处理链路中心。

负责连接：

- Gate Driver
- ADC
- DDR
- Ethernet Controller
- WiFi Module（适用型号）
- MCU（适用型号）

FPGA 是探测器数字系统的统一控制中心。

培训资料中，FPGA 位于 ADC 后级，负责数字图像数据处理及控制流程。

---

# 4. Physical Structure

FPGA 位于数字控制板。

主要连接：

- ADC
- DDR
- Ethernet Controller
- Gate Driver
- Power Board

系统位置：

```text
ADC

↓

FPGA

├──── Gate Driver

├──── DDR

├──── Ethernet

└──── Firmware
```

---

# 5. Internal Composition

根据培训资料，FPGA 承担数字逻辑控制功能。

主要组成包括：

- Timing Logic
- Data Buffer
- Image Control Logic
- Communication Control
- Hardware Interface

培训资料未说明 FPGA 内部逻辑资源结构，因此本知识库不定义具体 RTL 或 IP Core。

---

# 6. Physical Principle

FPGA 在系统启动后进入初始化状态。

工作过程中：

- 接收系统触发信号。
- 控制 Gate Driver 按时序扫描。
- 接收 ADC 输出数字数据。
- 完成数据缓存。
- 输出图像至通信模块。

整个流程受 FPGA 时序逻辑统一控制。

---

# 7. Working Process

```text
Power On

↓

FPGA Initialization

↓

Receive Trigger

↓

Generate Timing

↓

Control Gate Driver

↓

Receive ADC Data

↓

Image Buffer

↓

Image Output

↓

Communication

↓

Ready
```

---

# 8. Timing Relationship

FPGA 覆盖整个采集周期。

主要参与状态：

- Initialization
- Ready
- Exposure Control
- Readout
- Image Buffer
- Image Transfer

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

输入：

- Digital Pixel Data
- Trigger Signal
- Control Signal

输出：

- Timing Signal
- Image Frame
- Communication Data

Signal Flow：

```text
ADC

↓

Digital Pixel Data

↓

FPGA

↓

Image Frame

↓

Communication
```

Reference：

- ../02_System/SignalDomain.md

---

# 10. Interface

## Input

- ADC Data
- Trigger
- Configuration
- Clock

## Output

- Gate Driver Timing
- Image Data
- Communication Data

## Connected Hardware

- ADC
- Gate Driver
- DDR
- Ethernet Controller
- WiFi Module

---

# 11. Performance Characteristics

FPGA 负责：

- 时序控制
- 数据缓存
- 图像组织
- 通信控制
- 多模块协调

性能参数应以产品型号及 FPGA 配置文件为准。

---

# 12. Failure Mode

可能出现的失效模式包括：

- FPGA Initialization Failure
- Firmware Load Failure
- Timing Generation Failure
- Data Buffer Failure
- Image Output Failure
- Communication Control Failure
- Clock Failure
- Configuration Error

---

# 13. Failure Mechanism

FPGA 异常可能导致：

- 无法曝光
- 无法读出
- 图像无法生成
- 图像数据错误
- 图像传输失败
- 系统无法启动
- 工作流程中断

具体逻辑故障需结合 Firmware、日志及硬件测试综合分析。

---

# 14. Image Manifestation

FPGA 异常可能表现为：

- 黑屏
- 无图像
- 图像不完整
- 图像冻结
- 图像重复
- 图像帧错乱
- 图像无法发送

具体表现需结合 ADC、DDR、通信模块进行综合判断。

---

# 15. Diagnostic Method

建议诊断顺序：

1. 确认系统正常上电。
2. 检查 FPGA 初始化状态。
3. 检查 Firmware 是否正常加载。
4. 检查 Trigger 是否正常接收。
5. 检查 Gate Driver 时序输出。
6. 检查 ADC 数据输入。
7. 检查 DDR 数据缓存。
8. 检查通信接口输出。
9. 结合日志及故障树进行分析。

---

# 16. Related Calibration

FPGA 不执行校准算法。

FPGA 为 Calibration 提供：

- 图像数据
- 时序控制
- 数据缓存

FPGA 异常可能导致：

- Offset Calibration Failure
- Gain Calibration Failure
- Defect Calibration Failure

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

- ADC.md
- Gate_Driver.md
- DDR.md
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
Trigger
    │
    ▼
FPGA
 ├────────► Gate Driver
 ├────────► ADC
 ├────────► DDR
 ├────────► Ethernet
 └────────► Firmware
```

---

# 19. Document Boundary

本文件负责：

- FPGA 定义
- 系统位置
- 数字控制职责
- 工作流程
- 时序关系
- 接口关系
- 常见失效模式
- 图像影响
- 故障定位入口

本文件不负责：

- FPGA HDL 代码
- Firmware 开发
- IP Core 实现
- 图像算法
- 芯片维修

---

# 20. Reference

## Fact

- 《探测器工作原理1.1》：数字图像采集流程及 FPGA 在读出链路中的位置。

## Theory

- 培训资料关于 FPGA 数字控制、时序管理及图像输出流程。