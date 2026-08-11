# Image Phenomenon Catalog

| 类别 | 异常现象 |
|---|---|
| Pixel | 坏点、黑点、白点、坏点蔟 |
| Line / Pattern | 坏线、横条纹噪声、横竖条纹、等距竖条纹、拉链线、过度带、曝光行 |
| Channel / Readout | Read 通道伪影、Gate 通道伪影、通道伪影、通道跌落 |
| Noise / Baseline | 图像颗粒噪声、本底跳动、本底漂移、曲线异常 |
| Uniformity | 加载 Gain 图像灰度不均匀、灵敏度偏低 |
| Dynamic / Exposure | Ghost 残影、图像灰度值不随曝光剂量增加、饱和阶梯、mA 过高/低、kV 过高/低 |
| Geometry / Processing | 图像不规则伪影、图像奇偶差异明显、拼接错误、Image Shift、按压伪影 |
| Calibration | 原始暗场图灰度值异常、栅纹无法去除 |
| Interference | EMC 干扰、Microphony |
| Communication | 丢包 |
| Power / Thermal | 平板不上电、平板指示灯异常、探测器过热 |
| Exposure / Trigger | 内触发曝光不上图、外触发曝光不上图、软触发曝光不上图、AED 曝光不上图、软触发曝光超时 |

## 使用规则

1. 先按图像/现场现象分类。
2. 再提取空间、时间、剂量、重复性等特征。
3. 只有证据充分时才进入 Read / Gate / Channel / Hardware 等机制判断。
4. 新 Case 验证完成后，将图片、证据、Root Cause 和 Resolution 反哺对应条目。
