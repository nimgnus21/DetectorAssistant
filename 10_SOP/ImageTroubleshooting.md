# Image Troubleshooting

> Module: Standard Operating Procedure
>
> SOP ID: SOP-005
>
> Category: Image Troubleshooting
>
> Version: v1.2

---

# Scope

本 SOP 适用于探测器采图过程中的图像异常现场排查，包括：

- 横纹、条带和线状异常
- 丢失数据导致的条带
- 校正相关图像异常
- 坏点、坏线和局部异常
- 黑点伪影
- TFT 损伤相关异常
- 采图失败

---

# Objective

按照统一的“输入 → 过程 → 输出 → 标准 → 异常”流程完成图像故障分流，先区分现象，再执行对应排查，减少不必要的重复校正和硬件更换。

---

# Responsibility

| Role | Responsibility |
|---|---|
| FAE | 现场信息采集、复现、执行标准排查和验证 |
| Technical Support Engineer | 远程分析、日志与图像支持 |
| R&D Engineer | 标准流程无法定位时进行深入分析 |

---

# Preconditions

开始前确认：

- 探测器型号与 SN 已记录。
- Firmware Version 与 SDK Version 已记录。
- 原始异常图像已保存。
- 未覆盖原有校正文件。
- 如需重启或修改配置，先保存日志。

---

# Required Tools

- [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)（SDK 状态、连接、采图与日志初步排查）
- [DTDI Tool](../17_Tools/SDKTool/DTDITool.md)（适用产品的图像/模板处理）
- [ImageJ](../17_Tools/ImageJ/)（图像形态、位置和重复性比较）
- [Offset Viewer](../17_Tools/OffsetViewer/)（Offset 相关异常分析，如适用）
- [Wireshark](../17_Tools/Wireshark/)（怀疑网络传输异常或数据丢失时）
- [Log Viewer](../17_Tools/LogViewer/)（日志查看与异常时间点关联）

工具选择原则：只在对应现象分支中使用，工具输出必须与原始图像、日志或验证图像一起保存。

---

# Standard Workflow

```text
异常图像
   ↓
保存原始证据
   ↓
识别异常特征
   ↓
按现象分流
   ├── 横纹/条带
   ├── 固定坏点/坏线
   ├── 黑点伪影
   ├── TFT/物理损伤
   └── 无法正常采图
   ↓
执行对应排查 + 使用对应工具
   ↓
验证图像
   ↓
记录结果
   ↓
未解决 → DecisionTree / Escalation
```

---

# Procedure

## Step 1 — 保存原始证据

**输入：** 客户异常图像。

**过程：** 保存原始图像、异常截图、Detector.log（如适用），并记录 Detector Model、SN、Firmware、SDK Version。

**输出：** 完整初始证据集。

**标准：** 后续操作前原始证据可追溯。

**异常：** 无法获取日志时，记录无法获取的原因，不将缺失信息视为“正常”。必要时使用 [Log Viewer](../17_Tools/LogViewer/) 定位可获取日志中的异常时间点。

---

## Step 2 — 识别异常特征

**输入：** 原始异常图像。

**过程：** 判断异常是否固定、是否每幅重复、是否存在于暗场、是否随探测器位置变化、是否表现为数据缺失。可使用 [ImageJ](../17_Tools/ImageJ/) 对多张图像进行位置与形态比较。

**输出：** 明确的现象分类。

**标准：** 至少完成“重复性 + 位置固定性 + 图像形态”三项判断。

**异常：** 现象无法稳定复现时，保留多张样本并记录发生条件。

---

## Step 3 — 横纹/条带分流

| 观察结果 | 处理方向 | 推荐工具 |
|---|---|---|
| 暗场也存在，移动探测器后条纹变化或消失 | 环境干扰 → `InterferenceStripe.md` | ImageJ |
| 多段数据缺失，条带宽度一致 | 网络方向 → `PacketLoss.md` | Wireshark、Log Viewer |
| 每幅图出现等宽、亮暗相间规则条纹 | 校正方向 → `CalibrationStripe.md` | Offset Viewer、SDK Tool |
| Mercu0606X1 出现 Defective Bar | 先重新校正 → `DefectiveBar.md` | SDK Tool / DTDI Tool |
| 固定位置线状异常 | `09_DecisionTree/Image/HorizontalLine.md` | SDK Tool、Offset Viewer |

**输出：** 进入唯一的优先排查方向。

**标准：** 不将所有横纹直接归因于硬件。

---

## Step 4 — 执行对应处理

### 4.1 环境干扰

在多个位置重复采集暗场，使用 [ImageJ](../17_Tools/ImageJ/) 比较条纹位置与形态变化。

### 4.2 网络丢包

检查网络状态；必要时使用 [Wireshark](../17_Tools/Wireshark/) 或 [Log Viewer](../17_Tools/LogViewer/) 保留传输异常证据，改善网络环境后重新采图验证。

### 4.3 失校正

检查校正模板加载与有效状态，使用 [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md) 或适用的 [DTDI Tool](../17_Tools/SDKTool/DTDITool.md) 按产品流程恢复或重新执行相关校正。

### 4.4 Defective Bar

优先重新执行校正；仍存在时保留证据并升级处理。

### 4.5 固定坏线

按照现有 `HorizontalLine.md` 执行 SDK Demo、Offset、Gain 与硬件方向排查；Offset 相关现象可使用 [Offset Viewer](../17_Tools/OffsetViewer/) 辅助分析。

---

## Step 5 — 验证

**输入：** 处理后的探测器状态。

**过程：** 重新采集验证图像，并与原始异常图比较。

**输出：** 已恢复 / 未恢复 / 现象变化。

**标准：** 验证结果必须保存，不仅记录文字结论。

**异常：** 未恢复时进入对应 DecisionTree，并保留已执行步骤。

---

## Step 6 — 记录与升级

记录：

- 现象
- 发生条件
- 已执行操作
- 实际使用工具与输出
- 验证结果
- 原始图像与验证图像
- Firmware / SDK Version
- 日志（如可获取）

只有在标准排查无法解决，或怀疑硬件损伤时升级至进一步分析。

---

# Acceptance Checklist

- 原始证据已保存。
- 现象已分类。
- 横纹已完成特征分流（如适用）。
- 已使用工具与输出已记录。
- 校正文件未被无备份覆盖。
- 验证图像已保存。
- 处理结果可追溯。

---

# Related Documents

- [Interference Stripe](../07_FailureKnowledge/ImageFailure/InterferenceStripe.md)
- [Packet Loss](../07_FailureKnowledge/ImageFailure/PacketLoss.md)
- [Calibration Stripe](../07_FailureKnowledge/ImageFailure/CalibrationStripe.md)
- [Defective Bar](../07_FailureKnowledge/ImageFailure/DefectiveBar.md)
- [Defect Pixel / Line](../07_FailureKnowledge/ImageFailure/DefectPixelLine.md)
- [Horizontal Line DecisionTree](../09_DecisionTree/Image/HorizontalLine.md)
- [Failure Index](../00_Project/Index/FailureIndex.md)
- [ImageJ](../17_Tools/ImageJ/)
- [Offset Viewer](../17_Tools/OffsetViewer/)
- [Wireshark](../17_Tools/Wireshark/)
- [Log Viewer](../17_Tools/LogViewer/)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.2 | 2026-08-10 | Added direct tool links and tool-specific evidence flow |
| v1.1 | 2026-08-10 | Added image stripe classification and field verification workflow |
| v1.0 | 2026-08-07 | Initial release |