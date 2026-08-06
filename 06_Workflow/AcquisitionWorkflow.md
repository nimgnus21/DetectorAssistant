# ExposureWorkflow

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
- DetectorLifecycle.md
- ConnectionWorkflow.md
- AcquisitionWorkflow.md
- ../02_System/SignalFlow.md
- ../03_Hardware/Scintillator.md
- ../03_Hardware/Photodiode.md
- ../03_Hardware/TFT_Array.md
- ../04_Software/README.md
- README.md

---

# 1. Purpose

Exposure Workflow 定义数字平板探测器（Flat Panel Detector，FPD）从进入 Ready 状态到完成一次 X-ray Exposure 的标准控制流程。

本流程负责曝光准备、曝光触发、曝光状态监测及曝光结束控制，为后续 Acquisition Workflow 提供稳定、完整的信号采集条件。

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- AED Mode
- Trigger Mode
- Software Trigger
- Manual Trigger

---

# 3. Workflow Objectives

Exposure Workflow 的主要目标包括：

- 确认 Detector Ready
- 接收曝光指令
- 控制曝光状态
- 监测曝光过程
- 生成 Exposure Complete 信号
- 进入 Acquisition Workflow

---

# 4. Workflow Overview

```text
Detector Ready

↓

Exposure Request

↓

Exposure Preparation

↓

Trigger Detection

↓

Exposure Start

↓

Charge Integration

↓

Exposure End

↓

Exposure Complete

↓

Acquisition Workflow
```

---

# 5. Workflow Inputs

输入包括：

- Detector Ready
- Host Exposure Command
- Trigger Signal
- AED Signal（如支持）
- Exposure Parameters

---

# 6. Ready State Verification

开始曝光前确认 Detector 已满足曝光条件。

检查项目：

- Detector Online
- SDK Connected
- Calibration Loaded
- Temperature Normal
- Battery Normal（无线）
- Exposure Mode Valid
- Trigger Mode Valid

输出：

Ready for Exposure

---

# 7. Exposure Preparation

准备曝光环境。

包括：

- Exposure Parameter Download
- Trigger Configuration
- Exposure Timer Reset
- Integration Reset
- Detector Status Lock

输出：

Exposure Prepared

---

# 8. Trigger Detection

等待曝光触发。

支持模式：

### Software Trigger

由 Host 发送曝光命令。

---

### Hardware Trigger

由外部 Trigger Input 触发。

---

### AED Trigger

Automatic Exposure Detection。

Detector 自动检测 X-ray。

输出：

Exposure Triggered

---

# 9. Exposure Start

Detector 开始曝光。

主要事件：

- Integration Start
- TFT Integration Mode
- X-ray Detection
- Exposure Timer Start

输出：

Exposure Active

---

# 10. Charge Integration

曝光期间 Pixel 持续积分。

过程：

```text
X-ray

↓

Scintillator

↓

Visible Light

↓

Photodiode

↓

Charge Generation

↓

Pixel Charge Storage
```

Detector 持续监测曝光状态。

输出：

Integrated Charge

---

# 11. Exposure Monitoring

曝光过程中持续监测：

- Exposure Time
- Trigger Status
- Detector Status
- Temperature
- Battery Status
- Communication Status

异常时可中止曝光。

---

# 12. Exposure End

曝光结束条件：

- X-ray End
- Trigger Release
- Exposure Timeout
- Host Stop Command

主要动作：

- Integration Stop
- Exposure Timer Stop
- Detector Unlock

输出：

Exposure Finished

---

# 13. Workflow Outputs

Exposure Workflow 输出：

- Exposure Complete
- Integrated Pixel Charge
- Exposure Information
- Acquisition Start Signal

进入：

Acquisition Workflow

---

# 14. State Transition

```text
READY

↓

PREPARING

↓

WAITING TRIGGER

↓

EXPOSING

↓

INTEGRATING

↓

EXPOSURE COMPLETE

↓

ACQUISITION
```

---

# 15. Timing Relationship

```text
ConnectionWorkflow

↓

ExposureWorkflow

├── Ready Verification
├── Exposure Preparation
├── Trigger Detection
├── Exposure Start
├── Charge Integration
└── Exposure End

↓

AcquisitionWorkflow
```

---

# 16. Common Exposure Failure

| Failure | Description |
|----------|-------------|
| Detector Not Ready | Detector 未进入 Ready |
| Trigger Timeout | 长时间未收到 Trigger |
| Trigger Error | Trigger 信号异常 |
| Exposure Timeout | 曝光超时 |
| AED Failure | AED 检测失败 |
| Exposure Interrupted | 曝光过程中断 |
| Communication Lost | 曝光期间通信中断 |
| Temperature Alarm | 温度超限 |
| Battery Low | 电池电量不足 |

详细处理参见：

- WorkflowTroubleshooting.md
- 07_FailureKnowledge/ExposureFailure.md（规划中）

---

# 17. Engineering Notes

工程建议：

- Exposure 前必须确认 Calibration 已加载。
- Exposure 过程中禁止修改 Detector 参数。
- Exposure 状态下应持续监测温度及通信状态。
- 曝光结束后立即进入 Acquisition Workflow，避免积分电荷衰减。
- 所有曝光异常应记录日志及错误代码。

---

# 18. Relationship with Other Modules

## Connection Workflow

提供：

- Detector Ready
- Trigger Configuration
- Exposure Parameters

---

## Hardware

负责：

- Scintillator
- Photodiode
- TFT Array

---

## Software

负责：

- Trigger Control
- Exposure Control
- Status Monitoring

---

## Acquisition Workflow

Exposure 完成后进入 Acquisition Workflow，开始读取 Pixel Charge。

---

# 19. Document Boundary

本文件负责：

- Exposure 准备
- Trigger 检测
- Exposure 控制
- Charge Integration
- Exposure 状态监测
- Exposure 结束控制

本文件不负责：

- Pixel Charge Readout
- ADC Conversion
- Image Calibration
- Image Processing
- Image Transmission

上述内容由后续 Workflow 文档说明。

---

# 20. Knowledge Graph

```text
Detector Ready

↓

Exposure Request

↓

Exposure Preparation

↓

Trigger Detection

↓

Exposure Start

↓

Charge Integration

↓

Exposure Monitoring

↓

Exposure End

↓

Exposure Complete

↓

Acquisition Workflow
```

---

# 21. Summary

Exposure Workflow 定义 Detector 从 Ready 状态进入曝光并完成 X-ray 信号积分的全过程，包括曝光准备、触发检测、积分控制、曝光监测及曝光结束控制。完成本流程后，Detector 已完成像素电荷积分，为 Acquisition Workflow 的电荷读取提供完整输入，是图像形成流程中的关键控制阶段。