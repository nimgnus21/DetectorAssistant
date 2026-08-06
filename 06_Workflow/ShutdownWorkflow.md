# ShutdownWorkflow

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
- ImageTransmissionWorkflow.md
- PowerOnWorkflow.md
- InitializationWorkflow.md
- ../02_System/SystemArchitecture.md
- ../04_Software/README.md
- README.md

---

# 1. Purpose

Shutdown Workflow 定义数字平板探测器（Flat Panel Detector，FPD）正常结束工作并安全关机的标准流程。

本流程负责停止图像采集、终止通信、保存系统状态、关闭硬件模块及切断电源，确保 Detector 能够安全退出工作状态，并避免图像数据丢失或硬件损坏。

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Factory Test
- Clinical System
- Service Mode

适用于所有正常关机流程。

---

# 3. Workflow Objectives

Shutdown Workflow 的主要目标包括：

- 停止当前工作任务
- 确保图像传输完成
- 断开 Host 通信
- 保存系统运行状态
- 安全关闭硬件模块
- 完成系统关机

---

# 4. Workflow Overview

```text
Shutdown Request

↓

Stop Exposure

↓

Stop Acquisition

↓

Complete Image Transmission

↓

Disconnect Communication

↓

Save System Status

↓

Power Module Shutdown

↓

Detector Power Off
```

---

# 5. Workflow Inputs

输入包括：

- Shutdown Request
- User Command
- Host Command
- Service Command
- Automatic Shutdown（如适用）

---

# 6. Shutdown Request

系统接收关机请求。

来源包括：

- Host Software
- SDK
- Service Tool
- Local Power Button（如支持）

确认当前 Detector 状态允许关机。

输出：

Shutdown Accepted

---

# 7. Stop Current Operation

停止当前工作任务。

包括：

- 停止 Exposure
- 停止 Acquisition
- 停止 Readout
- 停止 Calibration（如正在执行）

确保不再启动新的工作流程。

输出：

Operation Stopped

---

# 8. Complete Image Transmission

检查图像发送状态。

包括：

- 当前 Frame 是否发送完成
- Buffer 是否为空
- Transmission Queue 是否完成
- Host 是否已接收

如仍有待发送数据，应等待完成后继续。

输出：

Transmission Complete

---

# 9. Disconnect Communication

关闭通信连接。

包括：

- 停止 Heartbeat
- 关闭 SDK Session
- 关闭 Communication Service
- 断开 Ethernet / Wi-Fi Connection

输出：

Communication Closed

---

# 10. Save System Status

保存系统状态。

包括：

- Detector Configuration
- Runtime Status
- Error Log
- Operation Log
- System Timestamp

确保下次启动能够恢复必要信息。

输出：

System State Saved

---

# 11. Hardware Shutdown

关闭硬件模块。

关闭顺序建议：

```text
Application Service

↓

FPGA Interface

↓

Readout ASIC

↓

Gate Driver

↓

Power Management

↓

Power Supply
```

关闭过程中应确认各模块进入安全状态。

输出：

Hardware Shutdown Complete

---

# 12. Power Off

完成系统关机。

包括：

- Disable Internal Power
- Battery Protection（无线）
- Enter Power Off State

输出：

Detector Powered Off

---

# 13. Workflow Outputs

输出包括：

- Shutdown Complete
- Communication Closed
- Hardware Powered Off
- System Safe

Workflow 生命周期结束。

---

# 14. State Transition

```text
RUNNING

↓

SHUTDOWN REQUEST

↓

STOP OPERATION

↓

TRANSMISSION COMPLETE

↓

COMMUNICATION CLOSED

↓

SAVE STATUS

↓

HARDWARE SHUTDOWN

↓

POWER OFF
```

---

# 15. Timing Relationship

```text
ImageTransmissionWorkflow

↓

ShutdownWorkflow

├── Stop Operation
├── Complete Transmission
├── Disconnect Communication
├── Save System Status
├── Hardware Shutdown
└── Power Off

↓

Workflow End
```

---

# 16. Common Shutdown Failure

| Failure | Description |
|----------|-------------|
| Exposure Active | 曝光尚未结束 |
| Image Sending | 图像仍在发送 |
| Communication Busy | 通信仍在使用 |
| Save Configuration Failed | 配置保存失败 |
| Hardware Shutdown Failed | 硬件关闭失败 |
| Power Off Timeout | 关机超时 |
| Detector Not Responding | Detector 无响应 |
| Forced Shutdown | 强制关机 |

详细处理参见：

- WorkflowTroubleshooting.md
- 07_FailureKnowledge（相关章节）

---

# 17. Engineering Notes

工程建议：

- 不应在 Exposure 或 Readout 过程中执行关机。
- 图像发送完成后再断开通信。
- 日志和配置应在断电前完成保存。
- 无线产品应执行 Battery Protection。
- 强制断电仅用于异常维护场景。

---

# 18. Relationship with Other Modules

## ImageTransmissionWorkflow

负责完成最后一帧图像发送。

---

## Communication Module

负责关闭 SDK Session、Heartbeat 及网络连接。

---

## Hardware Module

负责关闭 FPGA、ASIC、Gate Driver 及电源管理模块。

---

## PowerOnWorkflow

Shutdown 完成后，下一次启动将重新进入 PowerOn Workflow。

---

# 19. Document Boundary

本文件负责：

- 接收关机请求
- 停止工作流程
- 完成图像发送
- 关闭通信连接
- 保存系统状态
- 安全关闭硬件
- 系统断电

本文件不负责：

- 图像采集
- 图像处理
- Calibration
- 系统初始化
- 网络建立

上述内容由对应 Workflow 文档负责。

---

# 20. Knowledge Graph

```text
Shutdown Request

↓

Stop Operation

↓

Complete Image Transmission

↓

Disconnect Communication

↓

Save System Status

↓

Hardware Shutdown

↓

Power Off
```

---

# 21. Summary

Shutdown Workflow 定义 Detector 从正常运行状态进入安全关机状态的全过程，包括停止工作任务、完成图像发送、关闭通信、保存系统状态、关闭硬件模块及系统断电。完成本流程后，Detector 安全退出运行状态，为下一次 PowerOnWorkflow 提供可靠、稳定的启动基础。