# ShutdownFailure

Version: V2.0

Module: Failure Knowledge

Status: Released

Source Level:
- Engineering
- Service

Applicable Product:
- Wired Detector
- Wireless Detector

Related Documents:
- README.md
- StartupFailure.md
- DetectorOffline.md
- CommunicationTimeout.md
- WorkflowFailure.md
- ../SoftwareFailure/FirmwareFailure.md
- ../SoftwareFailure/DriverFailure.md
- ../HardwareFailure/PowerFailure.md
- ../HardwareFailure/MainBoardFailure.md
- ../../06_Workflow/ShutdownWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Shutdown Failure 描述数字平板探测器（Flat Panel Detector，FPD）在系统关闭过程中发生的各种异常，包括无法正常关机、关机超时、设备无响应、电源无法关闭、资源释放失败及异常断电等问题。

系统关机不仅包括关闭应用程序，还涉及曝光流程结束、缓存写入、通信终止、FPGA 停止运行、电源管理及硬件状态保存等多个步骤。任一环节异常均可能导致 Shutdown Failure。

本文件回答的问题：

> **为什么 Detector 无法正常关机？为什么关闭软件后设备仍保持在线？为什么强制断电后再次启动出现异常？**

---

# 2. Scope

适用于：

- Factory Test
- Installation
- Preventive Maintenance
- Technical Support
- Field Service
- Engineering Debug

适用于：

- System Shutdown
- Application Exit
- Firmware Shutdown
- Power Management
- Safe Power-Off

---

# 3. What is Shutdown Failure

Shutdown Failure 指：

**Detector 或系统在执行关机流程过程中，无法按照预定流程完成资源释放、通信关闭及电源管理，从而导致关机异常。**

主要表现：

- Shutdown Timeout
- Application Cannot Exit
- Detector Still Online
- Device No Response
- Forced Shutdown Required
- Restart Failure After Shutdown

---

# 4. Failure Classification

```text
Shutdown Failure

├── Application Exit Failure
├── Workflow Stop Failure
├── Communication Close Failure
├── Resource Release Failure
├── Power-Off Failure
├── Firmware Shutdown Failure
└── Forced Shutdown
```

---

# 5. Typical Symptoms

## 5.1 Application Exit Failure

特点：

- 软件无法关闭
- 界面卡死

可能原因：

- Process Deadlock
- Resource Occupied

---

## 5.2 Workflow Stop Failure

特点：

- 曝光流程未结束
- Workflow 持续运行

可能原因：

- Exposure Not Completed
- Background Task Running

---

## 5.3 Communication Close Failure

特点：

- Detector 仍在线
- Socket 未释放

可能原因：

- Driver Failure
- Communication Service Failure

---

## 5.4 Resource Release Failure

特点：

- 内存未释放
- 文件句柄未关闭

可能原因：

- Memory Leak
- File Lock

---

## 5.5 Power-Off Failure

特点：

- 电源无法关闭
- 风扇持续运行

可能原因：

- Power Controller Failure
- Main Board Failure

---

## 5.6 Firmware Shutdown Failure

特点：

- Firmware 无法停止
- FPGA 未复位

可能原因：

- Firmware Exception
- FPGA Busy

---

## 5.7 Forced Shutdown

特点：

- 必须断电才能关闭
- 下次启动异常

可能原因：

- System Hang
- Hardware Lockup

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Application Exit Failure | Software Exception |
| Workflow Stop Failure | Exposure Task Running |
| Communication Close Failure | Driver Failure |
| Resource Release Failure | Memory Leak |
| Power-Off Failure | Power Controller |
| Forced Shutdown | System Deadlock |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Main Board | Cannot Power Off |
| FPGA | Firmware Cannot Exit |
| Power Module | Power Remains On |
| Communication Board | Detector Still Online |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Application | Exit Failure |
| Driver | Communication Not Closed |
| Firmware | Shutdown Timeout |
| SDK | Resource Release Failure |

---

# 9. Relationship with Workflow

Shutdown Failure 常发生于：

- Image Acquisition 未结束
- Exposure Workflow 未退出
- Calibration Workflow 运行中
- File Saving 未完成
- Background Service 未停止

因此关机前必须确认所有 Workflow 已结束。

---

# 10. Diagnostic Workflow

```text
Shutdown Failed

↓

Application Exit？

↓

NO

↓

Check Process

↓

YES

↓

Workflow Stopped？

↓

NO

↓

Terminate Workflow

↓

YES

↓

Communication Closed？

↓

NO

↓

Driver Analysis

↓

YES

↓

Power Off？

↓

NO

↓

Power Module

↓

Shutdown Completed
```

---

# 11. Detection Methods

## Shutdown Log Analysis

检查：

- Shutdown Log
- Event Log
- System Log

---

## Process Verification

检查：

- Remaining Process
- Background Service
- Thread Status

---

## Communication Verification

检查：

- Socket
- TCP Connection
- Detector Online Status

---

## Power Verification

检查：

- Main Power
- Internal Voltage
- Power Controller

---

## Firmware Status

检查：

- Firmware Running Status
- FPGA State
- Shutdown Command Response

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Application Cannot Exit | Software Deadlock |
| Detector Still Online | Communication Not Closed |
| Device Must Be Power Cycled | Firmware Hang |
| Shutdown Timeout | Workflow Running |
| Power Cannot Be Turned Off | Power Controller Failure |
| Restart Failure After Forced Shutdown | Configuration Not Saved |

---

# 13. Engineering Recommendations

建议：

- 关闭系统前确认所有曝光及校准流程已结束。
- 禁止在数据保存过程中强制断电。
- 检查后台服务是否正常退出。
- 分析 Shutdown Log 与 Firmware Log。
- 强制关机后建议执行完整 Startup Self-Test。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## StartupFailure

异常关机可能导致下一次启动失败。

---

## CommunicationTimeout

通信未关闭可能导致 Shutdown Timeout。

---

## WorkflowFailure

Workflow 未结束是关机失败的重要原因。

---

## PowerFailure

Power Controller 故障可能导致无法断电。

---

## DecisionTree

Shutdown Failure 是系统生命周期分析的重要组成部分。

---

# 15. Knowledge Graph

```text
Shutdown Failure

├── Application Exit
├── Workflow Stop
├── Communication Close
├── Resource Release
├── Firmware Shutdown
├── Power-Off
└── Forced Shutdown

↓

Shutdown Verification

↓

Workflow Verification

↓

Communication Verification

↓

Hardware Analysis

├── Main Board
├── FPGA
├── Power
└── Communication

↓

Software Analysis

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Shutdown Failure 是 Flat Panel Detector 系统运行过程中重要的系统级故障，涉及应用退出、Workflow 停止、通信关闭、资源释放、Firmware 停止及电源管理等多个环节。其根因通常包括软件死锁、后台任务未结束、驱动异常、Firmware 卡死、电源控制故障及 Main Board 异常。通过 Shutdown Log、通信状态、资源释放状态及电源管理检查，可快速定位关机异常，并结合 Hardware Failure、Software Failure、Workflow Failure 与 DecisionTree 建立完整的系统关机故障分析体系。