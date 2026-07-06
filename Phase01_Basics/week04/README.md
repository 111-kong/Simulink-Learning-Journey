# Week 4：闭环跟踪 + 子系统 + Mask

**目标**：搭出完整反馈闭环，把「控制器 + 被控对象」打包成层级化子系统，并用 Mask 做出可配置的参数面板。

## 模型清单

| 文件 | 内容 | 关键技能 |
|------|------|---------|
| `closed_loop_tracking.slx` | 闭环阶跃跟踪：目标 → PID → Plant → 反馈 → Scope | Mux 合并多路信号 |
| `disturbance_test.slx` | 加入阶跃干扰，验证抗扰能力 | 反馈抗扰 |
| `subsystem_demo.slx` | 把 PID + Plant 封装为子系统并加 Mask 参数面板 | Subsystem + Mask |
| `pid_112.slx` | PID 综合练习 | 综合应用 |

> 注：`disturbance_test.slx.autosave` 为自动备份，已被 `.gitignore` 忽略。

## 知识点

- **闭环反馈**：误差 e = r − y 驱动控制器，形成负反馈稳定系统
- **Mux**：把多路标量合并为向量，单 Scope 可看多条曲线
- **Subsystem**：选中模块 → 右键 → 创建子系统，提升层级化与可读性
- **Mask**：右键子系统 → 编辑 Mask → 加参数（ωn / ζ / Kp）+ 初始化代码（`set_param`）
- 初始化代码范例（中文版 Simulink 同样适用）：

```matlab
omega_n_val = str2double(omega_n);
zeta_val    = str2double(zeta);
if isnan(omega_n_val), omega_n_val = 10; end   % 默认值防御
if isnan(zeta_val),    zeta_val = 0.7; end
den = [1, 2*zeta_val*omega_n_val, omega_n_val^2];
num = [omega_n_val^2];
set_param([gcb, '/Transfer Fcn'], 'Numerator',   mat2str(num), ...
                                  'Denominator', mat2str(den));
```

## 踩坑

1. **Scope 只有一条曲线** → 用 Mux 合并「目标 + 实际」再进同一个 Scope
2. **Mask 初始化「参数中的一个或多个条目不是有限值」** → 检查对话框是否留空 / 填 0，在代码里加 `isnan` 默认值防御，并确保 `set_param` 的模块名与模型完全一致

## 周末验证（Week 4 目标）

- [x] **层级化模型带参数面板**：双击 `subsystem_demo` 弹出 Mask 面板，修改 ωn / ζ / Kp 后仿真结果随之变化

## 面试一句话

> "Week 4 我能独立搭建反馈闭环并做抗扰验证，会用 Subsystem + Mask 把控制算法封装成带参数面板的层级化模块——这正是工程里交付可复用模型的方式。"
