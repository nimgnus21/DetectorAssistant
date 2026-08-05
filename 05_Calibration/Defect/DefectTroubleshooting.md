# DefectTroubleshooting

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
- DefectWorkflow.md
- DefectParameter.md
- DefectTemplate.md
- DefectFailure.md
- ../CalibrationTheory/DefectTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/
- ../../11_SOP/

---

# 1. Purpose

Defect Troubleshooting 定义 Defect Calibration 及 Defect Template 相关故障的标准排查流程。

本文件用于指导现场工程师按照统一流程分析 Defect Calibration Failure，定位故障位置，确认根因，并制定相应处理措施。

---

# 2. Scope

适用于以下情况：

- Defect Calibration Failed
- Defect Detection Failed
- Defect Template Generation Failed
- Template Upload Failed
- Template Download Failed
- Template Overlay Failed
- Active Template Not Updated
- Defect Correction Failed
- Bad Pixel Still Visible
- Bad Line Still Visible
- Calibration Success but Image Abnormal

---

# 3. Troubleshooting Principle

Defect Calibration 应按照 Calibration Workflow、Signal Flow 及 Template Lifecycle 逐级排查。

排查原则：

- 先确认 Detector 状态
- 再确认 Calibration 基础数据
- 再确认 Calibration Image
- 再确认 Defect Detection
- 最后确认 Template 是否真正参与 Image Correction

禁止直接重新执行 Calibration，应首先确认故障位置。

---

# 4. Standard Workflow

```text
Defect Calibration Failed

↓

Detector Status

↓

Communication Status

↓

Offset Calibration

↓

Gain Calibration

↓

Calibration Image

↓

Defect Detection

↓

Defect Template

↓

Template Upload / Overlay

↓

Calibration Data

↓

Image Verification

↓

Problem Resolved
```

---

# 5. Step 1 — Verify Detector Status

检查内容：

- Detector 是否 Online
- Detector 是否 Ready
- Initialization 是否完成
- 是否存在 Hardware Alarm
- 是否存在 Firmware Alarm

异常处理：

恢复 Detector 正常状态后继续排查。

---

# 6. Step 2 — Verify Communication

检查内容：

- Ethernet Link
- IP Address
- Network Stability
- SDK Connection
- iDetector Connection
- Calibration Command 是否正常发送

异常处理：

恢复通信后重新执行 Calibration。

---

# 7. Step 3 — Verify Offset & Gain Calibration

检查内容：

- Offset Calibration 是否完成
- Gain Calibration 是否完成
- Offset Data 是否有效
- Gain Data 是否有效
- Calibration Data 是否正确加载

异常处理：

若 Offset 或 Gain 数据异常，应重新完成对应 Calibration。

---

# 8. Step 4 — Verify Calibration Image

检查内容：

- Calibration Image 是否成功采集
- 图像是否完整
- 是否存在截断
- 是否存在饱和
- 是否存在曝光异常
- 是否满足 Defect Detection 条件

异常处理：

确认曝光条件及图像质量后重新采集。

---

# 9. Step 5 — Verify Defect Detection

检查内容：

- Detection 是否开始
- Detection 是否完成
- Pixel 是否完成分析
- Defect Pixel 是否识别
- Defect Line 是否识别
- Detection Log 是否存在异常

异常处理：

检查 Detection 模块及相关日志。

---

# 10. Step 6 — Verify Defect Template

检查内容：

- Defect Template 是否生成
- Template 是否完整
- Template Version 是否正确
- Defect Pixel List 是否生成
- Defect Map 是否生成

异常处理：

重新生成 Template，并确认保存成功。

---

# 11. Step 7 — Verify Template Management

检查内容：

- Template Upload 是否成功
- Template Download 是否成功
- Template Overlay 是否完成
- Factory Template 是否存在
- User Template 是否存在
- Active Template 是否更新

异常处理：

重新上传或重新加载 Template，确认 Active Template 已切换。

---

# 12. Step 8 — Verify Calibration Data

检查内容：

