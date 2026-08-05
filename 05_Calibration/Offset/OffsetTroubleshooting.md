# OffsetTroubleshooting

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
- OffsetWorkflow.md
- OffsetParameter.md
- OffsetFailure.md
- ../CalibrationTheory/OffsetTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/
- ../../11_SOP/

---

# 1. Purpose

Offset Troubleshooting 定义 Offset Calibration 故障的标准排查流程。

本文件用于指导现场工程师按照统一流程分析 Offset Calibration Failure，定位故障位置，确认故障原因，并决定后续处理措施。

---

# 2. Scope

适用于：

- Offset Calibration Failed
- Offset Data Error
- Background Offset
- Fixed Pattern Noise
- Offset Correction Failure
- Offset Calibration Timeout

---

# 3. Troubleshooting Principle

Offset Calibration 应按照信号流和执行流程逐级排查。

禁止直接重复执行 Calibration，而应首先确认失败位置。

标准排查顺序如下：

```text
Detector

↓

Communication

↓

Calibration Command

↓

Dark Image Acquisition

↓

Offset Calculation

↓

Calibration Data

↓

Image Verification
```

---

# 4. Troubleshooting Workflow

```text
Offset Calibration Failed

↓

Detector Status

↓

Communication Status

↓

Detector Ready

↓

Dark Image Acquisition

↓

Offset Calculation

↓

Offset Data Generation

↓

Calibration Data Storage

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

若 Detector 未进入 Ready 状态，应先恢复 Detector 工作状态，再重新执行 Offset Calibration。

---

# 6. Step 2 — Verify Communication

检查内容：

- Ethernet Link
- IP Address
- Network Stability
- Packet Loss
- SDK Connection
- iDetector Connection

异常处理：

恢复通信后重新执行 Calibration。

---

# 7. Step 3 — Verify Calibration Command

检查内容：

- Calibration Command 是否发送
- Detector 是否接收命令
- Detector 是否开始 Calibration
- 是否存在 Command Timeout

异常处理：

确认软件状态及通信正常后重新发送 Calibration Command。

---

# 8. Step 4 — Verify Dark Image Acquisition

检查内容：

- 是否完全无 X-Ray
- 是否存在杂散射线
- 是否存在误曝光
- Dark Image 是否采集完成
- Image Size 是否正确
- Image Data 是否完整

异常处理：

排除曝光干扰后重新采集 Dark Image。

---

# 9. Step 5 — Verify Offset Calculation

检查内容：

- Offset Calculation 是否开始
- 是否正常结束
- Offset Table 是否生成
- 是否存在 Calculation Error

异常处理：

若计算失败，应检查 Firmware、软件日志及 Calculation 模块状态。

---

# 10. Step 6 — Verify Calibration Data

检查内容：

- Offset Data 是否生成
- Calibration Data 是否更新
- Calibration Data 是否成功保存
- 新数据是否成功加载

异常处理：

若数据异常，应重新生成 Calibration Data，并确认数据版本一致。

---

# 11. Step 7 — Verify Image Result

完成 Calibration 后采集测试图像。

检查：

- Background Uniformity
- Fixed Pattern Noise
- Offset 是否消除
- 图像整体灰度
- 图像稳定性

若图像恢复正常，则 Calibration 成功。

---

# 12. Troubleshooting Decision Tree

```text
Offset Calibration Failed

├── Detector Offline
│       ↓
│   Restore Detector
│
├── Detector Not Ready
│       ↓
│   Complete Initialization
│
├── Communication Failure
│       ↓
│   Restore Network
│
├── Dark Image Failure
│       ↓
│   Re-acquire Dark Image
│
├── Offset Calculation Failure
│       ↓
│   Check Calculation Module
│
├── Calibration Data Failure
│       ↓
│   Rebuild Calibration Data
│
└── Image Still Abnormal
        ↓
    Continue Image Diagnosis
```

---

# 13. Root Cause Classification

| Category | Possible Cause |
|----------|----------------|
| Detector | Detector Offline、Initialization Failure、Hardware Fault |
| Communication | Ethernet Failure、Network Timeout、SDK Connection Failure |
| Calibration | Calibration Interrupted、Calibration Timeout |
| Image Acquisition | Dark Image Acquisition Failure、Unexpected Exposure |
| Calculation | Offset Calculation Failure、Algorithm Exception |
| Data | Offset Table Error、Calibration Data Corruption |
| Software | iDetector Exception、Firmware Exception |

---

# 14. Escalation Criteria

满足以下任一条件时，应升级处理：

- Offset Calibration 连续失败
- 多次重建 Calibration Data 无效
- Detector 无法进入 Ready
- Hardware Alarm 持续存在
- Background Artifact 无法消除
- 同一故障重复发生
- 怀疑 Detector 硬件损坏

---

# 15. Output

Troubleshooting 完成后，应明确输出以下结论：

- Failure Location
- Root Cause
- Affected Module
- Corrective Action
- Verification Result
- 是否需要重新 Calibration
- 是否需要维修
- 是否需要返厂

---

# 16. Related Documents

Calibration：

- OffsetWorkflow.md
- OffsetParameter.md
- OffsetFailure.md

Theory：

- ../CalibrationTheory/OffsetTheory.md
- ../CalibrationTheory/CalibrationFlow.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

SOP：

- ../../11_SOP/

---

# 17. Knowledge Graph

```text
Offset Calibration Failure

↓

Detector Check

↓

Communication Check

↓

Dark Image Check

↓

Offset Calculation

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

# 18. Document Boundary

本文件负责：

- Offset Calibration 故障排查流程
- 排查顺序
- 检查项目
- 根因分类
- 升级条件
- 输出结果

本文件不负责：

- Offset Calibration 理论
- 软件操作界面
- Calibration 参数配置
- Detector 硬件维修方法
- Image Artifact 分类

上述内容分别由对应文档说明。

---

# 19. Reference

## Fact

- 产品培训资料关于 Offset Calibration 故障处理流程。
- 产品用户手册关于 Calibration Failure 的处理要求。

## Engineering

- Offset Calibration 故障应遵循"Detector → Communication → Command → Image Acquisition → Calculation → Data → Verification"的标准排查路径。
- 故障定位完成后，应形成可追溯的 Root Cause 与 Corrective Action，为 Decision Tree 与 SOP 提供输入。