# TemplateVersion

Version: V2.0

Module: Calibration

Source Level:
- Engineering
- Product Implementation

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- CalibrationTemplate.md
- TemplateManagement.md
- TemplateBackup.md
- TemplateTroubleshooting.md
- ../Defect/DefectTemplate.md
- ../CalibrationTheory/CalibrationData.md
- ../../04_Software/iDetector.md

---

# 1. Purpose

Template Version 定义 Calibration Template 的版本管理原则。

本文件说明 Calibration Template 的版本组成、版本生命周期、版本一致性检查、版本兼容性及更新原则，为 Calibration Data 的长期维护和产品升级提供统一规范。

---

# 2. Scope

适用于所有 Calibration Template，包括：

- Factory Template
- User Template
- Active Template
- Backup Template
- Restore Template

---

# 3. Version Definition

Template Version 用于唯一标识一个 Calibration Template。

一个完整的 Template Version 应能够唯一对应一组 Calibration Data。

Version 应具有：

- 唯一性（Uniqueness）
- 可追溯性（Traceability）
- 一致性（Consistency）
- 可验证性（Verifiability）

---

# 4. Version Composition

Template Version 建议包含以下信息：

- Template ID
- Template Type
- Product Model
- Detector Serial Number
- Firmware Version
- Software Version
- Calibration Version
- Calibration Date
- Operator
- Template Status

其中：

Template Status 包括：

- Factory
- User
- Active
- Backup
- Archive

---

# 5. Template Types

## Factory Template

Factory Calibration 生成。

特点：

- 出厂版本
- 默认模板
- 一般不允许修改
- 可作为恢复基准

---

## User Template

现场重新 Calibration 或人工编辑后生成。

特点：

- 可更新
- 可替换
- 可重新生成

---

## Active Template

当前参与图像校正的 Template。

系统始终只允许一个 Active Template。

Image Pipeline 仅读取 Active Template。

---

## Backup Template

用于数据备份。

不参与图像处理。

仅用于恢复历史 Calibration Data。

---

## Archive Template

历史归档版本。

用于版本追溯及技术分析。

---

# 6. Version Lifecycle

```text
Factory Version

↓

User Calibration

↓

New Version

↓

Verification

↓

Activation

↓

Backup

↓

Archive
```

整个生命周期应保持版本连续性。

---

# 7. Version Update

以下情况应生成新的 Template Version：

- 完成 Offset Calibration
- 完成 Gain Calibration
- 完成 Defect Calibration
- 更新 Calibration Data
- 修改 Defect Template
- Detector 维修
- Factory Template 更新

每次更新均应形成新的 Version。

---

# 8. Version Consistency

Version 一致性应检查：

- Template Version
- Calibration Data Version
- Firmware Version
- Software Version
- Detector Model
- Detector SN

若存在不一致，应停止 Template Activation。

---

# 9. Version Compatibility

Template 应与以下内容保持兼容：

- Detector Model
- Detector Hardware Revision
- Firmware
- Driver
- SDK
- Image Processing Module

不同产品或不同硬件版本之间，不应直接混用 Calibration Template。

---

# 10. Version Verification

Version 验证包括：

- Template 完整性
- 数据完整性
- Metadata 完整性
- CRC（如产品支持）
- Version 一致性
- Calibration Time 合法性

验证通过后方可激活。

---

# 11. Version Switching

切换 Template Version 时，应执行：

```text
Current Active Template

↓

Load Target Version

↓

Verify

↓

Activate

↓

Image Verification
```

切换过程中不得中断 Calibration Data。

---

# 12. Version Rollback

若新 Version 出现异常，可执行 Rollback。

Rollback 流程：

```text
Current Version

↓

Load Backup Version

↓

Verify

↓

Activate

↓

Image Test
```

Rollback 后应重新确认图像质量。

---

# 13. Common Version Issues

常见问题包括：

- Version Mismatch
- Version Corruption
- Wrong Active Version
- Unsupported Version
- Incomplete Version Information
- Firmware Compatibility Error
- Software Compatibility Error

---

# 14. Best Practices

建议遵循以下原则：

- 每次 Calibration 后生成新的 Version。
- Factory Template 保持只读。
- User Template 修改后重新编号。
- Activation 前完成 Version Verification。
- 保留最近多个历史版本，便于回退。
- 重大软件升级后重新验证 Template Compatibility。

---

# 15. Relationship with Template Management

Template Version 是 Template Management 的组成部分。

管理流程如下：

```text
Generate

↓

Assign Version

↓

Verify

↓

Save

↓

Activate

↓

Backup

↓

Archive
```

---

# 16. Relationship with Calibration Data

每个 Template Version 均对应唯一的 Calibration Data。

```text
Calibration Data

↓

Template Version

↓

Active Template

↓

Image Processing
```

Calibration Data 更新后，应同步更新 Template Version。

---

# 17. Related Documents

Template：

- CalibrationTemplate.md
- TemplateManagement.md
- TemplateBackup.md
- TemplateTroubleshooting.md

Calibration：

- ../Defect/DefectTemplate.md

Theory：

- ../CalibrationTheory/CalibrationData.md

Software：

- ../../04_Software/iDetector.md

---

# 18. Document Boundary

本文件负责：

- Template Version 定义
- Version 生命周期
- Version 一致性
- Version 兼容性
- Version 更新
- Version 回退

本文件不负责：

- Template 上传下载
- Backup 操作流程
- Calibration 算法
- 软件界面
- SDK API

上述内容分别由对应文档说明。

---

# 19. Summary

Template Version 是 Calibration Template 生命周期管理的重要组成部分。

通过统一的版本编号、版本验证、兼容性检查及版本回退机制，可以确保 Detector 始终使用正确、可追溯且兼容的 Calibration Data，为 Image Processing 提供稳定可靠的校准基础，并为设备维护、软件升级及故障恢复提供版本保障。