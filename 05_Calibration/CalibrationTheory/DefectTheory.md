# DefectTheory

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
- GainTheory.md
- ../../02_System/ImagePipeline.md
- ../../03_Hardware/Photodiode.md
- ../../03_Hardware/TFT_Array.md
- ../../08_ImageDiagnosis/
- ../../09_DecisionTree/

---

# 1. Purpose

Defect Theory 描述数字平板探测器中异常 Pixel 的形成机制及 Defect Calibration 的理论基础。

Defect Calibration 的目标是识别响应异常的 Pixel，并建立 Defect Map，在图像重建过程中对异常 Pixel 进行补偿，提高图像连续性和一致性。

Defect Theory 是 Bad Pixel、Bad Column、Bad Row 等图像异常分析的重要理论基础。

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

Defect Pixel 是指响应明显偏离正常范围的 Pixel。

异常可能表现为：

- 无响应
- 响应过低
- 响应过高
- 响应不稳定

Defect Calibration 用于识别这些异常 Pixel，并建立 Defect Map。

---

# 4. Defect Generation

Defect Pixel 可发生于整个成像链。

可能涉及：

```text
Scintillator

↓

Photodiode

↓

TFT Array

↓

Readout ASIC

↓

ADC

↓

FPGA
```

任一环节异常均可能导致 Pixel Response 偏离正常范围。

---

# 5. Physical Principle

在正常曝光条件下：

所有 Pixel 应产生相近的响应。

若某些 Pixel 的输出长期偏离正常范围，则判定为 Defect Pixel。

Defect Calibration 根据检测结果生成 Defect Map。

图像处理阶段依据 Defect Map 对异常 Pixel 进行补偿。

---

# 6. Defect Characteristics

Defect Pixel 具有以下特点：

- 响应异常
- 可重复出现
- 位置固定
- 与曝光条件无直接对应关系
- 可建立 Defect Map

---

# 7. Defect Categories

根据 Pixel Response 可分为：

## Dead Pixel

Pixel 无响应。

---

## Bright Pixel

Pixel 输出明显高于周围区域。

---

## Dark Pixel

Pixel 输出明显低于周围区域。

---

## Unstable Pixel

Pixel 输出不稳定。

---

## Cluster Defect

多个相邻 Pixel 同时异常。

---

## Line Defect

连续 Pixel 异常形成 Bad Row 或 Bad Column。

---

# 8. Relationship with Pixel Response

Defect Pixel 本质上属于 Pixel Response 异常。

表现为：

```text
Normal Pixel

≈

Expected Response

Defect Pixel

≠

Expected Response
```

因此 Defect Calibration 建立于 Pixel Response 分析基础之上。

---

# 9. Relationship with Calibration

Defect Calibration 建立：

Defect Map。

图像处理流程：

```text
Pixel Response

↓

Defect Detection

↓

Defect Map

↓

Pixel Compensation

↓

Corrected Image
```

---

# 10. Image Influence

Defect 未处理时可能表现为：

- Dead Pixel
- Bright Pixel
- Dark Pixel
- Bad Column
- Bad Row
- Cluster Artifact

异常数量增加时会降低图像质量。

---

# 11. Failure Manifestation

Defect Calibration 异常可能表现为：

- Defect Calibration Failure
- Defect Map Error
- Pixel Compensation Failure
- Defect 数量异常增加
- 图像固定异常持续存在

---

# 12. Diagnostic Significance

出现以下现象时应检查 Defect：

- 固定亮点
- 固定暗点
- Bad Column
- Bad Row
- Cluster Artifact
- Defect Calibration Failure

同时结合 Offset、Gain Calibration 结果进行综合分析。

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

Defect Calibration 建立在 Offset 与 Gain Calibration 完成之后。

---

# 14. Knowledge Graph

```text
Pixel Response

↓

Defect Detection

↓

Defect Pixel

↓

Defect Map

↓

Pixel Compensation

↓

Corrected Image
```

---

# 15. Related Documents

Calibration：

- CalibrationOverview.md
- PixelResponse.md
- OffsetTheory.md
- GainTheory.md

Hardware：

- Photodiode.md
- TFT_Array.md

Knowledge：

- ../../08_ImageDiagnosis/
- ../../09_DecisionTree/

---

# 16. Document Boundary

本文件负责：

- Defect 定义
- Defect 形成机制
- Defect 分类
- Defect 对图像影响
- Defect 与 Calibration 的关系

本文件不负责：

- Defect Calibration 操作流程
- Defect Map 文件格式
- Pixel 补偿算法
- Defect SOP

上述内容由 Defect 模块进行说明。

---

# 17. Reference

## Fact

- 产品培训资料关于 Pixel Response、异常 Pixel 检测及图像校正流程。

## Theory

- Defect Pixel 是 Pixel Response 偏离正常范围的表现。
- Defect Calibration 通过建立 Defect Map 对异常 Pixel 进行补偿。