# ImageGenerationWorkflow

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
- CalibrationWorkflow.md
- ImageTransmissionWorkflow.md
- ../05_Calibration/README.md
- ../02_System/SignalFlow.md
- ../04_Software/README.md
- README.md

---

# 1. Purpose

Image Generation Workflow 定义数字平板探测器（Flat Panel Detector，FPD）完成图像校准后，生成完整图像数据（Image Frame）的标准流程。

本流程负责将校准后的像素数据组织成完整图像，生成图像元数据（Metadata），建立图像帧（Frame），并完成图像完整性验证，为 Image Transmission Workflow 提供可传输的图像对象。

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Static Detector
- Dynamic Detector

适用于 Detector 图像生成流程。

---

# 3. Workflow Objectives

Image Generation Workflow 的主要目标包括：

- 接收校准后的图像数据
- 组织完整图像帧
- 生成图像 Metadata
- 建立图像缓冲区
- 验证图像完整性
- 输出可传输图像

---

# 4. Workflow Overview

```text
Calibration Complete

↓

Corrected Image

↓

Image Assembly

↓

Metadata Generation

↓

Frame Construction

↓

Image Validation

↓

Image Ready

↓

ImageTransmissionWorkflow
```

---

# 5. Workflow Inputs

输入包括：

- Corrected Image
- Calibration Status
- Detector Information
- Exposure Information
- System Configuration

---

# 6. Image Assembly

将校准后的像素数据组织为完整图像。

主要内容：

- Pixel Matrix Assembly
- Row Ordering
- Column Ordering
- Image Dimension Verification
- Pixel Format Confirmation

输出：

Image Matrix Ready

---

# 7. Metadata Generation

生成图像元数据。

包括：

## Detector Information

- Detector Model
- Serial Number
- Firmware Version

---

## Exposure Information

- Exposure Time
- Trigger Mode
- Acquisition Mode

---

## Image Information

- Image Width
- Image Height
- Pixel Depth
- Frame Number
- Timestamp

输出：

Metadata Ready

---

# 8. Frame Construction

建立完整图像帧。

典型结构：

```text
Frame Header

↓

Image Metadata

↓

Image Data

↓

Frame Tail（Optional）
```

完成图像封装。

输出：

Image Frame

---

# 9. Image Buffer Management

管理图像缓存。

包括：

- Allocate Buffer
- Copy Image Data
- Buffer State Update
- Ready Queue Management

确保图像可安全传输。

输出：

Image Buffer Ready

---

# 10. Image Validation

验证生成结果。

检查内容：

- Frame Integrity
- Image Dimension
- Pixel Count
- Metadata Completeness
- Buffer Status

验证通过后允许进入发送流程。

输出：

Image Verified

---

# 11. Workflow Outputs

输出包括：

- Image Frame
- Image Metadata
- Image Buffer
- Image Ready Signal

进入：

ImageTransmissionWorkflow

---

# 12. State Transition

```text
CALIBRATION COMPLETE

↓

IMAGE ASSEMBLY

↓

METADATA GENERATION

↓

FRAME CONSTRUCTION

↓

BUFFER READY

↓

IMAGE VALIDATION

↓

IMAGE READY

↓

IMAGE TRANSMISSION
```

---

# 13. Timing Relationship

```text
CalibrationWorkflow

↓

ImageGenerationWorkflow

├── Image Assembly
├── Metadata Generation
├── Frame Construction
├── Buffer Management
└── Image Validation

↓

ImageTransmissionWorkflow
```

---

# 14. Common Image Generation Failure

| Failure | Description |
|----------|-------------|
| Image Assembly Failed | 图像组装失败 |
| Metadata Missing | 图像元数据缺失 |
| Frame Construction Failed | 图像帧生成失败 |
| Buffer Allocation Failed | 图像缓存分配失败 |
| Frame Validation Failed | 图像完整性校验失败 |
| Timestamp Error | 时间戳异常 |
| Frame Number Error | 帧编号异常 |
| Image Size Mismatch | 图像尺寸异常 |

详细处理参见：

- WorkflowTroubleshooting.md
- 07_FailureKnowledge（相关章节）

---

# 15. Engineering Notes

工程建议：

- Image Generation 应在 Calibration 完成后立即执行。
- 图像 Metadata 应保持完整、一致。
- 图像缓冲区应支持连续帧管理。
- Frame Number 应保持连续递增。
- 图像生成异常应记录日志及错误代码。

---

# 16. Relationship with Other Modules

## Calibration Workflow

提供：

- Corrected Image
- Calibration Status

---

## Software

负责：

- Frame Builder
- Metadata Manager
- Buffer Manager

---

## Image Transmission Workflow

接收：

- Image Frame
- Image Buffer
- Image Metadata

并负责图像发送。

---

# 17. Document Boundary

本文件负责：

- 图像组装
- Metadata 生成
- 图像帧建立
- Buffer 管理
- 图像完整性验证

本文件不负责：

- Offset/Gain/Defect 校正
- 网络通信
- 图像发送
- 图像存储
- DICOM 封装

上述内容由对应 Workflow 或 Software 模块负责。

---

# 18. Knowledge Graph

```text
Calibration Complete

↓

Corrected Image

↓

Image Assembly

↓

Metadata Generation

↓

Frame Construction

↓

Image Buffer

↓

Image Validation

↓

Image Ready

↓

ImageTransmissionWorkflow
```

---

# 19. Summary

Image Generation Workflow 定义 Detector 在完成图像校准后生成完整图像帧的全过程，包括图像组装、Metadata 生成、Frame 建立、Buffer 管理及完整性验证。完成本流程后生成标准 Image Frame，为 ImageTransmissionWorkflow 提供可靠、完整、可传输的图像对象，是连接图像校准与图像传输的重要工作阶段。