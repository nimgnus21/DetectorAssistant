# Photodiode

Version: V2.0

Module: Hardware

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- ../02_System/DetectorArchitecture.md
- ../02_System/ImagePipeline.md
- ../02_System/SignalDomain.md
- Scintillator.md
- TFT_Array.md
- ../08_ImageDiagnosis/
- ../09_DecisionTree/

---

# 1. Purpose

Photodiode（光电二极管）负责完成可见光向电荷信号（Charge）的转换。

Photodiode 接收 Scintillator 发出的可见光，通过光电效应产生与入射光强对应的电荷，并将电荷存储于 Pixel Unit 中，为后续 TFT Array 读出提供信号来源。

Photodiode 不负责 X-Ray 转换、像素读出及图像处理。

---

# 2. Scope

适用于采用间接转换（Indirect Conversion）结构的数字平板探测器。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Definition

Photodiode 是位于 Scintillator 下方、TFT Array 上方的光电转换器件。

曝光期间接收 Scintillator 输出的可见光，并通过光电转换产生电荷。

产生的电荷保存在对应像素节点，等待 Gate Driver 控制 TFT 导通后完成读出。

培训资料将 Photodiode 定义为间接转换探测器中完成 Light → Charge 转换的核心器件。

---

# 4. Physical Structure

Photodiode 位于探测器 Active Area 内部。

系统位置：

```text
X-Ray

↓

Scintillator

↓

Photodiode

↓

Pixel Charge

↓

TFT Array
```

Photodiode 与 TFT Pixel 一一对应，共同构成 Active Matrix Array（AMA）。

---

# 5. Internal Composition

Photodiode 属于像素单元组成部分。

每个 Pixel Unit 包括：

- Photodiode
- Charge Storage Node
- TFT Switch
- Pixel Electrode

培训资料未进一步描述 Photodiode 的 PN 结构、半导体层及制造工艺，本知识库不定义器件内部结构。

---

# 6. Physical Principle

曝光期间：

Scintillator 将 X-Ray 转换为可见光。

Photodiode 吸收可见光。

光子激发电子-空穴对。

形成光生电荷。

电荷积累于 Pixel Charge Storage Node。

曝光结束后，电荷保持在像素节点，等待 TFT 导通完成读出。

整个过程完成第二次能量转换：

```text
Visible Light

↓

Electrical Charge
```

培训资料描述了光电转换及电荷存储过程。

---

# 7. Working Process

```text
Visible Light

↓

Photodiode

↓

Photoelectric Conversion

↓

Charge Generation

↓

Charge Storage

↓

TFT Array

↓

Readout ASIC
```

---

# 8. Timing Relationship

Photodiode 工作于 Exposure 阶段。

工作过程：

- 曝光开始
- 持续产生电荷
- 电荷持续积分
- 曝光结束
- 保持电荷
- 等待读出

Photodiode 不参与：

- Readout Control
- Communication
- Calibration Calculation

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

输入：

- Visible Light

输出：

- Pixel Charge

Signal Domain：

```text
Optical Domain

↓

Photodiode

↓

Charge Domain
```

Reference：

- ../02_System/SignalDomain.md

---

# 10. Interface

## Input

- Visible Light（来自 Scintillator）

## Output

- Pixel Charge

## Connected Hardware

- Scintillator
- TFT Array

---

# 11. Performance Characteristics

Photodiode 负责：

- 光电转换
- 电荷产生
- 电荷积分
- 电荷保持

Photodiode 不负责：

- X-Ray 吸收
- 电荷放大
- 行扫描
- 模拟信号处理
- 数字图像处理

具体响应特性应以产品技术规格及培训资料为准。

---

# 12. Failure Mode

可能出现的失效模式包括：

- Photoelectric Conversion Reduction
- Charge Generation Failure
- Charge Leakage
- Pixel Response Reduction
- Local Photodiode Damage
- Pixel Failure

产品资料未进一步区分 Photodiode 器件级故障类型，本知识库不扩展定义。

---

# 13. Failure Mechanism

Photodiode 异常可能导致：

- 光电转换效率下降
- 光生电荷减少
- 电荷积分不足
- 电荷泄漏
- 像素响应降低
- 后续读出信号减弱

培训资料说明了 Photodiode 在信号链中的作用，但未展开器件级失效机理，因此本知识库不定义半导体物理层面的故障机制。

---

# 14. Image Manifestation

Photodiode 异常可能表现为：

- 图像亮度下降
- 局部灰度降低
- 图像均匀性下降
- 固定像素异常
- 局部响应异常
- 图像信噪比下降

最终图像表现需结合 TFT Array、Readout ASIC 及 Calibration 综合分析。

详细分析见：

- ../08_ImageDiagnosis/

---

# 15. Diagnostic Method

建议诊断顺序：

1. 确认 X-Ray 曝光正常。
2. 确认 Scintillator 工作正常。
3. 检查整体图像响应。
4. 分析异常区域是否固定。
5. 结合 Gain Calibration 结果判断响应一致性。
6. 排除 TFT Array 及 Readout ASIC 异常。
7. 根据 DecisionTree 综合定位故障。

---

# 16. Related Calibration

Photodiode 不执行校准算法。

Photodiode 工作状态直接影响：

- Offset Calibration
- Gain Calibration
- Defect Calibration

Photodiode 响应异常可能导致校准结果异常或校准失败。

Reference：

- ../05_Calibration/

---

# 17. Related Documents

System：

- DetectorArchitecture.md
- ImagePipeline.md
- SignalDomain.md

Hardware：

- Scintillator.md
- TFT_Array.md
- Readout_ASIC.md

Knowledge：

- ../08_ImageDiagnosis/
- ../09_DecisionTree/

---

# 18. Knowledge Graph

```text
X-Ray
    │
    ▼
Scintillator
    │
    ▼
Visible Light
    │
    ▼
Photodiode
    │
    ▼
Pixel Charge
    │
    ▼
TFT Array
    │
    ▼
Readout ASIC
```

---

# 19. Document Boundary

本文件负责：

- Photodiode 定义
- Light → Charge 转换
- 电荷产生
- 电荷积分
- 系统位置
- 工作流程
- 常见失效模式
- 图像影响
- 故障定位入口

本文件不负责：

- X-Ray 转换
- TFT 开关控制
- 模拟信号处理
- 数字图像处理
- 半导体制造工艺
- 器件级设计

---

# 20. Reference

## Fact

- 《探测器工作原理1.1》：间接转换探测器成像原理、Photodiode 光电转换、电荷存储及 TFT 有源矩阵读出流程。

## Theory

- 培训资料关于 X-Ray → Visible Light → Charge 的信号转换过程及 Photodiode 在成像链中的作用。