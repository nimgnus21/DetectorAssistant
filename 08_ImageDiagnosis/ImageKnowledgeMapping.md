# Image Phenomenon Cross-Layer Knowledge Mapping

> Purpose: connect each supported phenomenon to ImageDiagnosis, DecisionTree, FailureKnowledge, Case and image evidence. This file is a mapping layer; it does not invent missing technical conclusions or dead links.

## Diagnostic rule

A single image establishes an observed phenomenon, not a confirmed root cause. `Read Channel`, `Gate Channel`, `Hardware`, `Calibration`, `Network`, or other mechanisms remain candidates until the required evidence is available.

## Mapping

| Phenomenon | DecisionTree | FailureKnowledge | Existing Case | Required evidence | Status |
|---|---|---|---|---|---|
| 坏点 / Dead Pixel | `09_DecisionTree/Image/BlackDot.md`, `WhiteDot.md` | `07_FailureKnowledge/ImageFailure/` | `11_Case/Image/BlackDots.md`, `WhiteDots.md` | RAW, fixed coordinate, repeated frames, Defect Template, before/after correction | Mapped |
| 图像不规则伪影 | `09_DecisionTree/Image/README` equivalent not present; route through Image classification | `07_FailureKnowledge/ImageFailure/` | — | RAW, processed image, repeatability, exposure condition | Candidate only |
| Read 通道伪影 | `09_DecisionTree/Image/HorizontalLine.md`, `VerticalLine.md` | `07_FailureKnowledge/HardwareFailure/` | — | fixed row/column, RAW, repeatability, channel/readout correlation | Candidate only |
| Gate 通道伪影 | `09_DecisionTree/Image/HorizontalLine.md` | `07_FailureKnowledge/HardwareFailure/` | — | fixed row, RAW, repeatability, timing/gate evidence | Candidate only |
| 图像奇偶差异明显 | Image classification; no dedicated DecisionTree file currently | `07_FailureKnowledge/ImageFailure/` | — | odd/even row or column comparison, RAW, exposure condition, correction state | Candidate only |
| 图像颗粒噪声 | `09_DecisionTree/Image/Noise.md` | `07_FailureKnowledge/ImageFailure/` | `11_Case/Image/Noise.md` | RAW/Dark, repeated frames, exposure dependence, noise statistics | Mapped |
| 图像横条纹噪声 | `09_DecisionTree/Image/HorizontalLine.md` | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | `11_Case/Image/HorizontalLine.md` | fixed position, RAW, Dark, repeatability, correction result | Mapped |
| Ghost 残影 | `09_DecisionTree/Image/Ghost.md` | `07_FailureKnowledge/ImageFailure/` | `11_Case/Image/Ghost.md` | previous frame, current frame, exposure history, RAW, frame sequence | Mapped |
| 加载 Gain 后图像灰度不均匀 | Image classification; calibration path | `07_FailureKnowledge/CalibrationFailure/`, `ImageFailure/` | — | pre/post Gain images, Gain data, uniformity result, RAW | Candidate only |
| 坏点簇 | `09_DecisionTree/Image/BlackDot.md`, `WhiteDot.md` | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | `11_Case/Image/BlackDots.md`, `WhiteDots.md` | cluster coordinates, RAW, Defect Template, repeated frames | Mapped |
| 坏线 | `09_DecisionTree/Image/HorizontalLine.md`, `VerticalLine.md` | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | `11_Case/Image/HorizontalLine.md`, `VerticalLine.md` | row/column coordinate, RAW, repeatability, correction result | Mapped |
| 图像灰度值不随曝光剂量增加 | Image classification; no dedicated DecisionTree file currently | `07_FailureKnowledge/ImageFailure/` | — | dose series, pixel statistics, RAW, generator mA/kV, exposure log | Candidate only |
| 饱和阶梯 | Image classification; no dedicated DecisionTree file currently | `07_FailureKnowledge/ImageFailure/` | — | dose series, saturation level, RAW histogram, mA/kV | Candidate only |
| CrossTalk | Image classification; no dedicated DecisionTree file currently | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | — | adjacent-pixel response, exposure pattern, RAW, spatial correlation | Candidate only |
| Microphony | Image classification; no dedicated DecisionTree file currently | `07_FailureKnowledge/HardwareFailure/`, `EnvironmentFailure/` | — | mechanical condition, acquisition sequence, RAW, repeatability | Candidate only |
| EMC 干扰 | Image classification; no dedicated DecisionTree file currently | `07_FailureKnowledge/EnvironmentFailure/`, `HardwareFailure/` | — | interference timing, environment, cable/ground condition, RAW, repeatability | Candidate only |
| 横竖条纹 | `09_DecisionTree/Image/HorizontalLine.md`, `VerticalLine.md` | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | `11_Case/Image/HorizontalLine.md`, `VerticalLine.md` | orientation, fixed position, RAW, repeatability, correction result | Mapped |
| 过度带 | Image classification; no dedicated DecisionTree file currently | `07_FailureKnowledge/ImageFailure/` | — | boundary location, dose series, RAW, processed image | Candidate only |
| 曝光行 | `09_DecisionTree/Image/HorizontalLine.md` | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | — | row position, exposure sequence, trigger timing, RAW | Candidate only |
| 等距竖条纹 | `09_DecisionTree/Image/VerticalLine.md` | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | `11_Case/Image/VerticalLine.md` | periodicity, column interval, RAW, repeatability, frequency relation | Mapped |
| 原始暗场图灰度值异常 | Image classification; calibration path | `07_FailureKnowledge/CalibrationFailure/`, `ImageFailure/` | — | Dark RAW, mean/std, histogram, temperature, acquisition condition | Candidate only |
| 拼接错误 | `09_DecisionTree/Image/Mosaic.md` | `07_FailureKnowledge/ImageFailure/`, `SoftwareFailure/` | `11_Case/Image/Mosaic.md` | tile boundaries, RAW tiles, processed image, SDK version, assembly log | Mapped |
| 拉链线 | Image classification; no dedicated DecisionTree file currently | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | — | line periodicity, RAW, correction result, repeatability | Candidate only |
| 按压伪影 | Image classification; no dedicated DecisionTree file currently | `07_FailureKnowledge/EnvironmentFailure/`, `ImageFailure/` | — | pressure location, before/after pressure, recovery time, RAW | Candidate only |
| 栅纹无法去除 | Image classification; gate/readout candidate path | `07_FailureKnowledge/HardwareFailure/`, `CalibrationFailure/` | — | RAW, correction result, template, fixed pattern, repeatability | Candidate only |
| 黑斑 | `09_DecisionTree/Image/BlackDot.md` | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | `11_Case/Image/BlackDots.md` | coordinates, size, repeatability, RAW, Defect result | Mapped |
| 丢包 | `09_DecisionTree/Connection` network tree | `07_FailureKnowledge/ConnectionFailure/` | — | Ping, packet capture, SDK log, timestamps, packet statistics | Candidate only |
| 平板不上电 | `09_DecisionTree/Power` if present; otherwise system/power path | `07_FailureKnowledge/SystemFailure/`, `HardwareFailure/` | — | input power, indicator state, current, logs, power sequence | Candidate only |
| 平板指示灯异常 | Power/system path | `07_FailureKnowledge/SystemFailure/`, `HardwareFailure/` | — | LED state, power state, startup sequence, photos | Candidate only |
| 内触发曝光不上图 | `09_DecisionTree/Acquisition` / Software path if present | `07_FailureKnowledge/SoftwareFailure/`, `ConnectionFailure/` | — | trigger mode, exposure event, acquisition log, timeout, image callback | Candidate only |
| 外触发曝光不上图 | `09_DecisionTree/Acquisition` / Connection path if present | `07_FailureKnowledge/SoftwareFailure/`, `ConnectionFailure/` | — | external trigger timing, Evt_Exp_Enable/Prohibit, acquisition log | Candidate only |
| 软触发曝光不上图 | `09_DecisionTree/Software` acquisition path | `07_FailureKnowledge/SoftwareFailure/`, `ConnectionFailure/` | — | Cmd_StartAcq, timeout, callback/log, detector state | Candidate only |
| mA 过高/低 | Generator path; no dedicated Image DecisionTree | `07_FailureKnowledge/SystemFailure/` | — | commanded vs measured mA, generator log, exposure result | Candidate only |
| kV 过高/低 | Generator path; no dedicated Image DecisionTree | `07_FailureKnowledge/SystemFailure/` | — | commanded vs measured kV, generator log, exposure result | Candidate only |
| 通道跌落 | Readout/channel candidate path | `07_FailureKnowledge/HardwareFailure/`, `ImageFailure/` | — | fixed channel/row/column, RAW, repeated frames, hardware evidence | Candidate only |
| 本底跳动 | Image/calibration/environment path | `07_FailureKnowledge/ImageFailure/`, `EnvironmentFailure/` | — | repeated Dark frames, mean/std trend, temperature, time series | Candidate only |
| 本底漂移 | Image/calibration/environment path | `07_FailureKnowledge/ImageFailure/`, `EnvironmentFailure/` | — | Dark time series, temperature, warm-up state, RAW | Candidate only |
| 曲线异常 | Image/Tool analysis path | `07_FailureKnowledge/ImageFailure/`, `CalibrationFailure/` | — | profile curve, ROI, raw/processed comparison, calibration state | Candidate only |
| 灵敏度偏低 | Image/calibration/generator path | `07_FailureKnowledge/CalibrationFailure/`, `ImageFailure/` | — | dose-response curve, mA/kV, RAW mean, Gain data, baseline | Candidate only |
| 潮解 | Environment path | `07_FailureKnowledge/EnvironmentFailure/`, `HardwareFailure/` | — | environmental conditions, detector condition/photos, temperature/humidity | Candidate only |
| 白点 | `09_DecisionTree/Image/WhiteDot.md` | `07_FailureKnowledge/ImageFailure/`, `HardwareFailure/` | `11_Case/Image/WhiteDots.md` | coordinates, repeatability, RAW, Defect Template, correction result | Mapped |
| 软触发曝光超时 | `09_DecisionTree/Software` acquisition path | `07_FailureKnowledge/SoftwareFailure/` | — | timeout event, SDK log, detector state, trigger command | Candidate only |
| AED 曝光不上图 | Acquisition/AED path; no dedicated Image DecisionTree currently | `07_FailureKnowledge/SoftwareFailure/`, `SystemFailure/` | — | AED state, exposure detection, acquisition log, trigger timing | Candidate only |
| 探测器过热 | Power/thermal/environment path | `07_FailureKnowledge/EnvironmentFailure/`, `HardwareFailure/` | — | temperature log, duty cycle, ambient condition, recovery behavior | Candidate only |

## Existing image Case set

The current image Case set contains nine files: `BlackDots`, `WhiteDots`, `HorizontalLine`, `VerticalLine`, `Ghost`, `Lag`, `Mosaic`, `Noise`, and `ImageShift`. These are the first verified Case anchors for image diagnosis. 

## Sample-image rule

An image sample is only promoted to a reusable knowledge sample when the repository has the actual image file plus enough metadata to explain what the image demonstrates. Required metadata: phenomenon, product/model, detector SN when permitted, firmware, SDK, exposure condition, image type (RAW/Dark/processed), diagnosis status, and linked Case/DecisionTree.

Do not invent or fabricate image samples. If an image exists only in a chat attachment and has not been committed into the repository as an artifact, record it as `Pending Repository Artifact` rather than pretending that a repository image exists.
