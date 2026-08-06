# LogExport

Version: V1.0

Module: 17_Tools / SDKTool

Status: Draft

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- SDK_AIO Platform

Related Documents:

- README.md
- FirmwareUpgrade.md
- CalibrationTools.md
- ../../06_Workflow/WorkflowTroubleshooting.md

---

# 1. Purpose

Log Export 用于导出 SDK、Detector 及 Firmware 运行日志，为研发、FAE 及技术支持提供故障分析依据。

日志通常用于分析：

- Detector Connection Failure
- Image Loss
- Timeout
- Calibration Failure
- Firmware Upgrade Failure
- Trigger Failure
- Network Communication Failure
- SDK Exception

---

# 2. Log Classification

常见日志包括：

```text
Logs

├── SDK Log
├── Detector Log
├── Firmware Log
├── FPGA Log（部分平台）
├── Network Log
├── Calibration Log
└── Upgrade Log
```

不同故障需要对应日志。

---

# 3. Export Workflow

标准流程：

```text
Open SDK

↓

Enter Diagnostic Page

↓

Enable Log

↓

Reproduce Problem

↓

Stop Acquisition

↓

Export Log

↓

Compress Files

↓

Send To R&D
```

建议在问题复现后立即导出日志。

---

# 4. Recommended Log Information

建议同时记录：

- Detector SN
- Detector Model
- Firmware Version
- FPGA Version
- SDK Version
- Operating System
- Time of Failure
- Customer Description

---

# 5. Log Collection Checklist

建议收集：

□ SDK Log

□ Detector Log

□ Firmware Version

□ FPGA Version

□ Calibration Version

□ Detector SN

□ Software Version

□ Error Screenshot

□ Original RAW（如有）

□ Operation Steps

---

# 6. Engineering Experience

## 6.1 日志必须配合操作步骤

仅提供日志通常不足以定位问题。

建议同步记录：

1. 做了什么操作；
2. 问题出现在哪一步；
3. 是否可以稳定复现；
4. 复现概率。

---

## 6.2 出现 Image Loss

建议同时提供：

- SDK Log
- Network Configuration
- Jumbo Frame 配置
- 网卡驱动版本
- Frame Rate 配置

---

## 6.3 出现 Calibration Failure

建议同时提供：

- Calibration Log
- Offset Template
- Gain Template
- Defect Template
- Detector Firmware Version

---

## 6.4 Firmware Upgrade Failure

建议保存：

- Upgrade Log
- Firmware Package Version
- Upgrade Time
- 升级前后版本信息

---

# 7. Common Problems

## Log Empty

检查：

- 是否开启日志记录
- 是否具有写入权限
- 导出路径是否正确

---

## Log Too Large

建议：

- 压缩后发送
- 仅保留问题发生时间段日志

---

## Missing Key Information

确认是否记录：

- Detector SN
- Firmware Version
- SDK Version
- 问题复现步骤

---

# 8. Troubleshooting

建议排查顺序：

```text
Problem Reproduced

↓

Enable Log

↓

Export Log

↓

Collect Version Information

↓

Collect RAW

↓

Collect Screenshots

↓

Package

↓

Send To R&D
```

---

# 9. Best Practices

建议：

- 问题复现后立即导出日志
- 不要覆盖原始日志
- 保留原始 RAW 数据
- 记录详细操作步骤
- 日志与截图一并提交

---

# 10. FAQ

## Q1：为什么研发要求同时提供日志和 RAW？

A：

日志反映软件运行状态，RAW 保留原始图像数据，两者结合才能完整分析问题。

---

## Q2：日志越大越好吗？

A：

不是。

建议提供问题发生前后时间段的日志，提高分析效率。

---

## Q3：除了日志还需要什么？

A：

建议至少提供：

- Detector SN
- Firmware Version
- SDK Version
- 操作步骤
- 错误截图
- RAW 数据（如涉及图像问题）

---

# 11. References

- SDK User Manual
- Internal Troubleshooting Guide
- FAE Engineering Experience

---

# 12. Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| V1.0 | 2026-08 | Initial Release | 建立 Log Export 文档，规范日志导出、收集及提交流程。 |