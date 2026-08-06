# Case

Version: V1.0

Module: 11_Case

Status: Released

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Wired Detector
- Wireless Detector
- Pluto Series
- Veterinary DR
- Medical DR
- Industrial Detector（部分案例适用）

Related Documents:

- ../06_Workflow/
- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/
- ../09_DecisionTree/
- ../12_ErrorCode/
- ../17_Tools/

---

# 1. Overview

Case 模块用于沉淀 FAE（Field Application Engineer）在现场安装、调试、维修、培训及客户支持过程中积累的真实案例。

与 Workflow 不同：

- Workflow 描述标准操作流程。
- FailureKnowledge 介绍故障原理。
- ImageDiagnosis 分析图像异常特征。
- DecisionTree 提供故障定位路径。
- **Case 记录真实现场案例及最终解决方案。**

Case 是整个知识库中最贴近现场工作的模块，也是持续更新频率最高的模块。

---

# 2. Objectives

Case 模块目标：

- 沉淀现场经验
- 提高故障定位效率
- 避免重复踩坑
- 建立标准案例库
- 为新人培训提供参考
- 为研发提供现场反馈依据

---

# 3. Module Structure

```text
11_Case

├── README.md
│
├── Communication
│
├── Calibration
│
├── Image
│
├── Firmware
│
├── Software
│
├── Customer
│
└── EngineeringExperience（规划中）
```

说明：

- **Communication**：连接、网络及通信相关案例。
- **Calibration**：Offset、Gain、Defect、Ghost 等校准案例。
- **Image**：图像异常及处理案例。
- **Firmware**：固件升级、版本管理及兼容性案例。
- **Software**：SDK、License、软件配置案例。
- **Customer**：送样、OQC、客户支持及现场服务案例。
- **EngineeringExperience**：长期积累的工程经验（规划中）。

---

# 4. Case Classification

建议所有案例按以下类型分类：

## 4.1 Communication

例如：

- Detector Connection Failed
- Detector Offline
- Ping Failed
- Image Loss
- Timeout
- Network Configuration Error

---

## 4.2 Calibration

例如：

- Offset Generation Failed
- Gain Generation Failed
- Defect Generation Failed
- Ghost Correction
- Dynamic Calibration
- Pluto0900X Color Calibration

---

## 4.3 Image

例如：

- Vertical Line
- Horizontal Line
- White Pixel
- Black Pixel
- Noise
- Lag
- Ghost
- Mosaic
- Image Shift

---

## 4.4 Firmware

例如：

- Firmware Upgrade Failed
- Firmware Version Mismatch
- Boot Failure
- FPGA Upgrade Failure

---

## 4.5 Software

例如：

- License Locked
- SDK Exception
- Configuration Error
- Mode Configuration Error

---

## 4.6 Customer

例如：

- Sample Test
- OQC Inspection
- Customer Training
- Warranty Processing
- RMA Analysis

---

# 5. Standard Case Template

所有案例建议统一采用以下结构：

```text
Case Name

↓

Problem Description

↓

Applicable Products

↓

Environment

↓

Fault Phenomenon

↓

Root Cause Analysis

↓

Diagnostic Process

↓

Solution

↓

Verification

↓

Engineering Experience

↓

Related Documents
```

统一结构有利于案例检索和后期维护。

---

# 6. Case Writing Principles

建议遵循以下原则：

## 真实性

所有案例应来源于：

- 客户现场
- 公司实验室
- 培训记录
- 内部验证

避免记录未经验证的推测。

---

## 可复现

应尽量描述：

- 操作步骤
- 环境条件
- 软件版本
- Firmware 版本
- Detector 型号

保证其他工程师能够复现问题。

---

## 可验证

解决方案应具有明确验证方式，例如：

- 图像恢复正常
- 校准成功
- 通信恢复
- 日志无异常
- 连续运行稳定

---

## 可追溯

建议记录：

- 日期
- 产品型号
- Detector SN（如允许）
- Firmware Version
- SDK Version
- 作者
- 来源

便于后续更新。

---

# 7. Recommended Information

每个案例建议包含：

基础信息：

- Product Model
- Detector Model
- Firmware Version
- FPGA Version
- SDK Version
- Operating System

现场信息：

- Customer
- Project
- Environment
- Network Topology

故障信息：

- Fault Description
- Fault Frequency
- Reproduction Method

解决过程：

- Diagnostic Steps
- Root Cause
- Solution

最终结果：

- Verification
- Preventive Actions

---

# 8. Relationship with Other Modules

Case 不独立存在，应与其它模块建立关联。

```text
Case

↓

DecisionTree
（快速定位）

↓

FailureKnowledge
（故障原理）

↓

Workflow
（标准流程）

↓

Tools
（执行工具）

↓

ImageDiagnosis
（图像分析）

↓

ErrorCode
（错误信息）
```

例如：

```
Case：
Image Loss

↓

DecisionTree：
Image Loss Decision Tree

↓

FailureKnowledge：
Network Failure

↓

Workflow：
Connection Workflow

↓

Tools：
LogExport
Wireshark

↓

ImageDiagnosis：
Noise
```

通过交叉引用形成完整的故障处理链路。

---

# 9. Engineering Experience

Case 模块重点记录官方文档中通常不会涉及，但经过现场验证的工程经验。

例如：

- Pluto0900X 彩图校准过程中，第 63 张图像后不要提前停止曝光，应等待 SDK 自动完成第 64 张采集。
- Detector 连接失败时，仅修改当前连接探测器的网卡 IP，其余网络配置保持不变。
- Image Loss 排查时，应优先检查 Jumbo Frame、网卡驱动、Packet Size 及 Frame Rate。
- Firmware 升级完成后建议断电等待 10～20 秒，再重新上电。

工程经验应注明适用平台及版本，避免不同产品间直接套用。

---

# 10. Continuous Maintenance

Case 模块属于持续更新模块。

建议：

新增案例：

- 新产品问题
- 新 Firmware
- 新 SDK
- 新客户现场问题

更新已有案例：

- 新版本解决方案
- 新增排查方法
- 增加注意事项

定期复审：

建议每季度或重大版本发布后，对案例进行检查和更新。

---

# 11. References

- Workflow Module
- FailureKnowledge Module
- ImageDiagnosis Module
- SDK Tool Documents
- Internal Training Materials
- FAE Engineering Experience

---

# 12. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Case 模块导航文档，定义案例分类、编写规范及与知识库其它模块的关联关系。 |