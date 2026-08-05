# TemplateTroubleshooting

Version: V2.0

Module: Calibration

Source Level:
- Engineering
- Troubleshooting

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- CalibrationTemplate.md
- TemplateManagement.md
- TemplateVersion.md
- TemplateBackup.md
- ../Defect/DefectTemplate.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/
- ../../11_SOP/

---

# 1. Purpose

Template Troubleshooting 定义 Calibration Template 全生命周期中的标准故障排查流程。

本文件用于指导现场工程师分析 Calibration Template 的生成、保存、加载、上传、下载、激活及恢复过程中出现的异常，快速定位故障并恢复 Calibration Data 的正常使用。

---

# 2. Scope

适用于以下异常：

- Template Generate Failed
- Template Save Failed
- Template Load Failed
- Template Upload Failed
- Template Download Failed
- Template Activate Failed
- Template Restore Failed
- Template Backup Failed
- Version Mismatch
- Active Template Invalid
- Calibration Data Invalid

---

# 3. Troubleshooting Principle

Template 故障应遵循由外到内、由基础到应用的排查原则。

标准顺序：

```text
Detector

↓

Communication

↓

Calibration Data

↓

Template Integrity

↓

Template Version

↓

Upload / Download

↓

Activation

↓

Image Verification
```

禁止在未确认故障原因前反复执行 Calibration，以免覆盖有效 Calibration Data。

---

# 4. Standard Workflow

```text
Template Failure

↓

Verify Detector

↓

Verify Communication

↓

Verify Calibration Data

↓

Verify Template

↓

Verify Version

↓

Verify Upload / Download

↓

Verify Activation

↓

Image Verification

↓

Problem Resolved
```

---

# 5. Step 1 — Verify Detector

检查内容：

- Detector 是否 Online
- Detector 是否 Ready
- Firmware 是否正常
- Detector 是否存在 Alarm
- Detector 是否完成 Initialization

异常处理：

恢复 Detector 状态后继续排查。

---

# 6. Step 2 — Verify Communication

检查内容：

- Ethernet Link
- IP Address
- Network Stability
- SDK Connection
- iDetector Connection

异常处理：

恢复通信后重新执行相关操作。

---

# 7. Step 3 — Verify Calibration Data

检查内容：

- Offset Data 是否存在
- Gain Data 是否存在
- Defect Template 是否存在
- Calibration Metadata 是否完整
- Calibration Data 是否损坏

异常处理：

恢复 Calibration Data 或重新导入有效 Template。

---

# 8. Step 4 — Verify Template Integrity

检查内容：

- Template 是否存在
- Template 是否完整
- Template 是否损坏
- Template 是否包含全部 Calibration Data
- Template Metadata 是否完整

异常处理：

重新生成或恢复 Template。

---

# 9. Step 5 — Verify Version

检查内容：

- Template Version
- Detector Model
- Detector Serial Number
- Firmware Version
- Software Version
- Calibration Version

确认 Version 一致且兼容。

异常处理：

切换至兼容版本或重新生成 Template。

---

# 10. Step 6 — Verify Upload / Download

检查内容：

- Upload 是否完成
- Download 是否完成
- 文件是否完整
- 传输过程中是否中断
- Detector 是否正确接收 Template

异常处理：

重新执行 Upload 或 Download，并确认结果。

---

# 11. Step 7 — Verify Activation

检查内容：

- Active Template 是否更新
- Detector 是否重新加载 Calibration Data
- Image Pipeline 是否使用新的 Template
- Template Status 是否为 Active

异常处理：

重新 Activate Template，并重新启动相关服务（如产品要求）。

---

# 12. Step 8 — Image Verification

完成 Template 更新后，应采集测试图像确认：

- Offset Correction 正常
- Gain Correction 正常
- Defect Correction 正常
- 图像均匀性正常
- Bad Pixel 已校正
- 无新增 Image Artifact

