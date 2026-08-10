# DetectorAssistant

> 平板探测器技术支持知识中枢
>
> Technical Support Knowledge Hub for Flat-Panel Detector Troubleshooting

DetectorAssistant 用于将现场技术支持中的产品知识、故障机理、诊断路径、标准操作、工具、错误码和真实案例组织为可检索、可执行、可复用、可持续反哺的知识系统。

本项目的核心目标不是建立一个静态文档库，而是支持以下闭环：

```text
现场问题
   ↓
问题分类
   ↓
DecisionTree
   ↓
SOP / Workflow
   ↓
Tool / Evidence
   ↓
Root Cause
   ↓
Case
   ↓
Knowledge Feedback
   ↺
```

---

# 1. 项目定位

DetectorAssistant 是面向探测器售前、售后和现场技术支持的技术支持知识库。

主要解决以下问题：

- 现场问题不知道从哪里开始排查。
- 相同问题依赖个人经验重复处理。
- 故障现象、根因、工具和案例之间缺少关联。
- 技术支持过程无法形成统一证据标准。
- 真实案例无法稳定反哺故障知识。
- 新人员难以快速建立完整诊断路径。

项目将技术支持工作拆分为：

```text
System / Hardware / Software
        ↓
Calibration / Workflow
        ↓
Failure Knowledge / Image Diagnosis
        ↓
Decision Tree
        ↓
SOP
        ↓
Tool / Error Code / Template
        ↓
Case
        ↓
Knowledge Feedback
```

---

# 2. 快速开始

## 2.1 现场出现问题

优先进入：

- [09_DecisionTree](09_DecisionTree/README.md) — 根据症状选择诊断路径。
- [10_SOP](10_SOP/README.md) — 按标准步骤执行现场操作。
- [17_Tools](17_Tools/README.md) — 调用对应诊断工具。
- [11_Case](11_Case/README.md) — 查询已闭环的历史案例。

建议主路径：

```text
Symptom
   ↓
09_DecisionTree
   ↓
10_SOP / 06_Workflow
   ↓
17_Tools
   ↓
Evidence
   ↓
Root Cause
   ↓
11_Case
```

## 2.2 图像异常

优先进入：

- [08_ImageDiagnosis](08_ImageDiagnosis/README.md)
- [09_DecisionTree/Image](09_DecisionTree/Image/)
- [10_SOP/ImageTroubleshooting.md](10_SOP/ImageTroubleshooting.md)
- [11_Case/Image](11_Case/Image/)

典型问题包括：

- Horizontal Line
- Vertical Line
- Ghost
- Image Shift
- Lag
- Noise
- Mosaic
- Fixed Black Point
- Fixed White Point

## 2.3 网络或连接异常

优先进入：

- [09_DecisionTree/Connection](09_DecisionTree/Connection/)
- [10_SOP/NetworkConfiguration.md](10_SOP/NetworkConfiguration.md)
- [06_Workflow/ConnectionWorkflow.md](06_Workflow/ConnectionWorkflow.md)
- [17_Tools/Ping](17_Tools/Ping/README.md)
- [17_Tools/Wireshark](17_Tools/Wireshark/README.md)

## 2.4 校准失败

优先进入：

- [05_Calibration](05_Calibration/README.md)
- [09_DecisionTree/Calibration](09_DecisionTree/Calibration/)
- [10_SOP/Calibration.md](10_SOP/Calibration.md)
- [17_Tools/SDKTool/CalibrationTools.md](17_Tools/SDKTool/CalibrationTools.md)

## 2.5 固件或版本问题

优先进入：

- [09_DecisionTree/Firmware](09_DecisionTree/Firmware/)
- [10_SOP/FirmwareUpgrade.md](10_SOP/FirmwareUpgrade.md)
- [12_ErrorCode/Firmware](12_ErrorCode/Firmware/)
- [17_Tools/SDKTool/FirmwareUpgrade.md](17_Tools/SDKTool/FirmwareUpgrade.md)
- [11_Case/Firmware](11_Case/Firmware/)

## 2.6 SDK 或软件异常

优先进入：

- [04_Software](04_Software/README.md)
- [09_DecisionTree/Software](09_DecisionTree/Software/)
- [12_ErrorCode/SDK](12_ErrorCode/SDK/)
- [17_Tools/Log](17_Tools/Log/README.md)

