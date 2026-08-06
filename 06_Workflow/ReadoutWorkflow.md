# ReadoutWorkflow

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
- AcquisitionWorkflow.md
- CalibrationWorkflow.md
- ../02_System/SignalFlow.md
- ../03_Hardware/Readout_ASIC.md
- ../03_Hardware/FPGA.md
- ../03_Hardware/TFT_Array.md
- README.md

---

# 1. Purpose

Readout Workflow 定义数字平板探测器（Flat Panel Detector，FPD）完成 Pixel 电荷采集后，将模拟信号转换为数字图像数据的标准流程。

本流程负责模拟信号接收、信号调理、模数转换（ADC）、数据缓存及数据输出，为 Calibration Workflow 提供原始数字图像（Raw Image）。

---

# 2. Scope

适用于：

- TFT Flat Panel Detector
- Wired Detector
- Wireless Detector

适用于所有采用 Readout ASIC + FPGA 架构的探测器。

---

# 3. Workflow Objectives

Readout Workflow 的主要目标包括：

- 接收模拟像素信号
- 放大并稳定模拟信号
- 执行模拟采样
- 完成 ADC 转换
- 输出数字图像数据
- 建立 Raw Image Buffer

---

# 4. Workflow Overview

```text
Acquisition Complete

↓

Analog Signal Input

↓

Signal Conditioning

↓

Sampling

↓

ADC Conversion

↓

Digital Data Output

↓

FPGA Buffer

↓

Frame Assembly

↓

Raw Image

↓

Calibration Workflow
```

---

# 5. Workflow Inputs

输入包括：

- Analog Pixel Signal
- Row Scan Timing
- Readout Clock
- FPGA Clock
- ADC Reference Voltage

---

# 6. Analog Signal Input

Readout ASIC 接收来自 Data Line 的模拟信号。

输入来源：

- Column Data Line
- Pixel Analog Voltage

ASIC 建立输入缓冲并准备采样。

输出：

Analog Input Ready

---

# 7. Signal Conditioning

ASIC 对模拟信号进行调理。

包括：

- Input Buffer
- Signal Amplification
- Offset Compensation（硬件级）
- Common Mode Processing
- Noise Suppression

目标：

提高信号稳定性，为 ADC 提供最佳输入。

输出：

Conditioned Analog Signal

---

# 8. Signal Sampling

ASIC 按照采样时序保持模拟电压。

包括：

- Sample
- Hold
- Channel Switching
- Multiplexer Control

确保每一路信号均正确采样。

输出：

Sampled Signal

---

# 9. ADC Conversion

模拟信号转换为数字信号。

主要过程：

```text
Analog Voltage

↓

ADC Sampling

↓

Quantization

↓

Digital Output
```

ADC 输出数字灰度值。

输出：

Digital Pixel Data

---

# 10. Digital Data Transfer

数字数据传输至 FPGA。

包括：

- Parallel Interface
- LVDS（如适用）
- Data Clock
- Synchronization Signal

FPGA 接收所有列数据。

输出：

Digital Data Stream

---

# 11. Frame Assembly

FPGA 完成整帧数据组织。

包括：

- Row Ordering
- Column Ordering
- Frame Synchronization
- Buffer Management

生成完整 Raw Frame。

输出：

Raw Frame Buffer

---

# 12. Readout Completion

完成本次读出。

包括：

- Frame Complete
- Readout Status Update
- Buffer Ready
- Interrupt Notify（如适用）

输出：

Raw Image Ready

---

# 13. Workflow Outputs

Readout Workflow 输出：

- Raw Image
- Raw Frame Buffer
- Frame Status
- Readout Complete

进入：

Calibration Workflow

---

# 14. State Transition

```text
ACQUISITION COMPLETE

↓

SIGNAL INPUT

↓

SIGNAL CONDITIONING

↓

SAMPLING

↓

ADC

↓

DIGITAL OUTPUT

↓

FRAME BUFFER

↓

READOUT COMPLETE

↓

CALIBRATION
```

---

# 15. Timing Relationship

```text
AcquisitionWorkflow

↓

ReadoutWorkflow

├── Analog Input
├── Signal Conditioning
├── Sampling
├── ADC Conversion
├── FPGA Receive
└── Frame Assembly

↓

CalibrationWorkflow
```

---

# 16. Common Readout Failure

| Failure | Description |
|----------|-------------|
| ASIC Not Responding | ASIC 无响应 |
| ADC Failure | ADC 转换异常 |
| Sampling Error | 采样错误 |
| Readout Clock Error | Readout Clock 异常 |
| LVDS Error | 数据接口异常 |
| FPGA Buffer Overflow | FPGA Buffer 溢出 |
| Frame Incomplete | 图像帧不完整 |
| Synchronization Error | 同步异常 |
| Column Data Error | 列数据异常 |
| Readout Timeout | 读出超时 |

详细处理参见：

- WorkflowTroubleshooting.md
- 07_FailureKnowledge/ReadoutFailure.md（规划中）

---

# 17. Engineering Notes

工程建议：

- Readout Clock 必须与 Gate Scan 保持严格同步。
- ADC Reference Voltage 应保持稳定。
- FPGA 应校验每帧数据完整性。
- Frame Buffer 应避免覆盖未处理数据。
- 所有读出异常应记录错误日志及错误代码。

---

# 18. Relationship with Other Modules

## Acquisition Workflow

提供：

- Analog Pixel Signal
- Row Scan Timing

---

## Hardware

负责：

- Readout ASIC
- ADC
- FPGA
- Data Interface

---

## Software

负责：

- Readout Control
- Buffer Management
- Status Monitoring

---

## Calibration Workflow

Readout 完成后，Raw Image 输入 Calibration Workflow，执行 Offset、Gain、Defect 等图像校正。

---

# 19. Document Boundary

本文件负责：

- 模拟信号输入
- 信号调理
- 模拟采样
- ADC 转换
- 数字数据传输
- Frame 组装
- Raw Image 输出

本文件不负责：

- Offset Calibration
- Gain Calibration
- Defect Correction
- Image Enhancement
- Image Transmission

上述内容由后续 Workflow 文档负责。

---

# 20. Knowledge Graph

```text
Acquisition Complete

↓

Analog Signal Input

↓

Signal Conditioning

↓

Sampling

↓

ADC Conversion

↓

Digital Data Output

↓

FPGA Buffer

↓

Frame Assembly

↓

Raw Image

↓

Calibration Workflow
```

---

# 21. Summary

Readout Workflow 定义 Detector 将采集到的模拟像素信号转换为数字图像数据的全过程，包括模拟信号调理、采样保持、ADC 转换、数字数据传输及帧组装。完成本流程后生成完整的 Raw Image，为 Calibration Workflow 提供未经校正的原始图像数据，是连接硬件采集与图像校正的重要环节。