# SDKFailure

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
- DriverFailure.md
- ConfigurationFailure.md
- ../../06_Workflow/ConnectionWorkflow.md
- ../../06_Workflow/CommunicationWorkflow.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

SDK Failure 描述数字平板探测器（Flat Panel Detector，FPD）Software Development Kit（SDK）的典型故障模式、形成机理、系统表现、检测方法及根因分析。

SDK 为上层应用程序提供标准接口，用于设备连接、参数配置、图像采集、状态监控及图像传输。SDK 位于 Application 与 Driver 之间，是应用软件访问 Detector 功能的统一接口。

SDK 异常通常不会导致硬件损坏，但会造成设备无法控制、图像采集失败或 API 调用异常。

本文件回答的问题：

> **SDK 为什么会发生故障？故障后会导致哪些系统异常？**

---

# 2. Scope

适用于：

- Detector SDK
- Windows SDK
- Linux SDK
- C/C++ SDK
- C# SDK
- Python SDK（如适用）

适用于：

- Software Development
- Engineering Debug
- Technical Support
- Factory Test

---

# 3. SDK Overview

SDK 的主要职责：

- Device Discovery
- Device Connection
- Parameter Configuration
- Image Acquisition
- Image Reception
- Status Query
- Event Callback
- Error Reporting

软件架构：

```text
Application

↓

SDK

↓

Device Driver

↓

Firmware

↓

Detector
```

SDK 为应用程序提供统一的软件接口。

---

# 4. Failure Modes

| Failure Mode | Description |
|--------------|-------------|
| SDK Initialization Failure | SDK 初始化失败 |
| API Call Failure | API 调用失败 |
| Device Discovery Failure | 设备发现失败 |
| Device Connection Failure | 设备连接失败 |
| Parameter Configuration Failure | 参数配置失败 |
| Image Acquisition Failure | 图像采集失败 |
| Callback Failure | 回调函数异常 |
| Memory Management Failure | 内存管理异常 |
| Version Compatibility Failure | SDK 版本不兼容 |
| Exception Handling Failure | 异常处理失败 |

---

# 5. Failure Mechanisms

## 5.1 SDK Initialization Failure

SDK 初始化失败。

影响：

- SDK 无法使用

典型表现：

- Initialize Failed
- SDK Load Failed

---

## 5.2 API Call Failure

API 返回错误。

影响：

- 功能无法执行

典型表现：

- Invalid Handle
- API Return Error

---

## 5.3 Device Discovery Failure

无法搜索到 Detector。

影响：

- 无法建立连接

典型表现：

- No Device Found

---

## 5.4 Device Connection Failure

SDK 无法连接设备。

影响：

- 无法采集图像

典型表现：

- Connection Failed
- Connection Timeout

---

## 5.5 Parameter Configuration Failure

参数设置失败。

包括：

- Exposure
- Trigger Mode
- Gain
- Offset

典型表现：

- Invalid Parameter
- Configuration Failed

---

## 5.6 Image Acquisition Failure

SDK 无法接收图像。

影响：

- Image Lost
- Timeout

---

## 5.7 Callback Failure

事件回调异常。

影响：

- 图像未通知
- 状态更新失败

---

## 5.8 Memory Management Failure

SDK 内存申请或释放异常。

影响：

- Memory Leak
- Crash

---

## 5.9 Version Compatibility Failure

SDK 与 Driver、Firmware 不兼容。

影响：

- API 不支持
- 功能异常

---

## 5.10 Exception Handling Failure

SDK 未正确处理异常。

影响：

- Application Crash
- SDK Crash

---

# 6. Typical Symptoms

| Symptom | Possible Cause |
|----------|----------------|
| SDK Cannot Initialize | Initialization Failure |
| Device Not Found | Discovery Failure |
| Connection Timeout | Connection Failure |
| Image Timeout | Acquisition Failure |
| API Return Error | API Failure |
| Application Crash | Exception Failure |
| Invalid Parameter | Configuration Failure |

---

# 7. Failure Impact

| Module | Impact |
|---------|--------|
| Application | 无法控制 Detector |
| Image Acquisition | 图像采集失败 |
| Communication | 数据接收异常 |
| Workflow | 中断 |
| Entire Software | 功能不可用 |

---

# 8. Detection Methods

## SDK Version Check

检查：

- SDK Version
- API Version
- Release Note

---

## API Return Value

检查：

- Return Code
- Error Code
- Exception Information

---

## Log Analysis

检查：

- SDK Log
- Application Log
- Driver Log

---

## Compatibility Verification

确认：

- SDK
- Driver
- Firmware
- Operating System

版本是否匹配。

---

## Sample Program Test

运行官方 Demo：

- Device Discovery
- Connection
- Acquisition
- Image Reception

---

# 9. Root Cause Analysis

```text
Application Failure

↓

SDK Initialize？

↓

NO

↓

SDK Installation

↓

YES

↓

Device Found？

↓

NO

↓

Driver

↓

YES

↓

Image Received？

↓

NO

↓

Communication

↓

YES

↓

Check Application
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Wrong SDK Version | SDK 版本错误 |
| Driver Incompatible | 驱动不兼容 |
| Firmware Incompatible | 固件不兼容 |
| API Misuse | API 调用错误 |
| Callback Not Registered | 回调未注册 |
| Memory Leak | 内存泄漏 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 单个 API 异常 |
| Moderate | 部分功能不可用 |
| Major | 无法采集图像 |
| Critical | SDK 无法使用 |

---

# 12. Engineering Recommendations

建议：

- 使用官方 SDK。
- 保持 SDK、Driver、Firmware 版本一致。
- 检查 API 返回值，不忽略错误码。
- 优先使用官方 Demo 验证环境。
- SDK 异常确认前，应先排除 Driver、Firmware 和 Communication 故障。

---

# 13. Relationship with Other Modules

## DriverFailure

SDK 依赖 Driver 完成设备访问。

---

## FirmwareFailure

SDK 的设备控制最终由 Firmware 执行。

---

## ConnectionWorkflow

SDK 负责设备发现与连接。

---

## CommunicationWorkflow

SDK 负责图像及命令数据收发。

---

## ImageGenerationWorkflow

SDK 接收图像数据并交付上层应用。

---

## DecisionTree

SDK Failure 是以下诊断的重要节点：

- SDK Initialize Failed
- Device Discovery Failed
- Connection Timeout
- API Error
- Image Timeout

---

# 14. Knowledge Graph

```text
Application

↓

SDK

├── Initialization Failure
├── API Failure
├── Discovery Failure
├── Connection Failure
├── Configuration Failure
├── Acquisition Failure
├── Callback Failure
├── Memory Failure
├── Version Failure
└── Exception Failure

↓

Driver

↓

Firmware

↓

Detector

↓

System Symptoms

↓

DecisionTree
```

---

# 15. Summary

SDK Failure 是 Flat Panel Detector 软件系统中连接应用程序与底层驱动的重要故障类型，其主要表现为初始化失败、API 调用异常、设备发现失败、连接失败、图像采集失败、版本不兼容及异常处理错误等。由于 SDK 是应用软件访问 Detector 的统一接口，其故障通常导致设备无法控制、图像无法获取或软件运行异常。故障分析应结合 SDK 日志、API 返回值、版本兼容性及官方 Demo 进行综合判断，为 DecisionTree 和现场技术支持提供可靠依据。