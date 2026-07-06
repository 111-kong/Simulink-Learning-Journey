# Week 3：PID 控制

**目标**：理解 PID 三个环节各自作用，掌握手动整定与 Ziegler-Nichols 方法，认识积分饱和与抗饱和。

## 模型清单

| 文件 | 内容 |
|------|------|
| `pid_111.slx` | PID 三参数整定练习：P → PI → PID，含 Ziegler-Nichols 整定与抗扰 |

> 注：`pidcc.slx.autosave` / `pidcc.slx.original` 为 Simulink 自动备份，已被 `.gitignore` 忽略，无需关注。

## 知识点

- **P（比例）**：快速响应，但存在稳态误差
- **I（积分）**：消除稳态误差，但引入相位滞后，可能超调 / 振荡
- **D（微分）**：预测趋势、抑制超调，对噪声敏感
- **Ziegler-Nichols**：先增大 Kp 到临界振荡，记录临界增益 Ku 与振荡周期 Tu，再按经验表取 Kp / Ki / Kd
- **积分饱和 (Windup)**：执行器限幅时积分项持续累积，需 anti-windup（如钳位 / 回差）抑制

## 整定记录（按实际模型填写）

- ZN 法示例：Ku ≈ ?，Tu ≈ ? → Kp ≈ 30, Ki ≈ 3.2, Kd ≈ 0.8
- 手动微调：Kp = 50, Ki = 0.5, Kd = 5（低 Ki 抑制振荡）

## 面试一句话

> "Week 3 我掌握了 PID 三环节的物理意义与 Ziegler-Nichols 整定流程，知道积分饱和的成因和 anti-windup 的必要性。"
