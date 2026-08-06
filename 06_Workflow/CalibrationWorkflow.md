# CalibrationWorkflow

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
- ReadoutWorkflow.md
- ImageProcessingWorkflow.md
- ../05_Calibration/README.md
- ../05_Calibration/Offset/README.md
- ../05_Calibration/Gain/README.md
- ../05_Calibration/Defect/README.md
- ../05_Calibration/Template/README.md
- README.md

---

# 1. Purpose

Calibration Workflow 定义数字平板探测器（Flat Panel Detector，FPD）完成 Raw Image 采集后，对原始图像进行校准处理的标准流程。

本流程负责调用 Calibration Template，对 Raw Image 依次执行 Offset Correction、Gain Correction、Defect Correction 及相关校准处理，生成可用于后续图像处理的 Corrected Image。

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Static Detector
- Dynamic Detector

适用于所有采用 Calibration Template 的产品。

---

# 3. Workflow Objectives

Calibration Workflow 的主要目标包括：

- 加载 Calibration Template
- 校正 Offset
- 校正 Gain
- 修复 Defect Pixel
- 生成 Corrected Image
- 输出校准状态

---

# 4. Workflow Overview

```text
Raw Image

↓

Calibration Request

↓

Load Calibration Template

↓

Offset Correction

↓

Gain Correction

↓

Defect Correction

↓

Image Validation

↓

Corrected Image

↓

Image Processing Workflow
```

---

# 5. Workflow Inputs

输入包括：

- Raw Image
- Offset Template
- Gain Template
- Defect Template
- Calibration Parameter
- Detector Configuration

---

# 6. Calibration Preparation

开始校准前进行准备。

包括：

- 检查 Calibration Status
- 检查 Template Version
- 检查 Detector Model
- 检查 Calibration Parameter
- 建立 Calibration Context

输出：

Calibration Ready

---

# 7. Template Loading

加载 Calibration 数据。

包括：

- Offset Template
- Gain Template
- Defect Template
- Calibration Parameter

验证：

- Template Version
- Detector Compatibility
- File Integrity

输出：

Template Loaded

---

# 8. Offset Correction

执行 Offset 校正。

目的：

消除暗场偏置。

处理：

```text
Raw Image

↓

Offset Image

↓

Subtract Offset

↓

Offset Corrected Image
```

输出：

Offset Corrected Image

---

# 9. Gain Correction

执行 Gain 校正。

目的：

统一 Pixel Response。

处理：

```text
Offset Corrected Image

↓

Gain Template

↓

Pixel Normalization

↓

Gain Corrected Image
```

输出：

Gain Corrected Image

---

# 10. Defect Correction

修复异常 Pixel。

处理对象：

- Dead Pixel
- Hot Pixel
- Bad Pixel
- Cluster Pixel

方法包括：

- Neighbor Interpolation
- Average Interpolation
- Adaptive Replacement

输出：

Defect Corrected Image

---

# 11. Image Validation

校验校准结果。

包括：

- Image Size
- Pixel Range
- Calibration Status
- Template Status
- Processing Result

验证通过后继续。

输出：

Calibration Passed

---

# 12. Workflow Outputs

Calibration Workflow 输出：

- Corrected Image
- Calibration Status
- Calibration Log
- Image Ready

进入：

ImageProcessingWorkflow

---

# 13. State Transition

```text
RAW IMAGE

↓

LOAD TEMPLATE

↓

OFFSET

↓

GAIN

↓

DEFECT

↓

VALIDATION

↓

CALIBRATION COMPLETE

↓

IMAGE PROCESSING
```

---

# 14. Timing Relationship

```text
ReadoutWorkflow

↓

CalibrationWorkflow

├── Template Loading
├── Offset Correction
├── Gain Correction
├── Defect Correction
└── Validation

↓

ImageProcessingWorkflow
```

---

# 15. Common Calibration Failure

| Failure | Description |
|----------|-------------|
| Template Missing | 校准模板缺失 |
| Template Version Error | 模板版本错误 |
| Offset Correction Failed | Offset 校正失败 |
| Gain Correction Failed | Gain 校正失败 |
| Defect Template Error | Defect 模板异常 |
| Detector Model Mismatch | Detector 型号不匹配 |
| Calibration Timeout | 校准超时 |
| Validation Failed | 校准结果校验失败 |

详细处理参见：

- WorkflowTroubleshooting.md
- 05_Calibration/

---

# 16. Engineering Notes

工程建议：

- Calibration Template 应与 Detector SN 保持一致。
- Offset → Gain → Defect 的执行顺序不得改变。
- 校准过程中不得切换 Template。
- 校准完成后应记录 Template Version。
- 校准异常应保留完整日志。

---

# 17. Relationship with Other Modules

## Readout Workflow

提供：

- Raw Image

---

## Calibration Module

提供：

- Offset Template
- Gain Template
- Defect Template
- Calibration Parameter

---

## Software

负责：

- Calibration Engine
- Template Management
- Processing Control

---

## ImageProcessing Workflow

Calibration 完成后进入 Image Processing Workflow。

---

# 18. Document Boundary

本文件负责：

- Calibration Template 加载
- Offset 校正
- Gain 校正
- Defect 修复
- 校准结果验证

本文件不负责：

- 图像增强
- 窗宽窗位
- LUT
- 图像压缩
- 图像传输

上述内容由 ImageProcessingWorkflow 负责。

---

# 19. Knowledge Graph

```text
Raw Image

↓

Template Loading

↓

Offset Correction

↓

Gain Correction

↓

Defect Correction

↓

Validation

↓

Corrected Image

↓

ImageProcessingWorkflow
```

---

# 20. Summary

Calibration Workflow 定义 Detector 对 Raw Image 执行标准校准处理的全过程，包括 Calibration Template 加载、Offset Correction、Gain Correction、Defect Correction 及结果验证。完成本流程后生成 Corrected Image，为后续 Image Processing Workflow 提供一致、可靠的图像输入，确保图像质量满足临床及工程应用要求。