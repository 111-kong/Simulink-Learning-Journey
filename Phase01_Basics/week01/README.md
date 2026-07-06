# Week 1：基础模块与信号运算

**目标**：熟悉 Simulink 操作界面，掌握最常用信号源 / 运算 / 观测模块，理解信号叠加与相乘的时域与频域含义。

## 模型清单

| 文件 | 内容 | 关键模块 |
|------|------|---------|
| `my_first_model.slx` | 第一个模型：正弦波经增益进示波器 | Sine Wave, Gain, Scope |
| `gain_comparison.slx` | 对比不同增益对幅度/相位的影响 | Gain（多组并联） |
| `scale_offset.slx` | 缩放 + 偏置：y = a·x + b | Constant, Gain, Add |
| `wave_superposition.slx` | 多个正弦波叠加成复合信号 | Sine Wave ×N, Add |
| `product_demo.slx` | 两信号相乘（AM 调幅直觉） | Product |
| `waveform.png` | 波形截图参考 | — |

## 知识点

- **Sine Wave 参数**：幅值 (Amplitude)、频率 (rad/s)、相位 (Phase)
- **Gain** 改变信号幅度；**Add** 做加减；**Product** 做相乘
- **信号叠加 → 频域多根谱线**（各频率分量独立存在）
- **信号相乘 → 频谱搬移**（AM 调幅的本质：载波 × 包络）

## 面试一句话

> "Week 1 我熟悉了 Simulink 信号流建模，能用基础模块搭出信号叠加与相乘，并理解时域运算和频域谱线/搬移的对应关系。"