- Calibration Data 是否更新
- Defect Template 是否写入 Calibration Data
- Template Version 是否一致
- Calibration Data 是否成功加载

异常处理：

重新更新 Calibration Data，并验证数据一致性。

---

# 13. Step 9 — Verify Image Result

完成 Calibration 后采集测试图像。

检查内容：

- Bad Pixel 是否消失
- Bad Line 是否消失
- Image Continuity
- Interpolation 是否正常
- 是否存在 Residual Defect
- 是否出现新的 Image Artifact

若图像恢复正常，则 Defect Calibration 成功。

---

# 14. Troubleshooting Decision Tree

```text
Defect Calibration Failed

├── Detector Offline
│       ↓
│   Restore Detector
│
├── Communication Failure
│       ↓
│   Restore Communication
│
├── Offset / Gain Failure
│       ↓
│   Complete Required Calibration
│
├── Calibration Image Failure
│       ↓
│   Re-acquire Image
│
├── Defect Detection Failure
│       ↓
│   Check Detection Module
│
├── Template Generation Failure
│       ↓
│   Rebuild Template
│
├── Template Upload / Overlay Failure
│       ↓
│   Reload Active Template
│
├── Calibration Data Failure
│       ↓
│   Update Calibration Data
│
└── Image Still Abnormal
        ↓
    Continue Image Diagnosis
```

---

# 15. Root Cause Classification

| Category | Possible Cause |
|----------|----------------|
| Detector | Detector Offline、Initialization Failure、Hardware Failure |
| Communication | Ethernet Failure、Network Timeout、SDK Communication Failure |
| Calibration Dependency | Offset / Gain Calibration Incomplete |
| Calibration Image | Exposure Error、Image Saturation、Image Truncation |
| Detection | Detection Algorithm Failure、Threshold Error |
| Template | Generation Failure、Upload Failure、Overlay Failure、Version Mismatch |
| Calibration Data | Data Write Failure、Data Read Failure、Synchronization Failure |
| Software | Firmware Exception、iDetector Exception、Template Management Exception |

---

# 16. Escalation Criteria

满足以下任一条件时，应升级处理：

- Defect Calibration 连续失败
- Template 无法生成
- Template Upload 持续失败
- Active Template 无法更新
- Overlay 持续失败
- Calibration Data 持续异常
- Bad Pixel 或 Bad Line 无法校正
- 怀疑 Detector Hardware Failure

---

# 17. Output

Troubleshooting 完成后，应形成以下输出：

- Failure Location
- Root Cause
- Affected Module
- Corrective Action
- Verification Result
- 是否重新 Calibration
- 是否重新生成 Template
- 是否需要返厂维修

---

# 18. Related Documents

Calibration：

- DefectWorkflow.md
- DefectParameter.md
- DefectTemplate.md
- DefectFailure.md

Theory：

- ../CalibrationTheory/DefectTheory.md
- ../CalibrationTheory/CalibrationFlow.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

SOP：

- ../../11_SOP/

---

# 19. Knowledge Graph

```text
Defect Calibration Failure

↓

Detector Check

↓

Communication Check

↓

Offset / Gain Check

↓

Calibration Image

↓

Defect Detection

↓

Defect Template

↓

Template Management

↓

Calibration Data

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

- Defect Calibration 故障排查流程
- Defect Template 排查流程
- Template 生命周期检查
- 根因分析
- 升级条件
- 输出结果

本文件不负责：

- Defect Detection 算法实现
- 图像插值算法
- 软件操作界面
- SDK API
- Detector 硬件维修

上述内容分别由对应文档说明。

---

# 21. Reference

## Fact

- 产品培训资料关于 Defect Calibration、Correction Template、Template Upload、Template Download、Template Overlay 及模板管理流程。

## Engineering

- Defect Calibration 故障应遵循 **Detector → Communication → Offset → Gain → Calibration Image → Defect Detection → Defect Template → Template Management → Calibration Data → Image Verification** 的标准排查路径。
- 当涉及 Template 相关异常时，应优先确认 Active Template 是否已正确加载并参与 Defect Correction，再进一步分析图像结果。