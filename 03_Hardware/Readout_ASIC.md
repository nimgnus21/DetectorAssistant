# Readout ASIC

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
- ../02_System/ImagePipeline.md
- TFT_Array.md
- Gate_Driver.md
- ADC.md
- FPGA.md
- ../05_Calibration/OffsetCalibration.md
- ../05_Calibration/GainCalibration.md
- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/

---

# 1. Purpose

Readout ASIC（Readout Application Specific Integrated Circuit）是数字平板探测器模拟前端（Analog Front End，AFE）的核心器件。

负责接收 TFT Array 输出的像素电荷，将电荷信号转换为稳定的模拟电压信号，并按照系统时序输出至 ADC，为后续数字化处理提供高质量输入。

Readout ASIC 不负责数字图像处理、图像校准及网络通信。

---

# 2. Scope

适用于所有采用 TFT 有源矩阵（AMA）结构的数字平板探测器。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Definition

Readout ASIC 位于 TFT Array 与 ADC 之间。

在 Gate Driver 控制 TFT 阵列逐行导通后，Readout ASIC 接收对应行各列像素输出的电荷信号，并完成模拟前端处理后输出模拟电压信号。

培训资料将其作为图像读出链路的重要组成部分。

---

# 4. Physical Structure

Readout ASIC 位于探测器电子系统中。

主要连接对象包括：

- TFT Array
- ADC
- FPGA
- Analog Power

在系统架构中处于模拟信号处理阶段。

---

# 5. Internal Composition

根据培训资料，Readout ASIC 属于模拟读出电路，其主要职责包括：

- Pixel Signal Input
- Analog Front End
- Signal Conditioning
- Analog Signal Output

培训资料未进一步展开芯片内部功能模块组成，因此本知识库不定义其内部电路结构。

---

# 6. Physical Principle

读出阶段：

Gate Driver 使当前行 TFT 导通。

对应像素电荷经 Data Line 输入 Readout ASIC。

Readout ASIC 对输入电荷进行模拟处理，输出稳定模拟信号。

模拟信号继续送入 ADC 完成数字化。

整个过程随 Gate Driver 行扫描重复进行，直到全部像素完成读出。

---

# 7. Working Process

```text
Gate Driver Enable

↓

Current Row TFT ON

↓

Pixel Charge Output

↓

Readout ASIC Input

↓

Analog Signal Processing

↓

Analog Voltage Output

↓

ADC Sampling

↓

Next Row

↓

Frame Complete
```

---

# 8. Timing Relationship

Readout ASIC 工作于系统 Readout 阶段。

曝光期间：

Readout ASIC 不参与电荷采集。

读出期间：

随着 Gate Driver 行扫描同步工作。

每完成一行采集，等待下一行输入。

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

输入：

- Pixel Charge

输出：

- Analog Voltage

Signal Flow：

```text
Charge Domain

↓

Readout ASIC

↓

Analog Domain

↓

ADC
```

Reference：

- ../02_System/SignalDomain.md

---

# 10. Interface

## Input

- Pixel Charge（来自 TFT Array）
- Timing Control（系统时序）
- Analog Power

## Output

- Analog Voltage（至 ADC）

## Connected Hardware

- TFT Array
- Gate Driver
- ADC
- FPGA

---

# 11. Performance Characteristics

Readout ASIC 具有以下系统特性：

- 多通道并行读出
- 行扫描同步工作
- 模拟信号处理
- 支持连续 Frame 采集
- 与 ADC 紧密配合完成图像读出

具体通道数量、采样能力及性能指标应以对应 ASIC 技术资料为准。

---

# 12. Failure Mode

可能出现的失效模式包括：

- ASIC 无输出
- ASIC 输出异常
- 单通道异常
- 多通道异常
- 模拟噪声增加
- 模拟输出漂移
- ASIC 供电异常
- ASIC 初始化失败

具体失效模式应结合产品维修资料进一步确认。

---

# 13. Failure Mechanism

Readout ASIC 异常可能导致：

- 电荷无法正常转换
- 模拟信号失真
- 行数据异常
- 多列数据异常
- 图像噪声增加
- 图像灰度异常
- 图像无法正常生成

培训资料说明了其在读出链路中的作用，但未展开芯片级失效机理，因此本知识库不定义芯片内部故障机制。

---

# 14. Image Manifestation

Readout ASIC 异常可能表现为：

- 图像噪声增加
- 行灰度异常
- 多列异常
- 图像亮度异常
- 图像信噪比下降
- 图像缺失
- 图像无法生成

最终图像表现应结合：

- TFT Array
- ADC
- FPGA

进行综合分析。

详细分析见：

- ../08_ImageDiagnosis/

---

# 15. Diagnostic Method

建议诊断顺序：

1. 确认探测器正常上电。
2. 确认 Gate Driver 工作正常。
3. 确认 TFT Array 能正常输出电荷。
4. 检查 Readout ASIC 输入信号。
5. 检查 Readout ASIC 输出模拟信号。
6. 检查 ADC 是否正常采样。
7. 结合图像异常定位具体读出区域。
8. 结合日志、校准结果及故障树综合分析。

---

# 16. Related Calibration

Readout ASIC 不执行校准算法。

其输出质量直接影响：

- Offset Calibration
- Gain Calibration
- Defect Calibration

Readout ASIC 异常可能导致校准失败或校准结果异常。

Reference：

- ../05_Calibration/

---

# 17. Related Documents

System：

- DetectorArchitecture.md
- SignalDomain.md
- TimingArchitecture.md
- ImagePipeline.md

Hardware：

- TFT_Array.md
- Gate_Driver.md
- ADC.md
- FPGA.md

Knowledge：

- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/
- ../09_DecisionTree/

---

# 18. Knowledge Graph

```text
Photodiode
      │
      ▼
Charge Storage
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

- Readout ASIC 定义
- 系统位置
- 信号处理职责
- 工作流程
- 时序关系
- 接口关系
- 常见失效模式
- 图像影响
- 故障定位入口

本文件不负责：

- ASIC 内部电路设计
- 芯片版图
- 放大器电路实现
- ADC 转换原理
- FPGA 图像算法
- 芯片维修方法

---

# 20. Reference

## Fact

- 《探测器工作原理1.1》：探测器读出链路、逐行扫描及 Readout ASIC 在图像采集流程中的位置。

## Theory

- 培训资料关于 TFT 逐行读出、模拟信号处理及 ADC 前级处理流程。