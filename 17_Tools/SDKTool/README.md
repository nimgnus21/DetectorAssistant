# SDKTool

Version: V1.1

Module: 17_Tools

Status: Released

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Wired Detector
- Wireless Detector
- Pluto Series Detector
- SDK_AIO Platform

Related Documents:

- [Configuration Workflow](../../06_Workflow/ConfigurationWorkflow.md)
- [Calibration Workflow](../../06_Workflow/CalibrationWorkflow.md)
- [Mode Workflow](../../06_Workflow/ModeWorkflow.md)
- [Dynamic Acquisition Workflow](../../06_Workflow/DynamicAcquisitionWorkflow.md)
- [Workflow Troubleshooting](../../06_Workflow/WorkflowTroubleshooting.md)

---

# 1. Overview

SDKTool 模块用于介绍 Flat Panel Detector（FPD）开发、调试、校准、升级及故障分析过程中常用的 SDK 配套工具。

本模块重点关注：

- SDK 配置
- Firmware 升级
- License 管理
- Detector 校准
- 动态图像处理
- 日志导出
- 工程经验沉淀

本文档作为 SDKTool 模块的导航入口，不详细介绍工具的具体操作，各工具的使用方法请参考对应文档。

---

# 2. Module Architecture

```text
SDKTool

├── DTDITool.md
├── FirmwareUpgrade.md
├── LicenseManagement.md
├── ModeConfiguration.md
├── CalibrationTools.md
├── LogExport.md
└── iDetectorQuickTroubleshooting.md
```

SDKTool 不保留独立 FAQ 作为第二入口。具体问题应进入对应工具文件、DecisionTree 或 SOP，避免重复结论和版本漂移。

---

# 3. Tool Overview

## DTDITool

文件：`DTDITool.md`

功能：

- 动态 RAW 图像拼接
- TDI 图像重建
- Defect Template 应用
- 图像尺寸恢复
- 图像质量分析

主要适用于：

- Dynamic Detector
- TDI 数据分析
- 图像异常分析

## FirmwareUpgrade

文件：`FirmwareUpgrade.md`

功能：

- Firmware 升级
- Firmware 验证
- 升级记录管理

重点内容：

- 升级流程
- 升级注意事项
- OQC 版本确认
- 现场升级经验

## LicenseManagement

文件：`LicenseManagement.md`

功能：

- License 管理
- LIC 文件替换
- License 验证
- 图像锁定处理

重点内容：

- Image Locked
- License 更换
- License 验证

## ModeConfiguration

文件：`ModeConfiguration.md`

功能：

- Mode 参数配置
- ROI 配置
- Frame Rate 配置
- Trigger 配置
- Dynamic Mode 配置

## CalibrationTools

文件：`CalibrationTools.md`

功能：

- Offset Calibration
- Gain Calibration
- Defect Calibration
- Dynamic Calibration
- Template 管理

## LogExport

文件：`LogExport.md`

功能：

- SDK Log 导出
- Detector Log 收集
- Firmware Log 收集
- 故障信息整理

## iDetectorQuickTroubleshooting

文件：`iDetectorQuickTroubleshooting.md`

用于 SDK 初始化、连接、采图和基础异常的快速排查入口，并与相关 SOP 和 DecisionTree 配合使用。

---

# 4. Typical Engineering Workflow

```text
Detector Connection

↓

Mode Configuration

↓

Calibration

↓

Image Acquisition

↓

Image Analysis

↓

Problem Analysis

↓

Log Export

↓

Firmware / License Processing（如需要）

↓

Verification
```

不同工具贯穿于整个 Detector 生命周期。

---

# 5. Relationship with Other Modules

SDKTool 与知识库其它模块关系如下：

```text
SDKTool

├── Workflow
│      ├── ConfigurationWorkflow
│      ├── CalibrationWorkflow
│      ├── ModeWorkflow
│      └── DynamicAcquisitionWorkflow
│
├── FailureKnowledge
│      ├── CalibrationFailure
│      ├── SoftwareFailure
│      └── SystemFailure
│
├── DecisionTree
│
└── SOP
```

SDKTool 更关注工具使用方法；Workflow、FailureKnowledge、DecisionTree 和 SOP 分别承担流程、故障知识、诊断分流和标准执行职责。

---

# 6. Engineering Principles

使用 SDKTool 时建议遵循以下原则：

- 修改配置前先备份原始数据。
- 升级 Firmware 前保存出厂参数。
- 更换 License 前备份原 LIC 文件。
- 校准前确认 Detector 状态正常。
- 使用与当前 Detector 匹配的 Calibration Template。
- 问题复现后立即导出日志。
- 重要操作完成后执行完整采图验证。

---

# 7. Best Practices

建议建立标准化工具使用流程：

```text
Preparation

↓

Configuration

↓

Calibration

↓

Verification

↓

Image Test

↓

Log Collection

↓

Documentation
```

每次完成重要操作后，应记录：

- Detector SN
- Firmware Version
- FPGA Version
- SDK Version
- 操作时间
- 操作人员
- 操作内容
- 验证结果

形成完整的工程记录。

---

# 8. Engineering Experience

本模块重点记录官方文档中未详细说明，但经过现场验证的工程经验，例如：

- Pluto0900X 校准过程中彩图采集至第 63 张时不要停止曝光，应等待 SDK 自动完成第 64 张采集。
- DTDITool 推荐参数：Row Begin = 5、Step Lines = 2。
- Firmware 升级完成后建议断电等待 10～20 秒再重新上电。
- Image Locked 可通过更换正确的 LIC 文件恢复。
- 多个 Mode 在 ROI、PGA、Binning 一致时，可共用 Gain 与 Defect Template。

以上经验应结合具体 Detector 平台、Firmware 版本及 SDK 版本使用，并持续维护更新。

---

# 9. Future Expansion Rule

后续仅在存在明确真实需求、工具来源和技术支持调用关系时新增工具文档，例如：

- ParameterReference
- ReleaseNotes
- CompatibilityMatrix
- NetworkConfiguration
- PerformanceOptimization
- VersionHistory

不得为预留目录或规划功能创建空文件。

---

# 10. References

- Detector SDK User Manual
- SDK Release Notes
- Detector Firmware Guide
- Dynamic Detector Training Materials
- Internal Engineering Documents
- FAE Engineering Experience

---

# 11. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.1 | 2026-08-10 | Removed empty FAQ entry, converted related workflow paths to verified links, and clarified tool-module boundaries. |
| V1.0 | 2026-08 | Established SDKTool module navigation. |