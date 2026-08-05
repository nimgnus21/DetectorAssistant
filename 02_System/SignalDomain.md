# Signal Domain

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
- TimingArchitecture.md
- ImagePipeline.md
- ../03_Hardware/Scintillator/README.md
- ../03_Hardware/Photodiode/README.md
- ../03_Hardware/TFT_Array/README.md
- ../03_Hardware/Gate_Driver/README.md
- ../03_Hardware/Readout_ASIC/README.md
- ../03_Hardware/ADC/README.md
- ../03_Hardware/FPGA/README.md

---

# 1. Purpose

Signal Domain 定义数字平板探测器内部信号在不同物理域之间的转换关系。

本文件描述信号类型、信号边界、信号转换路径及各信号域之间的关系，不描述各硬件模块内部实现。

---

# 2. Scope

适用于所有采用 TFT 平板探测器架构的产品。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

本文件作为系统层信号模型，供 Hardware、Calibration、ImageDiagnosis、FailureKnowledge 统一引用。

---

# 3. Signal Domain Overview

数字平板探测器内部信号按照物理属性划分为六个信号域。

```
X-Ray Domain
        │
        ▼
Optical Domain
        │
        ▼
Charge Domain
        │
        ▼
Analog Domain
        │
        ▼
Digital Domain
        │
        ▼
Communication Domain
```

每个信号域之间通过对应硬件完成转换。

---

# 4. Signal Domain Definition

| Domain | Signal Type | Converter | Output |
|---------|-------------|-----------|--------|
| X-Ray Domain | X-Ray Photon | Scintillator | Visible Light |
| Optical Domain | Visible Light | Photodiode | Electrical Charge |
| Charge Domain | Stored Charge | TFT + Readout ASIC | Analog Signal |
| Analog Domain | Analog Voltage | ADC | Digital Pixel Data |
| Digital Domain | Digital Image Data | FPGA | Image Frame |
| Communication Domain | Network Packet | Ethernet Interface | Workstation |

---

# 5. Domain Description

## 5.1 X-Ray Domain

### Definition

探测器接收来自 X-Ray Source 的 X 射线光子。

### Signal Carrier

X-Ray Photon

### Input

人体衰减后的 X-Ray。

### Output

Scintillator 接收 X-Ray。

### Boundary

开始于 X-Ray 入射。

结束于闪烁体完成能量转换。

### Related Hardware

- Scintillator

---

## 5.2 Optical Domain

### Definition

闪烁体将 X-Ray 转换为可见光。

### Signal Carrier

Visible Light

### Input

X-Ray Energy

### Output

Visible Light

### Boundary

开始于 Scintillator。

结束于 Photodiode。

### Related Hardware

- Scintillator
- Photodiode

---

## 5.3 Charge Domain

### Definition

Photodiode 将可见光转换为电荷并存储于像素单元。

### Signal Carrier

Electrical Charge

### Input

Visible Light

### Output

Stored Charge

### Boundary

开始于 Photodiode。

结束于 Readout ASIC 输入端。

### Related Hardware

- Photodiode
- TFT Array
- Gate Driver

---

## 5.4 Analog Domain

### Definition

像素电荷经读出后形成模拟信号。

### Signal Carrier

Analog Voltage

### Input

Stored Charge

### Output

Analog Signal

### Boundary

开始于 Readout ASIC。

结束于 ADC 输入端。

### Related Hardware

- Readout ASIC
- ADC

---

## 5.5 Digital Domain

### Definition

ADC 将模拟信号转换为数字像素数据。

### Signal Carrier

Digital Pixel Data

### Input

Analog Signal

### Output

Digital Image

### Boundary

开始于 ADC。

结束于 FPGA 输出完整图像。

### Related Hardware

- ADC
- FPGA
- DDR

---

## 5.6 Communication Domain

### Definition

数字图像封装并发送至工作站。

### Signal Carrier

Ethernet Packet

### Input

Image Frame

### Output

Image Data

### Boundary

开始于 FPGA。

