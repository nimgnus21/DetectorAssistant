# LicenseManagement

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
- FirmwareUpgrade.md
- ../../06_Workflow/ConnectionWorkflow.md
- ../../06_Workflow/ConfigurationWorkflow.md

---

# 1. Purpose

License Management 用于管理探测器的软件授权（License），包括 License 的生成、导入、更换、验证及异常处理。

License 是 SDK 与 Detector 正常工作的授权凭证，没有正确 License 时，探测器可能无法正常采图或部分功能被限制。

License 管理主要应用于：

- 新设备交付
- License 更新
- 图像锁定解除
- SDK 授权更新
- 设备维修
- License 异常恢复

---

# 2. License Overview

License（LIC 文件）用于验证当前 Detector 是否具有合法授权。

通常包含以下信息：

- Detector SN
- Detector Model
- MAC Address（部分平台）
- 授权信息
- 有效范围
- 加密校验信息

License 与 Detector 存在绑定关系。

未经授权的 License 无法正常使用。

---

# 3. Typical Workflow

License 管理流程如下：

```text
Detector Connection

↓

Read Detector Information

↓

Check License Status

↓

Generate License（如需要）

↓

Replace LIC File

↓

Restart SDK / Detector

↓

Verify License

↓

Image Acquisition Test

↓

Finish
```

---

# 4. License File

License 通常表现为：

```text
*.lic
```

例如：

```text
Detector.lic
license.lic
pluto.lic
```

不同 SDK 版本命名可能不同。

---

# 5. License Generation

License 一般由研发或授权系统生成。

生成时通常需要提供：

- Detector SN
- Detector Model
- MAC Address（如需要）
- Customer Information（部分项目）

FAE 一般不负责 License 加密算法，仅负责：

- 获取 License
- 导入 License
- 验证 License

---

# 6. License Replacement

标准流程：

```text
关闭 SDK

↓

备份原 License

↓

复制新的 LIC 文件

↓

覆盖原 License

↓

重新启动 SDK

↓

重新连接 Detector

↓

验证授权状态
```

建议保留原 License 文件作为备份。

---

# 7. License Verification

完成 License 更换后，应确认：

- SDK 能正常识别 Detector
- Detector 可正常连接
- 无授权提示
- 图像可正常采集
- 无功能限制

建议执行一次完整采图验证。

---

# 8. Engineering Experience

## 8.1 图像被锁（Image Locked）

### 现场经验

当 SDK 提示图像被锁或无法正常采图时：

首先确认：

License 是否有效。

若 License 失效：

应重新生成对应 License。

然后：

替换原 LIC 文件。

重新启动 SDK 后再次验证。

---

## 8.2 License 替换

推荐流程：

```text
Backup Original LIC

↓

Copy New LIC

↓

Replace Original File

↓

Restart SDK

↓

Reconnect Detector

↓

Acquire Image
```

避免直接删除原文件。

---

## 8.3 License 与 Detector 对应关系

License 应与：

- Detector SN
- Detector Model

保持一致。

错误 License 可能导致：

- Detector 无法授权
- 图像锁定
- SDK 提示 License Error

---

## 8.4 License 管理建议

建议建立 License 管理记录：

- Detector SN
- License Version
- 更新日期
- 更新人员
- License 来源

便于后续追踪。

---

# 9. Common Problems

## License Error

可能原因：

- License 文件错误
- License 损坏
- Detector 不匹配

---

## Detector Connected But Cannot Acquire Image

检查：

- License 是否有效
- Firmware 是否正常
- SDK 是否识别 License

---

## Image Locked

### 工程经验

若确认：

图像被锁（Image Locked）

建议：

重新计算 License。

替换：

原 LIC 文件。

重新启动 SDK 后验证。

> **说明**
>
> 当前文档基于现场经验，仅记录处理流程。License 的生成算法及授权机制属于厂商内部实现，不在本文档讨论范围内。

---

## SDK Still Reports License Error

检查：

- License 是否放置正确目录
- License 是否覆盖成功
- SDK 是否已重新启动

---

# 10. Troubleshooting

建议按以下顺序排查：

```text
Detector Connection

↓

Detector SN

↓

License File

↓

License Directory

↓

Replace LIC

↓

Restart SDK

↓

Reconnect Detector

↓

Acquire Image
```

---

# 11. Best Practices

建议：

- License 更换前备份原文件
- 使用官方生成的 License
- 更换后重新启动 SDK
- 完成一次完整采图验证
- 建立 License 更新记录

---

# 12. FAQ

## Q1：什么时候需要更换 License？

A：

常见情况包括：

- 图像被锁
- License 失效
- 更换授权
- SDK 更新要求新的 License

---

## Q2：更换 License 后为什么还需要重启 SDK？

A：

多数 SDK 在启动时加载 License。

更换 License 后应重新启动 SDK，使新的授权重新生效。

---

## Q3：可以直接删除原 License 吗？

A：

不建议。

建议：

先备份。

确认新 License 工作正常后，再决定是否保留。

---

## Q4：License 可以多个 Detector 共用吗？

A：

通常不建议。

多数 License 与 Detector 存在绑定关系，应使用对应 Detector 的授权文件。

---

# 13. References

- SDK User Manual
- Detector License Guide
- FirmwareUpgrade.md
- FAE 现场经验
- 内部研发培训资料

---

# 14. Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| V1.0 | 2026-08 | Initial Release | 建立 License 管理文档，包含 License 更换流程、验证方法、工程经验及常见问题。 |