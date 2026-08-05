# TFT Array

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
- Gate_Driver.md
- Readout_ASIC.md
- Scintillator.md
- Photodiode.md
- ../08_ImageDiagnosis/
- ../07_FailureKnowledge/

---

# 1. Purpose

TFT Array（Thin Film Transistor Array）是数字平板探测器的核心成像阵列。

其作用是在曝光期间完成像素电荷存储，在读出期间通过 Gate Driver 的逐行扫描控制，将像素电荷输出至 Readout ASIC，实现整幅图像的数据采集。

---

# 2. Scope

适用于采用 a-Si TFT 有源矩阵（AMA，Active Matrix Array）结构的数字平板探测器。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

产品手册说明，上述产品采用非晶硅（a-Si）TFT 图像传感器。

---

# 3. Definition

TFT Array 是由大量像素单元组成的二维有源矩阵。

每个像素单元包含光电转换后的电荷存储结构及 TFT 开关，通过 Gate Line 与 Data Line 构成矩阵，实现逐行扫描、逐列读出的图像采集方式。

---

# 4. Physical Structure

TFT Array 主要由以下部分组成：

- Pixel Unit（像素单元）
- TFT（薄膜晶体管）
- Photodiode（光电二极管）
- Gate Line（栅极线）
- Data Line（数据线）
- Active Area（有效成像区域）

培训资料将其描述为 Active Matrix Array（AMA）结构。

---

# 5. Internal Composition

每个 Pixel Unit 包括：

- Photodiode
- TFT Switch
- Pixel Electrode
- Charge Storage Node

多个 Pixel Unit 组成完整二维阵列。

Gate Line 控制行扫描。

Data Line 负责列方向信号输出。

---

# 6. Physical Principle

曝光期间：

Photodiode 将闪烁体产生的可见光转换为电荷。

TFT 保持截止状态。

电荷保存在像素节点。

读出期间：

Gate Driver 输出 Gate Pulse。

对应行 TFT 同时导通。

像素电荷经 Data Line 输出至 Readout ASIC。

Readout ASIC 完成模拟信号采集。

全部行扫描完成后形成完整图像。

---

# 7. Working Process

```text
X-Ray Exposure

↓

Scintillator

↓

Photodiode

↓

Charge Storage

↓

Gate Driver Enable

↓

Current Row TFT ON

↓

Charge Output

↓

Data Line

↓

Readout ASIC

↓

ADC

↓

FPGA

↓

Next Row

↓

Frame Complete
```

---

# 8. Timing Relationship

曝光阶段：

所有 TFT 保持关闭。

像素持续积分。

读出阶段：

Gate Driver 按行依次开启 TFT。

每次仅一行导通。

完成当前行采集后切换下一行。

全部行完成后结束一次 Frame Readout。

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

输入：

- Optical Signal
- Gate Pulse

输出：

- Pixel Charge
- Analog Signal（经 Readout ASIC）

Signal Flow：

```text
Optical Signal

↓

Photodiode

↓

Charge Storage

↓

TFT ON

↓

Data Line

↓

Readout ASIC
```

Reference：

- ../02_System/SignalDomain.md

---

# 10. Interface

## Input

- Optical Signal（来自 Photodiode）
- Gate Pulse（来自 Gate Driver）

## Output

- Pixel Charge
- Data Line Signal

## Connected Hardware

- Scintillator
- Photodiode
- Gate Driver
- Readout ASIC

---

# 11. Performance Characteristics

主要特性：

- Active Matrix Array（AMA）
- 行扫描（Row Scan）
- 列数据输出（Column Readout）
- 像素独立存储
- 高空间分辨率
- 支持大面积阵列

具体像素尺寸、有效成像区域及分辨率应以产品规格书为准。

---

# 12. Failure Mode

培训资料及产品手册涉及的相关失效包括：

- TFT 损坏
- Gate Line 异常
- Data Line 异常
- Pixel 异常
- Charge Leakage
- Charge Retention Abnormal

其中产品手册明确列出 TFT 损坏相关故障。

---

# 13. Failure Mechanism

可能导致 TFT Array 工作异常的因素包括：

- TFT 无法正常导通
- TFT 无法正常截止
- Gate Line 无法正确驱动
- Data Line 信号异常
- 像素电荷未正常读出
- 像素电荷保持异常

具体机理分析应结合 Gate Driver、Readout ASIC 及现场检测结果进行综合判断。培训资料主要说明了读出机制，未进一步展开各类失效机理。

---

# 14. Image Manifestation

TFT Array 异常可能表现为：

- 行异常（Row Abnormal）
- 列异常（Column Abnormal）
- 局部图像缺失
- 图像固定缺陷
- 图像读出异常

产品手册明确指出 TFT 损坏可导致图像异常。

详细分析见：

- ../08_ImageDiagnosis/

---

# 15. Diagnostic Method

建议诊断顺序：

1. 确认曝光正常。
2. 确认 Gate Driver 输出正常。
3. 确认对应 Gate Line 工作状态。
4. 检查 Data Line 是否存在异常。
5. 检查 Readout ASIC 是否正常采集。
6. 根据图像异常定位影响范围。
7. 结合系统日志及校准结果综合判断。

具体检测流程由故障知识库与决策树定义。

---

# 16. Related Calibration

TFT Array 不执行校准算法。

其工作状态直接影响：

- Offset Calibration
- Gain Calibration
- Defect Calibration

当 TFT Array 存在异常时，校准结果可能失效或出现异常图像。

Reference：

- ../05_Calibration/

---

# 17. Related Documents

System：

- DetectorArchitecture.md
- SignalDomain.md
- TimingArchitecture.md

Hardware：

- Gate_Driver.md
- Readout_ASIC.md
- Photodiode.md
- Scintillator.md

Knowledge：

- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/
- ../09_DecisionTree/

---

# 18. Reference

## Fact

- 《探测器工作原理1.1》：AMA（Active Matrix Array）结构、TFT 像素结构、Gate Line、Data Line、逐行扫描及电荷读出过程。
- 产品手册：采用 a-Si TFT 图像传感器，包含 Active Area、像素规格及相关参数。
- 产品手册：TFT 损坏相关故障说明。

## Theory

- 培训资料关于 TFT 有源矩阵工作原理、逐行扫描机制及像素电荷读出流程。