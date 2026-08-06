# FirmwareUpgrade

Version: V1.0

Module: 17_Tools / SDKTool

Status: Draft

Applicable Products:

- Wired Flat Panel Detector
- Wireless Flat Panel Detector
- Dynamic Detector
- Static Detector

Related Documents:

- README.md
- LicenseManagement.md
- ModeConfiguration.md
- ../../06_Workflow/InitializationWorkflow.md
- ../../06_Workflow/ConfigurationWorkflow.md

---

# 1. Purpose

Firmware Upgrade 用于更新探测器内部 Firmware（固件），修复软件缺陷、增加新功能或适配新的 SDK 版本。

Firmware 升级属于高风险操作，升级过程中若出现异常，可能导致：

- Detector 无法启动
- Detector 无法连接
- Detector 无法采图
- 参数丢失
- Calibration 失效

因此必须严格按照标准流程执行。

---

# 2. Firmware Overview

Firmware 是运行在 Detector MCU / FPGA / Control Board 内部的软件程序。

主要负责：

- Detector 初始化
- 通信管理
- 图像采集控制
- Trigger 控制
- Mode 管理
- 图像传输
- 参数管理

Firmware 与 SDK、FPGA、硬件版本存在兼容关系。

升级 Firmware 前必须确认版本匹配。

---

# 3. Upgrade Prerequisites

升级前应确认以下内容：

- Detector 可正常连接
- 当前 Firmware Version 已记录
- 当前 FPGA Version 已记录
- SDK Version 已确认
- Detector SN 已记录
- 电源稳定
- 网络连接正常

升级过程中禁止：

- 断电
- 拔网线
- 强制关闭升级软件
- 重启电脑

---

# 4. Firmware Package

Firmware 包应来自正式发布版本。

### 工程经验（现场流程）

Firmware 路径通常位于：

```text
SVN
└── Software
    └── 01-DevelopmentVersion
        └── 324-SDK_AIO
            └── 03_ReleasePackage
```

升级前应确认：

- Firmware 型号正确
- Firmware 版本正确
- 与 Detector 型号一致

严禁使用未经验证的测试版本进行现场升级。

---

# 5. Standard Upgrade Workflow

标准升级流程如下：

```text
确认 Detector 信息

↓

保存出厂参数

↓

确认 Firmware 包

↓

开始 Firmware Upgrade

↓

等待升级完成

↓

断电

↓

等待 10~20 秒

↓

重新上电

↓

连接 Detector

↓

验证 Firmware Version

↓

验证功能正常

↓

升级完成
```

---

# 6. Backup Before Upgrade

升级 Firmware 前必须保存：

- Factory Parameters
- Detector Configuration
- Calibration Parameters（如支持）
- 当前 Firmware Version

建议同时记录：

- Detector SN
- Upgrade Date
- Upgrade Operator

便于后续追溯。

---

# 7. Upgrade Verification

升级完成后，应进行以下验证：

## 7.1 Version Check

确认：

- Firmware Version
- FPGA Version
- SDK Version

版本是否符合要求。

---

## 7.2 Detector Connection

确认：

- Detector Online
- 网络正常
- SDK 可识别 Detector

---

## 7.3 Image Acquisition

执行一次标准采图。

确认：

- 可以正常曝光
- 图像正常生成
- 无 Timeout
- 无 Image Loss

---

## 7.4 Calibration Status

确认：

- Offset 可生成
- Gain 正常
- Defect 正常

若校准异常，应重新确认 Firmware 与模板兼容性。

---

# 8. Engineering Experience

## 8.1 升级前必须保存出厂参数

升级 Firmware 前，首先保存 Detector 出厂参数。

若 Firmware 升级失败，可用于恢复设备配置。

---

## 8.2 Firmware 来源

建议仅使用正式 Release Package。

不要使用：

- Debug 版本
- 临时测试版本
- 未评审版本

---

## 8.3 升级完成后必须断电

### 工程经验

Firmware 升级完成后：

必须关闭 Detector 电源。

等待：

```text
10 ~ 20 秒
```

然后重新上电。

目的：

确保 Firmware 完全重新加载。

---

## 8.4 OQC 版本确认

送样或返修设备升级 Firmware 后，应在 OQC 确认：

- Firmware Version
- FPGA Version

是否一致。

若版本不一致：

不得直接发货。

应联系研发确认并完成评审。

---

## 8.5 升级记录

建议保存：

- Upgrade Time
- Firmware Version
- Detector SN
- Upgrade Operator

便于售后追踪。

---

# 9. Common Problems

## Firmware Upgrade Failed

可能原因：

- Firmware 包错误
- 网络中断
- 电源异常

---

## Detector Offline

可能原因：

- Firmware 未正常启动
- 网络配置异常
- Firmware 不兼容

---

## Detector Cannot Acquire Image

检查：

- Firmware Version
- SDK Version
- Mode Configuration

---

## Calibration Failed

检查：

- Calibration Template
- Firmware Compatibility
- Detector Parameters

---

# 10. Troubleshooting

建议按以下顺序排查：

```text
Firmware Package

↓

Detector Model

↓

Firmware Version

↓

FPGA Version

↓

Network

↓

Power

↓

Restart Detector

↓

Image Acquisition Test
```

---

# 11. Best Practices

建议：

- 升级前备份参数
- 使用正式 Release Package
- 升级完成后断电 10~20 秒
- 验证版本一致性
- 完成一次完整采图测试
- 保存升级记录

---

# 12. FAQ

## Q1：升级完成后为什么要断电？

A：

根据现场工程经验，Firmware 写入完成后需要重新上电，使 MCU、FPGA 及相关模块重新初始化。建议断电等待 **10~20 秒** 后再重新上电。

---

## Q2：Firmware 升级后需要重新校准吗？

A：

视 Firmware 更新内容而定。

若 Firmware 涉及采集流程、校准算法或硬件参数，建议重新验证 Offset、Gain、Defect 等校准结果。

---

## Q3：发现 Firmware Version 与 OQC 不一致怎么办？

A：

不要直接交付设备。

应联系研发确认版本差异，并完成内部评审后再决定是否继续使用该版本。

---

## Q4：升级过程中可以断电吗？

A：

不可以。

Firmware 写入过程中断电可能导致 Firmware 损坏，使 Detector 无法正常启动。

---

# 13. References

- SDK Release Notes
- Detector Firmware Release Package
- Detector Upgrade SOP
- FAE 现场经验
- 内部研发培训资料

---

# 14. Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| V1.0 | 2026-08 | Initial Release | 建立 Firmware Upgrade 工具文档，包含升级流程、验证方法、工程经验及常见问题。 |