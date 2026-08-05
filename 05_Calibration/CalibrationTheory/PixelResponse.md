# PixelResponse

Version: V2.0

Module: Calibration Theory

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- CalibrationOverview.md
- OffsetTheory.md
- GainTheory.md
- DefectTheory.md
- ../../02_System/ImagePipeline.md
- ../../02_System/SignalDomain.md
- ../../03_Hardware/Scintillator.md
- ../../03_Hardware/Photodiode.md
- ../../03_Hardware/TFT_Array.md

---

# 1. Purpose

Pixel Response（像素响应）描述数字平板探测器中单个像素对 X-Ray 辐射产生响应并输出数字灰度值的全过程。

Pixel Response 是数字平板探测器成像质量评价及校准体系的理论基础。

Offset Calibration、Gain Calibration 及 Defect Calibration 均建立在 Pixel Response 的一致性基础之上。

---

# 2. Scope

适用于采用间接转换（Indirect Conversion）结构的数字平板探测器。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Definition

Pixel Response 是指单个 Pixel 在受到 X-Ray 照射后，从能量吸收、光电转换、电荷积分、信号读出到最终数字灰度输出的完整响应过程。

对于相同曝光条件，理想情况下所有 Pixel 应具有一致的响应特性。

Pixel Response 包括：

- X-Ray Response
- Optical Response
- Charge Response
- Electrical Response
- Digital Response

最终表现为 Pixel Digital Value。

---

# 4. Signal Chain

Pixel Response 沿图像信号链产生。

响应路径如下：

```text
X-Ray

↓

Scintillator

↓

Visible Light

↓

Photodiode

↓

Charge

↓

TFT Array

↓

Readout ASIC

↓

ADC

↓

FPGA

↓

Image Data
```

每一级都会影响最终 Pixel Response。

Reference：

- ../../02_System/ImagePipeline.md

---

# 5. Response Generation

Pixel Response 的形成过程包括：

## Step 1

X-Ray 入射 Scintillator。

Scintillator 吸收 X-Ray 能量。

转换为 Visible Light。

↓

## Step 2

Photodiode 接收 Visible Light。

发生光电转换。

产生 Charge。

↓

## Step 3

Charge 在 Pixel 内积分。

曝光结束后保存。

↓

## Step 4

Gate Driver 控制 TFT 导通。

Charge 被释放。

↓

## Step 5

Readout ASIC 接收 Charge。

转换为模拟电压。

↓

## Step 6

ADC 完成模数转换。

↓

## Step 7

FPGA 输出 Pixel Digital Value。

---

# 6. Pixel Response Characteristics

Pixel Response 包括以下特性：

## Response Level

Pixel 输出灰度值。

## Response Uniformity

不同 Pixel 对相同曝光条件具有一致响应。

## Response Stability

同一 Pixel 在重复曝光下保持稳定输出。

## Response Linearity

Pixel 输出随曝光剂量变化保持一致关系。

## Response Repeatability

连续曝光响应一致。

---

# 7. Pixel Response Consistency

数字平板探测器要求：

相同曝光条件下：

```text
Pixel A

≈

Pixel B

≈

Pixel C

≈

Pixel D
```

若 Pixel Response 不一致，将导致：

- 图像亮度异常
- 图像均匀性下降
- 固定噪声增加
- 局部响应异常

因此需要 Calibration 进行补偿。

---

# 8. Factors Affecting Pixel Response

影响 Pixel Response 的因素包括：

## X-Ray

- 剂量
- 能量
- 曝光时间

## Scintillator

- 光转换效率

## Photodiode

- 光电转换效率

## TFT Array

- Charge 保持能力
- Charge Transfer

## Readout ASIC

- 模拟信号读出

## ADC

- 模数转换

## FPGA

- 数据处理

任何一级异常均可能改变 Pixel Response。

---

# 9. Relationship with Calibration

Calibration 的目标是提高 Pixel Response 的一致性。

对应关系如下：

| Calibration | 修正对象 | 目标 |
|--------------|----------|------|
| Offset Calibration | 暗场响应 | 消除固定偏移 |
| Gain Calibration | 响应增益 | 提高均匀性 |
| Defect Calibration | 异常 Pixel | 屏蔽异常响应 |

Pixel Response 是三类 Calibration 的共同理论基础。

---

# 10. Response Categories

根据曝光条件，Pixel Response 可分为：

## Dark Response

无 X-Ray 条件下 Pixel 输出。

用于 Offset Calibration。

---

## Flat Field Response

均匀曝光条件下 Pixel 输出。

用于 Gain Calibration。

---

## Defect Response

Pixel 输出明显偏离正常范围。

用于 Defect Calibration。

---

# 11. Image Manifestation

Pixel Response 异常可能表现为：

- Image Offset
- Bright Pixel
- Dark Pixel
- Bad Column
- Bad Row
- Nonuniformity
- Noise
- Image Artifact

具体表现由异常位置及异常程度决定。

Reference：

- ../../08_ImageDiagnosis/

---

# 12. Diagnostic Significance

Pixel Response 是分析图像异常的重要依据。

通过分析 Pixel Response，可判断：

- 是否存在 Offset 异常
- 是否存在 Gain 不一致
- 是否存在 Defect Pixel
- 是否需要重新 Calibration

Pixel Response 也是 Decision Tree 的核心判断依据。

---

# 13. Related Calibration

Pixel Response 与以下校准直接相关：

- Offset Calibration
- Gain Calibration
- Defect Calibration

理论关系：

```text
Pixel Response

├── Offset Theory

├── Gain Theory

└── Defect Theory
```

---

# 14. Knowledge Graph

```text
X-Ray

↓

Scintillator

↓

Photodiode

↓

Charge

↓

TFT Array

↓

Readout ASIC

↓

ADC

↓

FPGA

↓

Pixel Response

├────────► Offset Calibration

├────────► Gain Calibration

└────────► Defect Calibration
```

---

# 15. Related Documents

Calibration：

- CalibrationOverview.md
- OffsetTheory.md
- GainTheory.md
- DefectTheory.md

System：

- ../../02_System/ImagePipeline.md
- ../../02_System/SignalDomain.md

Hardware：

- ../../03_Hardware/Scintillator.md
- ../../03_Hardware/Photodiode.md
- ../../03_Hardware/TFT_Array.md

---

# 16. Document Boundary

本文件负责：

- Pixel Response 定义
- Pixel Response 形成过程
- Pixel Response 特性
- Pixel Response 一致性
- Pixel Response 与 Calibration 的关系

本文件不负责：

- Offset 校准算法
- Gain 校准算法
- Defect 校准算法
- 图像处理算法
- 校准操作流程

上述内容分别由对应理论文档进行说明。

---

# 17. Reference

## Fact

- 《探测器工作原理1.1》关于 X-Ray → Visible Light → Charge → Readout → Digital Image 的成像过程。
- 产品培训资料关于 Pixel 信号形成及读出流程。

## Theory

- Pixel Response 是数字平板探测器图像形成及校准理论的基础。
- Offset、Gain、Defect Calibration 均以 Pixel Response 一致性为目标。