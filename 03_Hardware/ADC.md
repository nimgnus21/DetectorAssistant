# ADC

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
- Readout_ASIC.md
- FPGA.md
- ../05_Calibration/
- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/

---

# 1. Purpose

ADC（Analog-to-Digital Converter）负责将 Readout ASIC 输出的模拟电压信号转换为数字像素数据，是数字平板探测器模拟域（Analog Domain）与数字域（Digital Domain）的边界模块。

ADC 输出的数据作为 FPGA 图像处理及后续校准流程的输入。

---

# 2. Scope

适用于所有采用 TFT 有源矩阵读出结构的数字平板探测器。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Definition

ADC 位于 Readout ASIC 与 FPGA 之间。

在读出阶段，ADC 根据系统时序对模拟电压进行采样和量化，将连续模拟信号转换为离散数字信号，形成数字像素数据。

培训资料将 ADC 定义为模拟读出链路进入数字处理链路的关键节点。

---

# 4. Physical Structure

ADC 位于模拟前端之后。

主要连接对象包括：

- Readout ASIC
- FPGA
- Analog Power
- Digital Power

系统位置：

```text
Readout ASIC

↓

ADC

↓

FPGA
```

---

# 5. Internal Composition

根据培训资料，ADC 主要完成：

- Analog Input
- Sampling
- Quantization
- Digital Output

培训资料未说明芯片内部架构，因此本知识库不定义比较器、采样保持、参考电压等内部实现。

---

# 6. Physical Principle

ADC 在系统时钟控制下，对 Readout ASIC 输出的模拟电压进行采样。

每次采样生成对应数字值。

连续采样后形成完整数字图像数据。

数字数据送入 FPGA。

培训资料说明 ADC 完成模拟信号数字化处理。

---

# 7. Working Process

```text
Readout ASIC Output

↓

Analog Voltage

↓

ADC Sampling

↓

ADC Quantization

↓

Digital Pixel Data

↓

FPGA

↓

Image Buffer
```

---

# 8. Timing Relationship

ADC 工作于 Readout 阶段。

特点：

- 与 Gate Driver 行扫描同步
- 与 Readout ASIC 输出同步
- 与 FPGA 数据接收同步

Reference：

- ../02_System/TimingArchitecture.md

---

# 9. Signal Relationship

输入：

Analog Voltage

输出：

Digital Pixel Data

Signal Domain：

```text
Analog Domain

↓

ADC

↓

Digital Domain
```

Reference：

- ../02_System/SignalDomain.md

---

# 10. Interface

## Input

- Analog Voltage（Readout ASIC）

## Output

- Digital Pixel Data（FPGA）

## Control

- Sampling Clock
- Timing Control

## Connected Hardware

- Readout ASIC
- FPGA

---

# 11. Performance Characteristics

ADC 主要承担：

- 模拟信号采样
- 模拟信号数字化
- 连续数据输出
- 与系统时钟同步

具体采样率、分辨率、位宽等参数应以产品技术规格为准。

---

# 12. Failure Mode

可能出现的失效模式包括：

- ADC 无输出
- Sampling Failure
- Quantization Error
- Output Overflow
- Output Saturation
- Clock Abnormal
- Data Output Error
- Power Failure

---

# 13. Failure Mechanism

ADC 异常可能导致：

- 模拟信号无法转换
- 数字数据错误
- 灰度异常
- 图像噪声增加
- 图像动态范围下降
- 图像失真
- 图像无法生成

培训资料未涉及 ADC 芯片内部失效机理，本知识库不扩展芯片级分析。

---

# 14. Image Manifestation

ADC 异常可能表现为：

- 图像灰度异常
- 图像噪声增加
- 图像亮度异常
- 图像层次减少
- 图像条纹
- 整幅图像异常
- 图像无法显示

具体表现需结合 Readout ASIC 与 FPGA 状态综合分析。

---

# 15. Diagnostic Method

建议诊断顺序：

1. 确认 Readout ASIC 输出正常。
2. 确认 ADC 电源正常。
3. 确认 Sampling Clock 正常。
4. 检查 ADC 输出数字数据。
5. 检查 FPGA 是否正常接收。
6. 对比原始图像及校准结果。
7. 结合故障树进行定位。

---

# 16. Related Calibration

ADC 不执行校准算法。

ADC 输出数据直接影响：

- Offset Calibration
- Gain Calibration
- Defect Calibration

ADC 异常可能导致校准失败或校准结果异常。

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

- Readout_ASIC.md
- FPGA.md

Knowledge：

- ../07_FailureKnowledge/
- ../08_ImageDiagnosis/
- ../09_DecisionTree/

---

# 18. Knowledge Graph

```text
Pixel Charge

↓

Readout ASIC

↓

Analog Voltage

↓

ADC

↓

Digital Pixel Data

↓

FPGA

↓

Image Pipeline
```

---

# 19. Document Boundary

本文件负责：

- ADC 定义
- 系统位置
- 信号转换
- 工作流程
- 时序关系
- 接口关系
- 常见失效模式
- 图像影响
- 故障定位入口

本文件不负责：

- ADC 芯片设计
- 采样算法实现
- FPGA 图像处理
- 图像校准算法
- 芯片维修方法

---

# 20. Reference

## Fact

- 《探测器工作原理1.1》：图像读出流程及 ADC 在数字化链路中的位置。

## Theory

- 培训资料关于模拟信号数字化流程及 ADC 与 Readout ASIC、FPGA 的关系。