# TemplateManagement

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
- TemplateVersion.md
- TemplateBackup.md
- TemplateTroubleshooting.md
- ../Defect/DefectTemplate.md
- ../../04_Software/iDetector.md

---

# 1. Purpose

Template Management 定义 Calibration Template 的标准管理流程。

本文件描述 Calibration Template 从生成、保存、加载、上传、下载、激活、更新到停用的完整生命周期，为 Calibration Data 管理提供统一规范。

---

# 2. Scope

适用于所有 Calibration Template，包括：

- Factory Template
- User Template
- Active Template

---

# 3. Management Lifecycle

Calibration Template 生命周期如下：

```text
Generate

↓

Verify

↓

Save

↓

Load

↓

Upload

↓

Download

↓

Activate

↓

Use

↓

Backup

↓

Restore

↓

Update

↓

Archive
```

---

# 4. Generate

Template 由 Calibration 完成后自动生成。

生成内容包括：

- Offset Data
- Gain Data
- Defect Template
- Calibration Metadata

生成完成后进入 Verify 阶段。

---

# 5. Verify

生成后应确认：

- Template 完整性
- Calibration Data 完整性
- 数据一致性
- Version 正确
- 无损坏

验证通过后允许保存。

---

# 6. Save

系统保存 Calibration Template。

保存后形成新的 Calibration Data。

保存过程中不得中断系统运行。

---

# 7. Load

Detector 初始化时加载 Calibration Template。

加载内容包括：

- Offset Data
- Gain Data
- Defect Template

加载成功后进入 Ready 状态。

---

# 8. Upload

Upload 用于将 Calibration Template 写入 Detector。

执行 Upload 后应确认：

- Upload Success
- Version Correct
- Active Template 已更新

---

# 9. Download

Download 用于从 Detector 导出 Calibration Template。

常见用途：

- 数据备份
- 数据恢复
- 技术分析
- 产品维护

---

# 10. Activate

只有 Active Template 才参与 Image Processing。

Activate 后：

- Calibration Data 更新
- Image Pipeline 使用新的 Calibration Data
- 后续图像采用新的校正参数

---

# 11. Update

以下情况需要更新 Template：

- 完成新的 Calibration
- 新增 Defect Pixel
- Calibration Data 更新
- Detector 维修
- Factory Template 更新

---

# 12. Backup

建议定期备份 Calibration Template。

备份内容包括：

- Offset Data
- Gain Data
- Defect Template
- Calibration Metadata

---

# 13. Restore

Restore 用于恢复已备份的 Calibration Template。

恢复完成后应重新验证：

- Version
- Active Template
- 图像质量

---

# 14. Archive

历史 Template 应归档保存。

归档内容包括：

- Version
- Calibration Time
- Product SN
- Operator
- Calibration Result

---

# 15. Management Rules

Template 管理应遵循以下原则：

- 同一时刻仅允许一个 Active Template。
- Upload 前应完成 Verify。
- Download 后应保持数据完整。
- Update 后应重新验证图像质量。
- Backup 应包含全部 Calibration Data。
- Restore 后应重新激活 Template。

---

# 16. Related Documents

- CalibrationTemplate.md
- TemplateVersion.md
- TemplateBackup.md
- TemplateTroubleshooting.md
- ../Defect/DefectTemplate.md

---

# 17. Document Boundary

本文件负责：

- Template 生命周期管理
- Upload / Download
- Save / Load
- Activate
- Backup / Restore
- Update

本文件不负责：

- Template 版本控制
- Template 故障分析
- Calibration 算法
- SDK API
- 软件界面操作

---

# 18. Summary

Template Management 定义 Calibration Template 的全生命周期管理流程。

通过统一管理 Generate、Verify、Save、Load、Upload、Download、Activate、Backup、Restore 及 Update，保证 Detector 始终使用正确、完整且可追溯的 Calibration Data，为 Image Processing 提供稳定的数据基础。