结束于 Workstation。

### Related Hardware

- Ethernet Controller
- Network Interface

---

# 6. Signal Conversion Chain

| From | To | Converter |
|------|----|-----------|
| X-Ray Domain | Optical Domain | Scintillator |
| Optical Domain | Charge Domain | Photodiode |
| Charge Domain | Analog Domain | TFT Array + Readout ASIC |
| Analog Domain | Digital Domain | ADC |
| Digital Domain | Communication Domain | FPGA + Ethernet Controller |

---

# 7. Signal Boundary

| Boundary | Start | End |
|----------|-------|-----|
| Radiation Boundary | X-Ray Source | Scintillator |
| Optical Boundary | Scintillator | Photodiode |
| Charge Boundary | Photodiode | Readout ASIC |
| Analog Boundary | Readout ASIC | ADC |
| Digital Boundary | ADC | FPGA |
| Network Boundary | FPGA | Workstation |

---

# 8. Signal Characteristics

| Domain | Storage | Sequence | Persistence |
|---------|---------|----------|-------------|
| X-Ray Domain | No | Instantaneous | No |
| Optical Domain | No | Instantaneous | No |
| Charge Domain | Pixel | Exposure Period | Temporary |
| Analog Domain | No | Row Readout | Instantaneous |
| Digital Domain | Memory Buffer | Frame Based | Temporary |
| Communication Domain | Packet Buffer | Packet Based | Temporary |

---

# 9. Relationship With Timing

Signal Domain 与 Timing Architecture 对应关系如下。

| Timing State | Active Domain |
|--------------|---------------|
| Idle | None |
| Exposure | X-Ray Domain、Optical Domain、Charge Domain |
| Readout | Charge Domain、Analog Domain、Digital Domain |
| Transfer | Communication Domain |

Reference：

TimingArchitecture.md

---

# 10. Relationship With Image Pipeline

Image Pipeline 从 Digital Domain 开始。

Signal Domain 负责生成数字图像。

Image Pipeline 负责数字图像校正。

Reference：

ImagePipeline.md

---

# 11. Relationship With Calibration

Calibration 仅作用于 Digital Domain。

包括：

- Offset Calibration
- Gain Calibration
- Defect Calibration

Reference：

../05_Calibration/

---

# 12. Failure Mapping

| Signal Domain | Possible Failure | Related Knowledge |
|---------------|------------------|-------------------|
| X-Ray Domain | X-Ray Dose Abnormal | FailureKnowledge |
| Optical Domain | Light Conversion Abnormal | ImageDiagnosis |
| Charge Domain | Charge Leakage / Charge Loss | ImageDiagnosis |
| Analog Domain | Analog Noise | FailureKnowledge |
| Digital Domain | Data Error | FailureKnowledge |
| Communication Domain | Packet Loss | Communication |

---

# 13. Knowledge Relationship

```
DetectorArchitecture
        │
        ▼
SignalDomain
        │
        ├────────► TimingArchitecture
        │
        ├────────► ImagePipeline
        │
        ├────────► Calibration
        │
        ├────────► Hardware
        │
        ├────────► FailureKnowledge
        │
        └────────► ImageDiagnosis
```

---

# 14. Document Boundary

本文件负责：

- 信号域定义
- 信号边界
- 信号转换关系
- 信号流向
- 系统引用关系

本文件不负责：

- 硬件工作原理
- 电路设计
- 校准算法
- 图像处理算法
- 故障处理流程
- SOP 操作步骤

---

# 15. Reference

## Fact

- Mammo1012C 用户手册：产品系统组成、使用范围、安全要求。:contentReference[oaicite:0]{index=0}
- Mammo1012X 用户手册：产品安装、运行环境及系统使用要求。:contentReference[oaicite:1]{index=1}

## Theory

- 数字 X 射线探测器培训资料：X 射线成像原理、闪烁体、光电二极管、TFT 读出、Readout ASIC、ADC、FPGA、逐行读出流程。（依据已提供培训资料）