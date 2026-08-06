# ImageTransmissionWorkflow

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
- ImageGenerationWorkflow.md
- ShutdownWorkflow.md
- ../02_System/Communication.md
- ../04_Software/README.md
- README.md

---

# 1. Purpose

Image Transmission Workflow 定义数字平板探测器（Flat Panel Detector，FPD）完成图像生成后，将图像数据发送至 Host、SDK 或 Workstation 的标准流程。

本流程负责图像发送准备、数据传输、完整性确认、传输状态管理及资源释放，确保图像能够可靠、安全、完整地到达接收端。

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Static Detector
- Dynamic Detector

适用于所有 Detector 图像输出流程。

---

# 3. Workflow Objectives

Image Transmission Workflow 的主要目标包括：

- 获取待发送图像
- 建立发送任务
- 发送 Image Frame
- 确认数据完整性
- 更新传输状态
- 释放图像缓存

---

# 4. Workflow Overview

```text
Image Ready

↓

Transmission Request

↓

Transmission Preparation

↓

Image Sending

↓

Host Reception

↓

Transmission Verification

↓

Transmission Complete

↓

Buffer Release
```

---

# 5. Workflow Inputs

输入包括：

- Image Frame
- Image Metadata
- Connection Status
- Communication Channel
- Transmission Configuration

---

# 6. Transmission Preparation

发送前检查：

- Connection Ready
- Host Online
- Buffer Ready
- Image Complete
- Communication Available

输出：

Transmission Ready

---

# 7. Image Sending

开始发送图像。

包括：

- Frame Header
- Metadata
- Image Data

按照通信协议发送。

输出：

Frame Transmitting

---

# 8. Host Reception

Host 接收数据。

包括：

- Receive Frame
- Parse Header
- Receive Metadata
- Receive Image Data

输出：

Frame Received

---

# 9. Transmission Verification

验证发送结果。

包括：

- Frame Integrity
- Packet Count
- CRC（如支持）
- Transmission Status

输出：

Transmission Verified

---

# 10. Buffer Release

发送完成后释放资源。

包括：

- Image Buffer Release
- Queue Update
- Memory Recovery

输出：

Transmission Finished

---

# 11. Workflow Outputs

输出包括：

- Transmission Complete
- Image Delivered
- Transmission Status
- Buffer Released

Detector 返回 Ready 状态，等待下一次曝光。

---

# 12. State Transition

```text
IMAGE READY

↓

TRANSMISSION READY

↓

SENDING

↓

RECEIVING

↓

VERIFYING

↓

COMPLETE

↓

READY
```

---

# 13. Timing Relationship

```text
ImageGenerationWorkflow

↓

ImageTransmissionWorkflow

├── Preparation
├── Sending
├── Reception
├── Verification
└── Buffer Release

↓

Detector Ready
```

---

# 14. Common Transmission Failure

| Failure | Description |
|----------|-------------|
| Connection Lost | 通信连接中断 |
| Transmission Timeout | 发送超时 |
| Packet Loss | 数据包丢失 |
| CRC Error | 数据校验失败 |
| Host Not Responding | Host 无响应 |
| Buffer Overflow | 缓存溢出 |
| Transmission Interrupted | 图像发送中断 |
| Retry Failed | 重传失败 |

详细处理参见：

- WorkflowTroubleshooting.md
- 07_FailureKnowledge（相关章节）

---

# 15. Engineering Notes

工程建议：

- 图像发送前确认 Connection Workflow 已建立稳定连接。
- 每帧图像应具有唯一 Frame ID。
- 发送完成后再释放 Buffer。
- 通信异常应支持日志记录及重试机制。
- 连续曝光时应采用队列方式管理待发送图像。

---

# 16. Relationship with Other Modules

## ImageGenerationWorkflow

提供：

- Image Frame
- Metadata
- Buffer

---

## Communication Module

负责：

- 网络连接
- 数据发送
- 状态维护

---

## ShutdownWorkflow

完成发送后，Detector 可继续待机或进入关机流程。

---

# 17. Document Boundary

本文件负责：

- 图像发送准备
- 图像传输
- 数据完整性验证
- 发送状态管理
- Buffer 释放

本文件不负责：

- 图像采集
- 图像校准
- 图像生成
- DICOM 存储
- PACS 上传

---

# 18. Knowledge Graph

```text
Image Ready

↓

Transmission Preparation

↓

Image Sending

↓

Host Reception

↓

Transmission Verification

↓

Transmission Complete

↓

Detector Ready
```

---

# 19. Summary

Image Transmission Workflow 定义 Detector 将 Image Frame 发送至 Host 或 Workstation 的全过程，包括发送准备、数据传输、完整性验证及资源释放。完成本流程后，一次完整的图像采集生命周期结束，Detector 返回 Ready 状态，可继续执行下一次 Exposure Workflow。