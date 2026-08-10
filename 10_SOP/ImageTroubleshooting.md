# Image Troubleshooting

> Module: Standard Operating Procedure
>
> SOP ID: SOP-005
>
> Category: Image Troubleshooting
>
> Version: v1.1

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

- SDK Tool / iDetector（适用时）
- DTDI Tool（适用时）
- 图像查看工具
- 网络连接与测试工具（适用时）

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
执行对应排查
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

**异常：** 无法获取日志时，记录无法获取的原因，不将缺失信息视为“正常”。

---

## Step 2 — 识别异常特征

**输入：** 原始异常图像。

**过程：** 判断异常是否固定、是否每幅重复、是否存在于暗场、是否随探测器位置变化、是否表现为数据缺失。

**输出：** 明确的现象分类。

**标准：** 至少完成“重复性 + 位置固定性 + 图像形态”三项判断。

**异常：** 现象无法稳定复现时，保留多张样本并记录发生条件。

---

## Step 3 — 横纹/条带分流

| 观察结果 | 处理方向 |
|---|---|
| 暗场也存在，移动探测器后条纹变化或消失 | 环境干扰 → `InterferenceStripe.md` |
| 多段数据缺失，条带宽度一致 | 网络方向 → `PacketLoss.md` |
| 每幅图出现等宽、亮暗相间规则条纹 | 校正方向 → `CalibrationStripe.md` |
| Mercu0606X1 出现 Defective Bar | 先重新校正 → `DefectiveBar.md` |
| 固定位置线状异常 | `09_DecisionTree/Image/HorizontalLine.md` |

**输出：** 进入唯一的优先排查方向。

**标准：** 不将所有横纹直接归因于硬件。

---

## Step 4 — 执行对应处理

### 4.1 环境干扰

在多个位置重复采集暗场，比较条纹变化。

### 4.2 网络丢包

检查网络状态，改善网络环境后重新采图验证。

### 4.3 失校正

检查校正模板加载与有效状态，按产品适用流程恢复或重新执行相关校正。

### 4.4 Defective Bar

优先重新执行校正；仍存在时保留证据并升级处理。

### 4.5 固定坏线

按照现有 `HorizontalLine.md` 执行 SDK Demo、Offset、Gain 与硬件方向排查。

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
- 校正文件未被无备份覆盖。
- 验证图像已保存。
- 处理结果可追溯。

---

# Related Documents

- `07_FailureKnowledge/ImageFailure/InterferenceStripe.md`
- `07_FailureKnowledge/ImageFailure/PacketLoss.md`
- `07_FailureKnowledge/ImageFailure/CalibrationStripe.md`
- `07_FailureKnowledge/ImageFailure/DefectiveBar.md`
- `07_FailureKnowledge/ImageFailure/DefectPixelLine.md`
- `09_DecisionTree/Image/HorizontalLine.md`
- `00_Project/Index/FailureIndex.md`

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.1 | 2026-08-10 | Added image stripe classification and field verification workflow |
| v1.0 | 2026-08-07 | Initial release |