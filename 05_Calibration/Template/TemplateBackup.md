# TemplateBackup

Version: V2.0

Module: Calibration

Source Level:
- Engineering
- Maintenance

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- CalibrationTemplate.md
- TemplateManagement.md
- TemplateVersion.md
- TemplateTroubleshooting.md
- ../CalibrationTheory/CalibrationData.md
- ../../04_Software/iDetector.md
- ../../11_SOP/

---

# 1. Purpose

Template Backup 定义 Calibration Template 的备份、恢复及迁移规范。

本文件用于保证 Calibration Data 的安全性、完整性及可恢复性，防止因设备故障、软件升级、数据损坏或误操作导致 Calibration Data 丢失。

---

# 2. Scope

适用于所有 Calibration Template，包括：

- Factory Template
- User Template
- Active Template
- Backup Template
- Archive Template

---

# 3. Backup Objective

Template Backup 的目标包括：

- 防止 Calibration Data 丢失
- 快速恢复 Detector 工作状态
- 保证 Calibration Data 可追溯
- 支持设备维修与更换
- 支持软件升级
- 支持现场维护

---

# 4. Backup Content

标准 Backup 应包含以下内容：

- Offset Data
- Gain Data
- Defect Template
- Calibration Metadata
- Template Version Information

建议同时保存：

- Detector Model
- Detector Serial Number
- Firmware Version
- Software Version
- Calibration Date
- Operator
- Backup Time

---

# 5. Backup Trigger

建议在以下情况执行 Backup：

- Factory Calibration 完成
- Offset Calibration 更新
- Gain Calibration 更新
- Defect Calibration 更新
- Calibration Template 更新
- Detector 维修完成
- 软件升级前
- Firmware 升级前
- 更换主机前
- 定期维护

---

# 6. Backup Workflow

```text
Verify Calibration Data

↓

Verify Template

↓

Verify Version

↓

Export Template

↓

Generate Backup File

↓

Verify Backup Integrity

↓

Archive Backup
```

Backup 完成后，应确认备份文件完整可用。

---

# 7. Backup Verification

Backup 完成后，应检查：

- Backup Success
- File Integrity
- Template Version
- Calibration Data Integrity
- Metadata Completeness
- File Readability

确认无误后方可归档。

---

# 8. Backup Storage

建议采用多级存储策略：

Primary Backup

- 工程师维护电脑

Secondary Backup

- 服务器
- NAS
- 企业文件管理系统

Archive Backup

- 长期归档存储

避免仅保存单一副本。

---

# 9. Restore Purpose

Restore 用于恢复已保存的 Calibration Template。

适用于：

- Calibration Data 丢失
- Detector 更换控制板
- 软件异常
- Firmware 异常
- Template 损坏
- 版本回退

---

# 10. Restore Workflow

```text
Select Backup

↓

Verify Compatibility

↓

Verify Version

↓

Upload Template

↓

Activate Template

↓

Verify Image Quality
```

Restore 后必须重新验证图像质量。

---

# 11. Restore Verification

恢复完成后，应确认：

- Template Upload Success
- Active Template Updated
- Calibration Data Loaded
- Version Correct
- Offset Correction Normal
- Gain Correction Normal
- Defect Correction Normal

确认通过后恢复正常使用。

---

# 12. Template Migration

Template Migration 用于 Calibration Data 的迁移。

典型场景：

- 主机更换
- 系统重装
- 软件升级
- 数据迁移

迁移前必须确认：

- Detector Model 一致
- Hardware Revision 一致
- Firmware Compatibility
- Software Compatibility

不同 Detector 之间禁止直接迁移 Calibration Template。

---

# 13. Backup Integrity

Backup 文件应满足：

- 数据完整
- Metadata 完整
- Version 正确
- 文件无损坏
- 可正常读取
- 可成功恢复

必要时应采用校验机制（如 CRC 或 Hash）验证文件完整性。

---

# 14. Backup Failure

常见 Backup 异常包括：

- Backup Failed
- Export Failed
- File Corruption
- Storage Full
- File Permission Denied
- Backup Interrupted
- Restore Failed
- Compatibility Error
- Version Mismatch

详细排查见：

TemplateTroubleshooting.md

---

# 15. Best Practices

建议遵循以下原则：

- 每次 Calibration 更新后立即 Backup。
- Factory Template 永久保留。
- 保留多个历史版本。
- Backup 与 Detector SN 一一对应。
- Restore 前完成 Compatibility Check。
- Restore 后执行完整图像验证。
- 定期验证 Backup 文件可恢复性。

---

# 16. Backup Lifecycle

```text
Calibration Complete

↓

Generate Template

↓

Backup

↓

Verify

↓

Archive

↓

Restore (If Required)

↓

Activate

↓

Image Verification
```

---

# 17. Relationship with Other Modules

Template：

- CalibrationTemplate.md
- TemplateManagement.md
- TemplateVersion.md
- TemplateTroubleshooting.md

Calibration：

- ../Offset/
- ../Gain/
- ../Defect/

Theory：

- ../CalibrationTheory/CalibrationData.md

Software：

- ../../04_Software/iDetector.md

SOP：

- ../../11_SOP/

---

# 18. Document Boundary

本文件负责：

- Calibration Template Backup
- Restore
- Migration
- Backup Verification
- Backup Storage
- Backup Best Practices

本文件不负责：

- Template 生命周期管理
- Template Version 定义
- Template 故障排查
- Calibration 算法
- 软件界面操作
- SDK API

上述内容分别由对应文档说明。

---

# 19. Knowledge Graph

```text
Calibration Template

↓

Backup

↓

Verification

↓

Archive

↓

Restore

↓

Activate

↓

Image Verification

↓

Normal Operation
```

---

# 20. Summary

Template Backup 是 Calibration Data 生命周期中的关键环节。

通过建立标准化的 Backup、Restore、Migration 及 Verification 流程，可以有效保护 Calibration Data，降低数据丢失风险，提升设备维护效率，并确保 Detector 在维修、升级或异常恢复后能够快速恢复到稳定、可靠的工作状态。