# Simulink + ROS 学习记录

研一（2026年7月）→ 研二秋招（2027年9月）长期学习计划。
每日 30~45 分钟，七阶段进阶。

---

## 阶段进度

- [x] **Phase 1：Simulink 基础建模（第1-5周，2026年7月）— Week 1-4 已完成，Week 5 阶段考核待做**
- [ ] Phase 2：Stateflow + 线性化分析（第6-9周，2026年8月）
- [ ] Phase 3：代码生成 Embedded Coder（第10-17周，2026年9-10月）⭐ 主战场
- [ ] Phase 4：dSPACE + ControlDesk（第18-25周，2026年11-12月）
- [ ] Phase 5：ROS + Simulink ROS Toolbox（第26-31周，2027年1-2月）
- [ ] Phase 6：行业实战项目组合（第32-43周，2027年3-5月）
- [ ] Phase 7：面试冲刺 + 简历包装（第44-62周，2027年6-9月）

---

## Phase 1 明细（Week 1–4，基础建模）

### 文件清单 (File Inventory)

```
Phase01_Basics/
├── week01/                      # 基础模块 + 信号运算
│   ├── my_first_model.slx       # 第一个模型：Sine Wave → Gain → Scope
│   ├── gain_comparison.slx      # 增益对比
│   ├── scale_offset.slx         # 缩放 + 偏置 (Constant + Gain + Add)
│   ├── wave_superposition.slx   # 多正弦信号叠加 (Add)
│   ├── product_demo.slx         # 信号相乘 (Product)
│   └── waveform.png             # 波形截图参考
├── week02/                      # 一阶 / 二阶 / 状态空间
│   ├── first_order_comparison.slx        # 一阶系统时间常数对比 (63.2%)
│   ├── second_order_comparison.slx       # 二阶系统阻尼比对比 (欠/临界/过阻尼)
│   ├── natural_frequency_comparison.slx  # 固有频率 ωn 对比
│   └── mass_spring_damper.slx   # 质量-弹簧-阻尼物理模型 (集总参数)
├── week03/                      # PID 控制
│   └── pid_111.slx              # PID 三参数整定 (P / PI / PID + Ziegler-Nichols)
└── week04/                      # 闭环跟踪 + 子系统 + Mask
    ├── closed_loop_tracking.slx # 完整闭环：目标→PID→Plant→反馈→Scope(Mux)
    ├── disturbance_test.slx     # 抗扰验证 (加阶跃干扰)
    ├── subsystem_demo.slx       # 子系统封装 + Mask 参数面板 (ωn/ζ/Kp)
    └── pid_112.slx              # PID 综合练习
```

> 说明：`*.autosave` 和 `*.original` 是 Simulink 自动备份文件，已在 `.gitignore` 中忽略，不要提交。

### 每周能力小结 (Weekly Summary)

| Week | 主题 | 核心能力 | 简历对应点 |
|:----:|:-----|:---------|:-----------|
| 1 | 基础模块与信号运算 | Sine Wave / Gain / Add / Product / Scope 搭建与信号叠加 | Simulink 基础建模 |
| 2 | 一阶 / 二阶 / 状态空间 | 时间常数、阻尼比、固有频率、质量-弹簧-阻尼建模 | 动态系统建模 |
| 3 | PID 控制 | P / PI / PID 三参数作用、Ziegler-Nichols 整定 | 经典控制 |
| 4 | 闭环 + 子系统 + Mask | 反馈闭环、抗扰、Subsystem 层级化、Mask 参数面板 | 模型层级化设计 |

### 踩坑记录 (Gotchas，面试可讲)

1. **Scope 只显示一条曲线** → 用 `Mux` 把目标值和实际值合并成向量再进同一个 Scope。
2. **Mask 初始化报错「参数中的一个或多个条目不是有限值」** → Mask 对话框留空或填 `0` 会让 `str2double` 返回 `NaN`；在初始化代码里加默认值防御（`if isnan(x), x=默认值; end`），并确保模块名与 `set_param` 完全一致。
3. **MATLAB R2021b 启动崩溃 (Access Violation / m_lxe.dll)** → 旧显卡 OpenGL 硬件加速冲突，用 `-softwareopengl` 启动参数或 `opengl('save','software')` 切软件渲染解决。

---

## 目录结构

```
G:\Simulink-Learning-Journey\
├── README.md                          ← 本文件，进度总览
├── Simulink长期学习规划_研一至秋招.md   ← 62周详细计划
├── .gitignore                         ← 忽略 Simulink 自动备份
├── Phase01_Basics/                    ← 阶段一：基础建模 (Week1-4 已完成)
│   ├── week01/ ~ week04/              ← 每周一个文件夹，内含 README.md
├── Phase02_Stateflow/                 ← 阶段二：Stateflow
├── Phase03_CodeGen/                   ← 阶段三：代码生成
├── Phase04_dSPACE/                    ← 阶段四：dSPACE
├── Phase05_ROS/                       ← 阶段五：ROS集成
├── Phase06_Projects/                  ← 阶段六：项目实战
└── Phase07_Interview/                 ← 阶段七：面试冲刺
```

---

## 贯穿习惯

- ✅ **Git 提交**：每个练习都 commit，面试时给链接
- ✅ **面试素材积累**：Phase 3 起每周15分钟自问自答
- ✅ **简历迭代**：每阶段结束更新一版简历
- ✅ **ROS 环境**：Phase 1-2 期间装好 Ubuntu + ROS2

---

## 核心技能目标

```
Simulink 建模（熟练） +
Stateflow 状态逻辑（熟练） +
Embedded Coder 代码生成（深度掌握） ← 稀缺
+ dSPACE/桌面实时部署（掌握工作流） +
ROS + Simulink ROS Toolbox 集成（打通） ← 稀缺
+ 实际项目经验（可讲15分钟的故事）
```

---

*启动日期：2026-07-05 · 最近更新：2026-07-06（Phase 1 Week1-4 README 补全）*
