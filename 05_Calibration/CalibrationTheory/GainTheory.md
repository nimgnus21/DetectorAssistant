# GainTheory

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
- OffsetTheory.md
- DefectTheory.md
- ../../02_System/ImagePipeline.md
- ../../03_Hardware/Scintillator.md
- ../../03_Hardware/Photodiode.md
- ../../03_Hardware/TFT_Array.md

---

# 1. Purpose

Gain Theory 描述数字平板探测器 Pixel 对相同 X-Ray 曝光条件产生不同响应的原因，以及 Gain Calibration 的理论基础。

Gain Calibration 的目标是在均匀曝光条件下测量每个 Pixel 的响应差异，通过建立 Gain Correction 数据，使整个探测器输出具有一致的响应，提高图像均匀性。

Gain Theory 是 Gain Calibration、均匀性校正及图像质量分析的重要理论基础。

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

Gain 是 Pixel 对相同曝光条件下响应能力的相对大小。

理论上：

所有 Pixel 在相同曝光剂量下应输出一致的数字值。

实际系统中：

由于器件特性及信号链差异，各 Pixel 响应存在差异。

Gain Calibration 的目标就是消除这种差异。

---

# 4. Gain Generation

Gain 差异来源于整个成像链。

主要包括：

```text
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
```

任何一级响应差异都会最终表现为 Gain Difference。

---

# 5. Physical Principle

在均匀 X-Ray 曝光条件下：

所有 Pixel 接收相同剂量 X-Ray。

理论输出应一致。

实际由于响应效率不同：

不同 Pixel 输出不同数字值。

Gain Calibration 建立 Gain Correction Table。

图像处理阶段按照对应 Gain 值进行补偿。

---

# 6. Gain Characteristics

Gain 具有以下特点：

- 在均匀曝光条件下测量
- 每个 Pixel 具有独立 Gain
- Pixel 间存在响应差异
- Gain 相对稳定
- 可通过 Calibration 补偿

---

# 7. Gain Uniformity

理想情况下：

```text
Pixel A

=

Pixel B

=

Pixel C

=

Pixel D
```

实际系统：

```text
Pixel A

≠

Pixel B

≠

Pixel C

≠

Pixel D
```

Gain Calibration 的目标是使校正后输出趋于一致。

---

# 8. Relationship with Pixel Response

Pixel Response 可表示为：

```text
Pixel Output

=

(Exposure Response × Gain)

+

Offset
```

图像处理流程：

```text
Offset Correction

↓

Gain Correction

↓

Corrected Image
```

---

# 9. Relationship with Calibration

Gain Calibration 建立：

Gain Table。

后续图像按照对应 Gain 系数完成响应补偿。

流程如下：

```text
Flat Field Image

↓

Gain Calculation

↓

Gain Table

↓

Image Correction
```

---

# 10. Image Influence

Gain 未校正时可能表现为：

- 图像不均匀
- 明暗区域
- Fixed Pattern
- Shading
- Response Difference

Gain Correction 后：

图像均匀性提高。

---

# 11. Failure Manifestation

Gain 异常可能表现为：

- Gain Calibration Failure
- Gain Table Error
- Image Nonuniformity
- Bright Area
- Dark Area
- Shading Artifact

---

# 12. Diagnostic Significance

当出现以下现象时应检查 Gain：

- 图像均匀性下降
- 平场出现明暗区域
- Gain Calibration Failure
- Calibration 后图像无改善
- 大面积响应异常

同时应结合 Offset 及 Defect Calibration 综合分析。

---

# 13. Relationship with Other Calibration

理论关系如下：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

Gain Calibration 建立在 Offset Correction 基础之上。

---

# 14. Knowledge Graph

```text
Uniform X-Ray

↓

Pixel Response

↓

Gain Difference

↓

Gain Calibration

↓

Gain Table

↓

Uniform Image
```

---

# 15. Related Documents

Calibration：

- CalibrationOverview.md
- PixelResponse.md
- OffsetTheory.md
- DefectTheory.md

Hardware：

- Scintillator.md
- Photodiode.md
- TFT_Array.md

System：

- ImagePipeline.md

---

# 16. Document Boundary

本文件负责：

- Gain 定义
- Gain 形成机制
- Gain 特性
- Gain 对图像影响
- Gain 与 Calibration 的关系

本文件不负责：

- Gain Calibration 操作流程
- Gain 文件格式
- Gain 参数配置
- Gain SOP

上述内容由 Gain 模块进行说明。

---

# 17. Reference

## Fact

- 产品培训资料关于平场曝光、Pixel Response 及 Gain Calibration 流程。

## Theory

- Gain 为 Pixel 对相同曝光条件响应能力的差异。
- Gain Calibration 通过建立 Gain Table 提高图像均匀性。