---

# 3. 一级目录导航

| Directory | Role | When to Use |
|---|---|---|
| [00_Project](00_Project/) | 项目架构与设计 | 了解系统结构、流程图和项目规则 |
| [02_System](02_System/) | 系统知识 | 理解探测器系统组成和工作原理 |
| [03_Hardware](03_Hardware/) | 硬件知识 | 排查电源、接口、网络及硬件模块 |
| [04_Software](04_Software/) | 软件与 SDK | 排查 SDK、软件配置、日志和升级问题 |
| [05_Calibration](05_Calibration/) | 校准知识 | 理解和执行 Offset、Gain、Defect 等校准 |
| [06_Workflow](06_Workflow/) | 工作流程 | 按系统流程理解启动、连接、采集和配置 |
| [07_FailureKnowledge](07_FailureKnowledge/) | 故障知识 | 理解故障分类、分析方法和根因逻辑 |
| [08_ImageDiagnosis](08_ImageDiagnosis/) | 图像诊断 | 根据图像表现进行专项分析 |
| [09_DecisionTree](09_DecisionTree/) | 故障决策 | 根据现场症状选择排查分支 |
| [10_SOP](10_SOP/) | 标准操作 | 执行可重复的现场处理步骤 |
| [11_Case](11_Case/) | 真实案例 | 查询和沉淀已闭环的现场问题 |
| [12_ErrorCode](12_ErrorCode/) | 错误码 | 根据错误码进入对应诊断链路 |
| [13_Template](13_Template/) | 模板 | 使用记录、回复和工作模板 |
| [14_Glossary](14_Glossary/) | 术语 | 统一产品、故障和技术术语 |
| [15_Reference](15_Reference/) | 参考资料 | 保存外部或基础参考信息 |
| [16_KnowledgeAssets](16_KnowledgeAssets/) | 知识资产 | 保存可复用的知识资产和辅助材料 |
| [17_Tools](17_Tools/) | 诊断工具 | 执行网络、日志、图像、SDK 等诊断操作 |

一级目录作为项目架构层维护。新增内容应优先进入现有分类，不应为了单个问题随意新增一级目录。

---

# 4. 技术支持闭环

## Step 1 — 记录问题

先固定基础信息：

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Host Environment
- Symptom
- Reproduction Condition

## Step 2 — 进行问题分类

优先判断问题属于：

```text
Image
Communication
Calibration
Firmware
Software / SDK
Hardware
```

随后进入对应 [09_DecisionTree](09_DecisionTree/README.md)。

## Step 3 — 执行标准路径

DecisionTree 用于回答：

> 下一步应该检查什么？

SOP 用于回答：

> 具体应该怎么做？

Workflow 用于回答：

> 系统正常流程应该是什么？

## Step 4 — 使用工具获取证据

工具不是独立存在的功能说明，而是诊断链路中的证据获取节点。

典型工具包括：

- Ping
- Wireshark
- Log Viewer
- ImageJ
- Offset Viewer
- SDK Tool
- Firmware Upgrade
- Calibration Tools

工具入口：[17_Tools](17_Tools/README.md)

## Step 5 — 形成根因判断

根因判断必须区分：

- Confirmed Root Cause
- Suspected Root Cause
- Ruled Out Cause
- Evidence Required

不能仅根据单一现象直接判定硬件故障。

## Step 6 — 检查历史 Case

进入 [11_Case](11_Case/README.md)，确认是否已有相同或相近问题。

如果已有 Case：

```text
Case
→ 验证适用条件
→ 复用诊断路径
→ 比对当前证据
```

如果没有 Case：

```text
New Issue
→ Complete Diagnosis
→ Evidence
→ Root Cause
→ Case Admission
```

## Step 7 — Knowledge Feedback

满足以下条件时，应更新相关知识节点：

```text
New Symptom
→ 09_DecisionTree

New Standard Operation
→ 10_SOP

New Root Cause
→ 07_FailureKnowledge

New Tool Usage
→ 17_Tools

New Error Mapping
→ 12_ErrorCode

Verified Field Incident
→ 11_Case
```

---

# 5. Case 准入原则

真实案例不是简单的问题记录。