若图像异常，应继续分析 Calibration Data 或硬件状态。

---

# 13. Common Failure and Action

| Failure | Recommended Action |
|----------|--------------------|
| Template Generate Failed | 检查 Calibration 是否完成 |
| Template Save Failed | 检查存储空间及写入权限 |
| Template Load Failed | 检查文件完整性及版本 |
| Template Upload Failed | 检查网络连接及 Detector 状态 |
| Template Download Failed | 检查通信状态及文件保存路径 |
| Template Activate Failed | 检查 Active Template 是否更新 |
| Version Mismatch | 使用兼容版本 Template |
| Calibration Data Invalid | 恢复 Backup Template 或重新 Calibration |

---

# 14. Root Cause Classification

## Detector

- Detector Offline
- Initialization Failure
- Hardware Fault

---

## Communication

- Ethernet Disconnect
- Network Timeout
- SDK Communication Failure

---

## Storage

- Template File Missing
- Storage Full
- File Corruption
- Read / Write Failure

---

## Version

- Template Version Mismatch
- Firmware Compatibility Issue
- Software Compatibility Issue
- Wrong Detector Model

---

## Calibration

- Offset Data Missing
- Gain Data Missing
- Defect Template Missing
- Calibration Data Corruption

---

## Software

- Firmware Exception
- iDetector Exception
- Template Management Failure

---

# 15. Decision Tree

```text
Template Failure

├── Detector
│       ↓
│   Restore Detector
│
├── Communication
│       ↓
│   Restore Network
│
├── Calibration Data
│       ↓
│   Restore Data
│
├── Template Integrity
│       ↓
│   Rebuild / Restore
│
├── Version
│       ↓
│   Verify Compatibility
│
├── Upload / Download
│       ↓
│   Retry Transfer
│
├── Activation
│       ↓
│   Activate New Template
│
└── Image Verification
        ↓
    Confirm Image Quality
```

---

# 16. Escalation Criteria

出现以下情况应升级处理：

- Template 无法恢复
- Calibration Data 损坏
- Active Template 持续无效
- Version 无法匹配
- Detector 无法加载 Calibration Data
- 图像持续异常且排除 Calibration 原因
- 怀疑 Detector Hardware Failure

---

# 17. Troubleshooting Output

排查完成后，应形成以下记录：

- Failure Description
- Root Cause
- Affected Module
- Corrective Action
- Template Version
- Calibration Data Status
- Image Verification Result
- 是否恢复 Backup Template
- 是否重新 Calibration

---

# 18. Related Documents

Template：

- CalibrationTemplate.md
- TemplateManagement.md
- TemplateVersion.md
- TemplateBackup.md

Calibration：

- ../Defect/DefectTemplate.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

SOP：

- ../../11_SOP/

---

# 19. Knowledge Graph

```text
Template Failure

↓

Detector

↓

Communication

↓

Calibration Data

↓

Template Integrity

↓

Template Version

↓

Upload / Download

↓

Activation

↓

Image Verification

↓

Root Cause

↓

Corrective Action
```

---

# 20. Document Boundary

本文件负责：

- Template 故障排查流程
- Template 生命周期检查
- Version 检查
- Calibration Data 检查
- 故障定位方法
- 排查输出

本文件不负责：

- Template 管理规范
- Version 定义
- Backup 操作规范
- Calibration 算法
- SDK API
- 软件界面操作

上述内容分别由对应文档说明。

---

# 21. Reference

## Fact

- 产品培训资料关于 Calibration Template 的生成、保存、加载、上传、下载、激活及恢复流程。
- 产品用户手册关于 Calibration Data 管理及模板维护要求。

## Engineering

- Template 故障排查应遵循 **Detector → Communication → Calibration Data → Template Integrity → Template Version → Upload / Download → Activation → Image Verification** 的标准路径。
- 任何 Template 更新或恢复完成后，均应执行图像验证，确认新的 Calibration Data 已正确参与 Image Processing。