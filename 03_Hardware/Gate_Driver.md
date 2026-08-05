# Gate Driver

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
- ../02_System/SignalDomain.md
- ../02_System/TimingArchitecture.md
- TFT_Array.md
- Readout_ASIC.md
- FPGA.md
- ../07_FailureKnowledge/Image/RowAbnormal.md
- ../08_ImageDiagnosis/HorizontalLine.md

---

# 1. Purpose

Gate Driver 是数字平板探测器 TFT 读出系统的时序控制模块。

负责按照预定时序逐行开启 TFT 阵列，使像素电荷能够依次输出至 Readout ASIC。

Gate Driver 不参与图像处理、信号放大及图像校准，仅负责 TFT 行选通信号的产生与控制。

---

# 2. Scope

适用于所有采用 TFT Array 读出架构的数字平板探测器。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Definition

Gate Driver（栅极驱动器）负责向 TFT Array 的 Gate Line 输出扫描脉冲。

扫描过程中，同一时刻仅有一行 Gate Line 被激活，其对应行的所有 TFT 同时导通。

导通期间，该行所有像素存储的电荷通过 Data Line 输出至 Readout ASIC。

完成当前行读出后，Gate Driver 关闭当前行，并开启下一行。

整个探测器图像由全部行依次完成读出。

---

# 4. Position in Detector Architecture

```text
X-Ray

↓

Scintillator

↓

Photodiode

↓

Charge Storage

↓

TFT Array

↑
│
Gate Driver

↓

Readout ASIC

↓

ADC

↓

FPGA
```

---

# 5. Hardware Relationship

| Module | Relationship |
|----------|--------------|
| FPGA | 输出扫描控制时序 |
| Gate Driver | 产生 Gate Pulse |
| TFT Array | 接收 Gate Pulse |
| Readout ASIC | 接收像素电荷 |
| ADC | 数字化模拟信号 |

---

# 6. Physical Principle

TFT 本质上是电子开关。

每个像素对应一个 TFT。

Gate Driver 通过改变 Gate Line 电压控制 TFT 的导通与截止。

当 Gate Pulse 到达某一行时：

- 当前行全部 TFT 同时导通。
- 当前行所有像素电荷释放。
- Readout ASIC 同时采集该行全部列数据。

Gate Pulse 消失后：

- 当前行 TFT 截止。
- 电荷停止输出。
- 下一行开始扫描。

---

# 7. Working Process

```text
System Ready

↓

FPGA Generate Timing

↓

Gate Driver Receive Timing

↓

Generate Gate Pulse

↓

Select One Gate Line

↓

TFT Turn ON

↓

Pixel Charge Output

↓

Readout ASIC Sampling

↓

Gate OFF

↓

Next Row

↓

Repeat

↓

Frame Complete
```

---

# 8. Timing Relationship

Gate Driver 按照固定扫描顺序工作。

```text
Row 1

↓

Row 2

↓

Row 3

↓

...

↓

Row N
```

同一时刻：

仅允许一条 Gate Line 被驱动。

所有行扫描完成后，一个完整 Frame 完成读出。

Reference：

../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

输入：

Timing Signal

输出：

Gate Pulse

控制对象：

TFT Array

信号关系：

```text
Timing Signal

↓

Gate Pulse

↓

TFT Switch

↓

Charge Output
```

Reference：

../02_System/SignalDomain.md

---

# 10. Interface

## Input

Timing Control Signal

Power Supply

Enable Signal

---

## Output

Gate Pulse

Gate Line Voltage

---

## Controlled Object

TFT Array

---

## Cooperating Module

Readout ASIC

---

# 11. Engineering Characteristics

- 逐行扫描（Row-by-Row Scan）
- 同行像素同步导通
- 单行工作机制
- 与列数据同步采集
- 扫描顺序固定
- 一个 Gate Pulse 对应一行像素

---

# 12. Failure Mode

| Failure | Description |
|----------|-------------|
| Gate Pulse Missing | 无栅极驱动脉冲 |
| Gate Pulse Width Abnormal | 脉冲宽度异常 |
| Gate Voltage Low | 栅压不足 |
| Continuous Gate Output | 连续导通 |
| Wrong Scan Sequence | 扫描顺序错误 |
| Gate Driver IC Failure | 驱动器异常 |
| Gate Line Open | Gate 线路开路 |
| Gate Line Short | Gate 线路短路 |

---

# 13. Failure Symptoms

| Failure | Possible Symptom |
|----------|------------------|
| Gate Pulse Missing | 无法读出图像 |
| Single Gate Line Failure | 单行异常 |
| Multiple Gate Failure | 多行异常 |
| Continuous Gate Output | 图像拖尾、串扰 |
| Wrong Scan Sequence | 图像错位 |
| Gate Voltage Instability | 图像闪烁 |
| Gate Line Short | 大面积行异常 |
| Gate Line Open | 固定行无信号 |

---

# 14. Related Image Artifacts

可能关联的图像异常包括：

- Horizontal Line
- Row Dropout
- Row Noise
- Image Misalignment
- Partial Image Loss
- Frame Corruption

详细内容引用：

- ../08_ImageDiagnosis/

---

# 15. Diagnostic Method

推荐按照以下顺序进行分析：

1. 确认探测器能够正常上电。
2. 确认 FPGA 已输出正常 Timing Signal。
3. 检查 Gate Driver 工作状态。
4. 检查 Gate Line 是否存在开路或短路。
5. 检查 TFT Array 是否正常响应 Gate Pulse。
6. 检查 Readout ASIC 是否接收到对应行数据。
7. 结合图像表现定位异常行范围。

具体检测方法及维修流程引用：

- ../07_FailureKnowledge/
- ../09_DecisionTree/

---

# 16. Related Calibration

Gate Driver 不参与：

- Offset Calibration
- Gain Calibration
- Defect Calibration

Gate Driver 异常可能导致校准失败或校准结果异常，但不执行任何校准算法。

Reference：

../05_Calibration/

---

# 17. Related Documents

System：

- DetectorArchitecture.md
- SignalDomain.md
- TimingArchitecture.md

Hardware：

- TFT_Array.md
- Readout_ASIC.md
- FPGA.md

Failure：

- RowAbnormal.md
- ReadoutFailure.md

Image：

- HorizontalLine.md
- RowNoise.md

Decision Tree：

- GateDriverFailure.md

---

# 18. Knowledge Graph

```text
FPGA
 │
 ▼
Gate Driver
 │
 ▼
Gate Line
 │
 ▼
TFT Array
 │
 ▼
Readout ASIC
 │
 ▼
ADC
 │
 ▼
FPGA
```

---

# 19. Document Boundary

本文件负责：

- Gate Driver 定义
- 功能职责
- 工作原理
- 时序关系
- 信号关系
- 常见失效模式
- 图像影响
- 故障定位入口

本文件不负责：

- FPGA 时序程序实现
- Gate Driver 芯片电路设计
- Gate Driver PCB 布局
- 电压参数设计
- 芯片级维修

---

# 20. Reference

## Fact

- 产品培训资料中关于 TFT 逐行扫描、Gate Driver 控制流程及探测器读出架构。
- 产品用户手册中关于系统组成及图像采集流程。

## Theory

- TFT Array 行扫描原理。
- Gate Driver 与 Readout ASIC 协同读出机制。

## Engineering

后续引用：

- 07_FailureKnowledge/Readout
- 08_ImageDiagnosis
- 09_DecisionTree
- 11_Case