Case 至少应能够回答：

1. What happened?
2. Under what condition?
3. How was it reproduced?
4. What evidence was collected?
5. Which diagnostic path was used?
6. What root cause was confirmed or suspected?
7. What was done?
8. How was the result verified?
9. Which knowledge node should be updated?

Case 应与以下节点建立反向关联：

```text
Case
 ↔ DecisionTree
 ↔ SOP
 ↔ Workflow
 ↔ Tool
 ↔ ErrorCode
 ↔ FailureKnowledge
```

---

# 6. Evidence 优先原则

技术支持结论应尽量基于可复查证据。

根据问题类型，可能需要：

### Image

- RAW Image
- Processed Image
- Dark Image
- Calibration Result
- Fixed Coordinate Comparison

### Communication

- Ping Result
- Network Configuration
- Packet Capture
- SDK Log
- Detector Status

### Calibration

- Calibration Log
- Offset / Gain / Defect Result
- Firmware Version
- SDK Version
- Before / After Image

### Firmware

- Firmware Version
- Upgrade Log
- Upgrade Result
- Parameter / License Status

### Software / SDK

- API Error
- SDK Log
- DLL Version
- Reproduction Condition

---

# 7. 推荐使用方式

## FAE / 现场支持

```text
现场现象
→ DecisionTree
→ SOP
→ Tool
→ Evidence
→ Case
```

## 技术支持工程师

```text
Case / ErrorCode
→ FailureKnowledge
→ DecisionTree
→ Tool
→ Root Cause
→ Knowledge Feedback
```

## 新人员

建议学习顺序：

```text
02_System
→ 03_Hardware
→ 04_Software
→ 05_Calibration
→ 06_Workflow
→ 07_FailureKnowledge
→ 08_ImageDiagnosis
→ 09_DecisionTree
→ 10_SOP
→ 17_Tools
→ 11_Case
```

## 研发协同

当现场无法完成根因确认时，至少输出：

```text
Symptom
Environment
Reproduction Condition
Evidence
Actions Already Performed
Result
Suspected Module
Open Questions
```

再进入研发分析或问题升级。

---

# 8. 当前重点知识域

当前技术支持链路重点覆盖：

```text
Image Abnormality
Network / Communication
Calibration Failure
Firmware
SDK / Software
```

典型高频问题优先级：

1. Image Abnormality
2. Network Connection
3. Calibration Failure
4. Unable to Exposure / Acquisition
5. Firmware / SDK Compatibility

---

# 9. 文档维护规则

## 一级目录冻结

项目一级目录是架构层，不因单个文档问题随意调整。

原则：

```text
Fix content before changing structure.
Reuse existing category before creating new category.
Freeze top-level directories unless structurally necessary.
```

## 新增文档

新增文档前检查：

- 是否已有相同问题？
- 是否可以补充现有文档？
- 应属于哪个一级目录？
- 是否需要建立 Related Documents？
- 是否会形成孤立知识节点？

## 新增 Case

优先检查：

```text
Existing Case
→ DecisionTree
→ SOP
→ FailureKnowledge
→ Tool
```

只有无法被现有知识完整覆盖，或具有新的证据、根因或诊断价值时，再新增独立 Case。

## 链接规则

文档间引用应优先使用相对 Markdown 链接：

```markdown
[DecisionTree](../09_DecisionTree/...)
```

避免只保留无法点击的裸路径；删除不存在且无等价节点的历史路径，不虚构文件。

---

# 10. 维护状态

本仓库当前正在进行项目级完整性治理，重点包括：

- 根 README 建设
- 一级目录 README 一致性审计
- Markdown Link Audit
- DecisionTree / SOP / Tool 反向链接
- Case 准入与知识反哺
- ErrorCode → DecisionTree → Tool → Evidence 闭环

项目状态应以当前仓库文件和链接审计结果为准，不以单个历史进度描述替代实际验证。

---

# 11. 项目核心原则

```text
Do not guess when evidence can be collected.
Do not classify a symptom as a root cause.
Do not create a Case without diagnostic value.
Do not leave knowledge nodes isolated.
Do not change the project structure without necessity.
```

最终目标：

> 让一次现场问题不仅被解决，还能留下可验证、可复用、可导航的技术支持知识。