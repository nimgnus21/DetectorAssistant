````markdown
# GainTroubleshooting

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
- GainWorkflow.md
- GainParameter.md
- GainFailure.md
- ../CalibrationTheory/GainTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/
- ../../11_SOP/

---

# 1. Purpose

Gain Troubleshooting 定义 Gain Calibration 故障的标准排查流程。

本文件用于指导现场工程师按照统一流程分析 Gain Calibration Failure，定位故障位置，确认故障原因，并制定相应处理措施。

---

# 2. Scope

适用于以下情况：

- Gain Calibration Failed
- Gain Calibration Timeout
- Gain Data Error
- Gain Correction Failure
- Image Nonuniformity
- Bright Area
- Dark Area
- Calibration Success but Image Abnormal

---

# 3. Troubleshooting Principle

Gain Calibration 应按照 Calibration Workflow 和 Signal Flow 逐级排查。

排查过程中应遵循：

- 先确认 Detector 状态
- 再确认 Offset Calibration
- 再确认曝光条件
- 最后分析 Gain Data 与图像结果

禁止直接重复执行 Calibration，而应首先确认故障位置。

---

# 4. Standard Workflow

```text
Gain Calibration Failed

↓

Detector Status

↓

Communication Status

↓

Offset Calibration Status

↓

Exposure Condition

↓

Flat Field Image

↓

Gain Calculation

↓

Gain Data

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
- 是否完成 Initialization
- 是否存在 Hardware Alarm
- 是否存在 Firmware Alarm

异常处理：

恢复 Detector 正常工作状态后，再继续排查。

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

恢复通信后重新执行 Gain Calibration。

---

# 7. Step 3 — Verify Offset Calibration

检查内容：

- Offset Calibration 是否完成
- Offset Data 是否存在
- Calibration Data 是否正确加载
- Offset Calibration 是否与当前 Detector 匹配

异常处理：

若 Offset Calibration 未完成或数据异常，应重新执行 Offset Calibration。

---

# 8. Step 4 — Verify Exposure Condition

检查内容：

- X-Ray Generator 是否正常
- 曝光参数是否符合要求
- 曝光剂量是否稳定
- Beam 是否覆盖整个 Detector
- Beam 是否均匀

异常处理：

修正曝光条件后重新执行 Gain Calibration。

---

# 9. Step 5 — Verify Flat Field Image

检查内容：

- Flat Field Image 是否采集成功
- 图像是否完整
- 是否存在饱和
- 是否存在截断
- 是否存在遮挡
- 图像是否具有均匀曝光特征

异常处理：

确认均匀曝光条件后重新采集 Flat Field Image。

---

# 10. Step 6 — Verify Gain Calculation

检查内容：

- Gain Calculation 是否开始
- 是否正常完成
- Gain Table 是否生成
- 是否存在 Algorithm Error

异常处理：

检查 Firmware、软件日志及 Gain Calculation 模块状态。

---

# 11. Step 7 — Verify Calibration Data

检查内容：

- Gain Data 是否生成
- Calibration Data 是否更新
- 新 Gain Data 是否成功写入
- Calibration Data 是否正确加载

异常处理：

重新生成 Gain Data，并确认 Calibration Data 更新成功。

---

# 12. Step 8 — Verify Image Result

完成 Gain Calibration 后采集测试图像。

检查内容：

- Image Uniformity
- Bright Area
- Dark Area
- Response Consistency
- Fixed Pattern Noise
- Contrast
- Image Stability

若图像恢复正常，则 Gain Calibration 成功。

---

# 13. Troubleshooting Decision Tree

```text
Gain Calibration Failed

├── Detector Offline
│       ↓
│   Restore Detector
│
├── Communication Failure
│       ↓
│   Restore Communication
│
├── Offset Calibration Failure
│       ↓
│   Rebuild Offset Data
│
├── Exposure Failure
│       ↓
│   Correct Exposure Condition
│
├── Flat Field Image Failure
│       ↓
│   Re-acquire Image
│
├── Gain Calculation Failure
│       ↓
│   Check Calculation Module
│
├── Gain Data Failure
│       ↓
│   Rebuild Gain Data
│
└── Image Still Abnormal
        ↓
    Continue Image Diagnosis
```

---

# 14. Root Cause Classification

| Category | Possible Cause |
|----------|----------------|
| Detector | Detector Offline、Initialization Failure、Hardware Failure |
| Communication | Ethernet Failure、Network Timeout、SDK Communication Failure |
| Offset | Offset Calibration Failure、Offset Data Invalid |
| Exposure | Generator Failure、Exposure Parameter Error、Beam Nonuniformity |
| Image Acquisition | Flat Field Image Acquisition Failure、Image Saturation、Image Truncation |
| Calculation | Gain Calculation Failure、Algorithm Exception |
| Data | Gain Data Error、Calibration Data Corruption |
| Software | Firmware Exception、iDetector Exception |

---

# 15. Escalation Criteria

满足以下任一条件时，应升级处理：

- Gain Calibration 连续失败
- 多次重新 Calibration 无效
- Gain Data 无法生成
- Calibration Data 无法更新
- 图像均匀性无法恢复
- Bright/Dark Area 持续存在
- 怀疑 Detector Hardware Failure

---

# 16. Output

Troubleshooting 完成后，应形成以下输出：

- Failure Location
- Root Cause
- Affected Module
- Corrective Action
- Verification Result
- 是否重新执行 Calibration
- 是否需要维修
- 是否需要返厂

---

# 17. Related Documents

Calibration：

- GainWorkflow.md
- GainParameter.md
- GainFailure.md

Theory：

- ../CalibrationTheory/GainTheory.md
- ../CalibrationTheory/CalibrationFlow.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

SOP：

- ../../11_SOP/

---

# 18. Knowledge Graph

```text
Gain Calibration Failure

↓

Detector Check

↓

Communication Check

↓

Offset Check

↓

Exposure Check

↓

Flat Field Image

↓

Gain Calculation

↓

Gain Data

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

# 19. Document Boundary

本文件负责：

- Gain Calibration 故障排查流程
- 排查顺序
- 检查项目
- 根因分类
- 升级条件
- 输出结果

本文件不负责：

- Gain Calibration 理论
- 软件操作界面
- 参数配置
- Firmware 实现
- Detector 硬件维修

上述内容分别由对应文档说明。

---

# 20. Reference

## Fact

- 产品培训资料关于 Gain Calibration 流程及故障处理要求。
- 产品用户手册关于 Calibration Failure 的处理流程。

## Engineering

- Gain Calibration 故障应遵循 "Detector → Communication → Offset → Exposure → Flat Field Image → Gain Calculation → Gain Data → Calibration Data → Image Verification" 的标准排查路径。
- Troubleshooting 应形成完整的 Root Cause、Corrective Action 及 Verification Result，为 Decision Tree 与 SOP 提供依据。
````
