# SystemFailure

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
- ShutdownFailure.md
- DetectorOffline.md
- CommunicationTimeout.md
- ExposureFailure.md
- WorkflowFailure.md
- ../HardwareFailure/README.md
- ../SoftwareFailure/README.md
- ../EnvironmentFailure/README.md
- ../CalibrationFailure/README.md
- ../../06_Workflow/
- ../../09_DecisionTree/

---

# 1. Purpose

System Failure 模块用于描述数字平板探测器（Flat Panel Detector，FPD）在系统运行层面发生的各种故障，包括设备启动失败、关机异常、Detector Offline、通信超时、曝光失败及工作流程异常等问题。

与 Hardware Failure 不同，System Failure 更关注系统级运行状态；与 Software Failure 不同，System Failure 更强调多个软硬件模块协同工作过程中产生的整体异常。

本模块建立统一的系统故障分类、分析方法及诊断流程，为研发、生产测试、现场服务及故障分析提供标准参考。

---

# 2. Scope

适用于：

- Factory Test
- FAT
- SAT
- Installation
- Preventive Maintenance
- Technical Support
- Field Service

包括：

- System Startup
- System Shutdown
- Detector Online Status
- Communication Status
- Exposure Workflow
- System Workflow

---

# 3. System Failure Architecture

```text
System Failure

├── Startup Failure
├── Shutdown Failure
├── Detector Offline
├── Communication Timeout
├── Exposure Failure
└── Workflow Failure
```

各子模块职责如下：

| Module | Description |
|----------|-------------|
| StartupFailure | 系统启动异常 |
| ShutdownFailure | 系统关机异常 |
| DetectorOffline | Detector 无法上线 |
| CommunicationTimeout | 通信超时 |
| ExposureFailure | 曝光流程异常 |
| WorkflowFailure | 系统工作流程异常 |

---

# 4. System Architecture

```text
User

↓

Application

↓

SDK

↓

Driver

↓

Firmware

↓

FPGA

↓

Detector Hardware
```

任何一层发生异常，都可能最终表现为 **System Failure**。

---

# 5. Common Failure Symptoms

典型表现包括：

- Startup Failed
- Detector Offline
- Communication Timeout
- Exposure Timeout
- Workflow Interrupted
- Unexpected Restart
- Image Acquisition Failed
- Shutdown Failed

系统故障通常具有以下特点：

- 涉及多个模块
- 需要跨层分析
- 单一日志难以定位根因
- 需要结合 Hardware、Software、Environment 综合判断

---

# 6. Failure Classification

## 6.1 Startup Failure

系统无法正常启动或初始化失败。

---

## 6.2 Shutdown Failure

系统无法正常退出或资源释放失败。

---

## 6.3 Detector Offline

Detector 无法建立连接或上线失败。

---

## 6.4 Communication Timeout

系统等待响应超时。

---

## 6.5 Exposure Failure

曝光流程未完成或中途终止。

---

## 6.6 Workflow Failure

多个流程节点之间协同失败。

---

# 7. Relationship with Other Failure Modules

| Failure Module | Relationship |
|----------------|--------------|
| Hardware Failure | 系统故障可能由硬件引起 |
| Software Failure | 系统流程依赖软件运行 |
| Calibration Failure | 校准异常影响系统运行 |
| Environment Failure | 环境因素可诱发系统故障 |
| Image Failure | 系统异常最终可能表现为图像异常 |

---

# 8. Standard Diagnostic Workflow

```text
System Failure

↓

Startup Successful？

↓

NO

↓

Startup Analysis

↓

YES

↓

Detector Online？

↓

NO

↓

Communication Analysis

↓

YES

↓

Exposure Successful？

↓

NO

↓

Exposure Analysis

↓

YES

↓

Workflow Complete？

↓

NO

↓

Workflow Analysis

↓

YES

↓

Image Verification

↓

Root Cause Analysis
```

---

# 9. Troubleshooting Principles

推荐按照以下顺序排查：

1. 确认系统是否正常启动。
2. 检查 Detector 是否成功上线。
3. 检查通信链路状态。
4. 检查曝光流程是否完成。
5. 检查 Workflow 执行状态。
6. 检查日志、错误码及系统事件。
7. 结合 Hardware、Software、Environment 进行 Root Cause Analysis。

---

# 10. Related Documents

## StartupFailure

分析系统启动异常。

---

## ShutdownFailure

分析系统关机异常。

---

## DetectorOffline

分析 Detector 无法上线问题。

---

## CommunicationTimeout

分析通信超时问题。

---

## ExposureFailure

分析曝光失败问题。

---

## WorkflowFailure

分析完整工作流程异常。

---

## DecisionTree

System Failure 是系统级故障分析的重要入口。

---

# 11. Knowledge Graph

```text
System Failure

├── Startup
├── Shutdown
├── Detector Offline
├── Communication Timeout
├── Exposure
└── Workflow

↓

System Verification

↓

Communication Verification

↓

Image Verification

↓

Hardware Analysis

↓

Software Analysis

↓

Environment Analysis

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 12. Summary

System Failure 是 Flat Panel Detector 故障知识体系中的系统层模块，主要涵盖启动、关机、Detector 上线、通信、曝光及工作流程等系统运行过程中的异常。System Failure 通常是 Hardware Failure、Software Failure、Calibration Failure 及 Environment Failure 的综合表现，需要结合日志分析、流程分析及系统状态验证进行定位，并通过 DecisionTree 建立完整的系统级 Root Cause Analysis。