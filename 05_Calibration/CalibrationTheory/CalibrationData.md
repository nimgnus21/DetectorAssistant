# CalibrationData

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
- CalibrationFlow.md
- CalibrationTiming.md
- PixelResponse.md
- OffsetTheory.md
- GainTheory.md
- DefectTheory.md
- ../../02_System/ImagePipeline.md
- ../../04_Software/Firmware.md
- ../../04_Software/iDetector.md

---

# 1. Purpose

Calibration Data 是数字平板探测器完成 Calibration 后生成的校准数据集合。

Calibration Data 用于记录 Detector 当前 Pixel Response 特性，并在图像处理过程中参与图像校正，提高图像质量及一致性。

Calibration Data 本身不是图像数据，而是用于修正图像的数据。

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

Calibration Data 是 Calibration 过程生成的数据集合。

Calibration Data 反映当前 Detector 的响应特性。

图像处理阶段读取 Calibration Data，对 Raw Image 进行校正。

Calibration Data 来源于：

- Offset Calibration
- Gain Calibration
- Defect Calibration

---

# 4. Composition

Calibration Data 包括：

- Offset Data
- Gain Data
- Defect Data

不同产品的软件实现及存储格式可能不同。

本文件仅说明逻辑组成，不定义具体文件格式。

---

# 5. Data Generation

Calibration Data 由 Calibration 过程生成。

生成流程如下：

```text
Calibration

↓

Image Acquisition

↓

Data Calculation

↓

Calibration Data

↓

Data Storage
```

Calibration Data 更新后替换旧版本数据。

---

# 6. Data Usage

正常曝光流程如下：

```text
Raw Image

↓

Load Calibration Data

↓

Offset Correction

↓

Gain Correction

↓

Defect Correction

↓

Corrected Image
```

Calibration Data 在每次图像处理过程中都会参与计算。

---

# 7. Data Lifecycle

Calibration Data 生命周期包括：

```text
Calibration

↓

Data Generation

↓

Data Storage

↓

Image Processing

↓

Data Update

↓

Data Replacement
```

Calibration Data 可根据系统维护要求重新生成。

---

# 8. Relationship with Image Pipeline

Calibration Data 不参与图像采集。

Calibration Data 在 Image Pipeline 中参与图像校正。

位置如下：

```text
Raw Image

↓

Calibration Data

↓

Image Correction

↓

Corrected Image
```

Reference：

- ../../02_System/ImagePipeline.md

---

# 9. Relationship with Firmware

Calibration Data 通常由 Firmware 管理。

Firmware 负责：

- 数据读取
- 数据加载
- 数据调用
- 数据更新

具体实现方式由产品软件架构决定。

Reference：

- ../../04_Software/Firmware.md

---

# 10. Relationship with iDetector

iDetector 可执行 Calibration 操作。

Calibration 完成后：

Calibration Data 被更新。

后续曝光使用新的 Calibration Data。

具体软件操作流程见：

- ../../04_Software/iDetector.md

---

# 11. Failure Influence

Calibration Data 异常可能导致：

- Offset Correction Failure
- Gain Correction Failure
- Defect Correction Failure
- Calibration Failure
- Image Artifact
- Nonuniformity
- Fixed Pattern Noise

Calibration Data 与 Detector 不匹配时，也可能导致图像质量下降。

---

# 12. Diagnostic Significance

分析 Calibration 相关故障时，应确认：

- Calibration 是否完成
- Calibration Data 是否成功生成
- Calibration Data 是否正确加载
- Calibration Data 是否与当前 Detector 对应
- Calibration Data 是否需要重新生成

---

# 13. Knowledge Graph

```text
Calibration

├────────► Offset Data

├────────► Gain Data

└────────► Defect Data

↓

Calibration Data

↓

Firmware

↓

Image Processing

↓

Corrected Image
```

---

# 14. Related Documents

Calibration：

- CalibrationOverview.md
- CalibrationFlow.md
- CalibrationTiming.md
- PixelResponse.md
- OffsetTheory.md
- GainTheory.md
- DefectTheory.md

Software：

- Firmware.md
- iDetector.md

System：

- ImagePipeline.md

---

# 15. Document Boundary

本文件负责：

- Calibration Data 定义
- Calibration Data 组成
- Calibration Data 生命周期
- Calibration Data 与 Image Pipeline 的关系
- Calibration Data 与 Firmware 的关系

本文件不负责：

- Calibration 操作流程
- Calibration 参数
- Calibration 文件格式
- Firmware 实现细节
- 数据存储结构

上述内容由对应文档说明。

---

# 16. Reference

## Fact

- 产品培训资料关于 Calibration、图像处理及数据调用流程。
- 产品用户手册关于 Calibration 操作流程。

## Theory

- Calibration Data 是 Calibration 生成的数据集合。
- Calibration Data 在图像处理过程中用于图像校正。