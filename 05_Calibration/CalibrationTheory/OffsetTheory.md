# OffsetTheory

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
- PixelResponse.md
- GainTheory.md
- DefectTheory.md
- ../../02_System/ImagePipeline.md
- ../../03_Hardware/Photodiode.md
- ../../03_Hardware/TFT_Array.md

---

# 1. Purpose

Offset Theory 描述数字平板探测器暗场响应（Dark Response）的形成机制及 Offset Calibration 的理论基础。

Offset Calibration 的目标是在无 X-Ray 曝光条件下测量每个 Pixel 的固定输出，并在后续图像处理中进行补偿，以降低固定模式噪声，提高图像一致性。

Offset Theory 是 Offset Calibration、图像预处理及图像质量分析的重要理论基础。

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

Offset 是指在无 X-Ray 曝光条件下，Pixel 输出的数字值。

理论上，无曝光条件下 Pixel 输出应保持一致。

实际系统中，由于器件特性、模拟电路及读出链路的影响，各 Pixel 会产生固定的暗场响应。

Offset Calibration 的作用是测量该固定响应，并在图像处理中进行补偿。

---

# 4. Offset Generation

Offset 来源于整个信号链，而非单一硬件模块。

响应路径如下：

```text
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

Offset Value
```

Offset 为系统固有响应，与正常曝光图像叠加存在。

---

# 5. Physical Principle

在无 X-Ray 条件下：

Pixel 不接收曝光信号。

系统完成一次完整读出。

各 Pixel 输出固定数字值。

这些数字值构成 Offset Image。

Offset Image 记录了系统暗场响应。

---

# 6. Offset Characteristics

Offset 具有以下特点：

- 无曝光条件下获得
- 每个 Pixel 均存在对应 Offset
- Pixel 间存在差异
- 同一 Pixel 在稳定工作条件下具有较好的重复性
- Offset 可通过 Calibration 补偿

---

# 7. Offset Distribution

理想情况下：

```text
Pixel A ≈ Pixel B ≈ Pixel C ≈ Pixel D
```

实际系统中：

```text
Pixel A ≠ Pixel B ≠ Pixel C ≠ Pixel D
```

因此形成固定模式偏移。

---

# 8. Relationship with Pixel Response

Pixel Response 可表示为：

```text
Pixel Output

=

Offset

+

Exposure Response
```

因此：

图像处理中首先需要扣除 Offset，再进行后续 Gain Correction。

---

# 9. Relationship with Calibration

Offset Calibration 的目标：

- 建立 Offset Map
- 记录每个 Pixel Offset
- 图像处理中进行 Offset Correction

处理流程：

```text
Dark Image

↓

Offset Calculation

↓

Offset Table

↓

Image Correction
```

---

# 10. Image Influence

Offset 未补偿时可能导致：

- 图像整体灰度偏移
- 固定背景纹理
- 固定模式噪声
- 图像均匀性下降
- 图像对比度下降

Offset 补偿后：

图像背景一致性提高。

---

# 11. Failure Manifestation

Offset 异常可能表现为：

- Offset Calibration Failure
- Offset Table Error
- Background Nonuniformity
- Fixed Pattern Noise
- Image Background Offset

---

# 12. Diagnostic Significance

当出现以下现象时，应检查 Offset：

- 背景灰度异常
- 图像固定纹理
- 校准失败
- 图像整体偏亮
- 图像整体偏暗

同时结合 Gain Calibration 结果进行综合分析。

---

# 13. Relationship with Other Calibration

校准顺序如下：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

Offset Calibration 是后续校准的基础。

---

# 14. Knowledge Graph

```text
Dark Image

↓

Pixel Response

↓

Offset

↓

Offset Calibration

↓

Offset Table

↓

Image Correction
```

---

# 15. Related Documents

Calibration：

- CalibrationOverview.md
- PixelResponse.md
- GainTheory.md
- DefectTheory.md

Hardware：

- Photodiode.md
- TFT_Array.md

System：

- ImagePipeline.md

---

# 16. Document Boundary

本文件负责：

- Offset 定义
- Offset 形成机制
- Offset 特性
- Offset 对图像影响
- Offset 与 Calibration 的关系

本文件不负责：

- Offset Calibration 操作流程
- Offset 文件格式
- Offset 参数配置
- Offset SOP

上述内容分别由 Offset 模块进行说明。

---

# 17. Reference

## Fact

- 产品培训资料关于暗场采集、Pixel 输出及图像校准流程。

## Theory

- Offset 为无曝光条件下 Pixel 固定响应。
- Offset Calibration 用于建立 Offset Table，并在图像处理中完成 Offset Correction。