# Scintillator

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
- Photodiode.md
- TFT_Array.md
- ../08_ImageDiagnosis/
- ../09_DecisionTree/

---

# 1. Purpose

Scintillator（闪烁体）负责完成 X-Ray 能量向可见光能量的转换。

它是数字平板探测器成像链路中的第一层转换介质，为 Photodiode 提供可检测的光信号，是形成数字 X-Ray 图像的起点。

Scintillator 不负责光电转换、电荷存储及图像读出。

---

# 2. Scope

适用于采用间接转换（Indirect Conversion）成像结构的数字平板探测器。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Definition

Scintillator 是位于 X-Ray 入射方向最前端的转换层。

曝光时吸收 X-Ray 光子，并发射可见光。

发出的光进入 Photodiode，被进一步转换为电荷信号。

培训资料将其定义为 X-Ray 转换流程的第一阶段。

---

# 4. Physical Structure

Scintillator 位于探测器 Active Area 最上层。

系统位置：

```text
X-Ray

↓

Scintillator

↓

Photodiode

↓

TFT Array
```

---

# 5. Internal Composition

Scintillator 为 X-Ray 能量转换层。

培训资料未描述其材料组成、晶体结构及制造工艺，本知识库不定义具体材料及工艺。

---

# 6. Physical Principle

曝光过程中：

X-Ray 入射 Scintillator。

Scintillator 吸收 X-Ray 能量。

吸收后的能量转换为可见光。

可见光向下传播至 Photodiode。

完成第一次能量转换：

```text
X-Ray

↓

Visible Light
```

---

# 7. Working Process

```text
X-Ray Exposure

↓

Scintillator

↓

Light Generation

↓

Optical Output

↓

Photodiode
```

---

# 8. Timing Relationship

Scintillator 仅在曝光阶段工作。

曝光结束后：

不参与图像读出。

不参与校准。

不参与通信。

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

输入：

X-Ray

输出：

Visible Light

Signal Domain：

```text
X-Ray Domain

↓

Scintillator

↓

Optical Domain
```

Reference：

- ../02_System/SignalDomain.md

---

# 10. Interface

## Input

- X-Ray

## Output

- Visible Light

## Connected Hardware

- Photodiode

---

# 11. Performance Characteristics

Scintillator 负责：

- X-Ray 吸收
- 光转换
- 光输出

不负责：

- 电荷产生
- 图像采集
- 图像读出

---

# 12. Failure Mode

可能出现：

- Conversion Efficiency Reduction
- Local Damage
- Mechanical Damage
- Aging

---

# 13. Failure Mechanism

Scintillator 异常可能导致：

- 光输出下降
- 光分布异常
- 后续 Photodiode 接收信号降低

培训资料未涉及材料级失效机理，本知识库不展开说明。

---

# 14. Image Manifestation

可能表现为：

- 图像亮度下降
- 局部亮度异常
- 图像均匀性下降

最终表现需结合 Photodiode 与 Calibration 综合分析。

---

# 15. Diagnostic Method

建议检查：

1. 确认曝光正常。
2. 排除发生器异常。
3. 检查探测器整体响应。
4. 结合 Gain Calibration 判断是否存在整体响应下降。
5. 结合图像异常分析定位。

---

# 16. Related Calibration

Scintillator 不参与校准算法。

其转换效率直接影响：

- Gain Calibration
- Image Uniformity

---

# 17. Related Documents

System：

- DetectorArchitecture.md
- ImagePipeline.md

Hardware：

- Photodiode.md
- TFT_Array.md

Knowledge：

- ../08_ImageDiagnosis/
- ../09_DecisionTree/

---

# 18. Knowledge Graph

```text
X-Ray

↓

Scintillator

↓

Visible Light

↓

Photodiode
```

---

# 19. Document Boundary

本文件负责：

- Scintillator 定义
- X-Ray→Light 转换
- 系统位置
- 工作流程
- 图像影响

本文件不负责：

- 光电转换
- 电荷读出
- 材料工艺
- 制造过程

---

# 20. Reference

## Fact

- 《探测器工作原理1.1》：X-Ray 经闪烁体转换为可见光，作为后续 Photodiode 输入。

## Theory

- 间接转换探测器成像流程。