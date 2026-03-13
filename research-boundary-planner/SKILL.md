---
name: research-boundary-planner
description: turn a paper or repo into a practical research extension plan with baseline reproduction, boundary tests, mechanism hypotheses, ablation priorities, improvement routes, milestones, and writing outline. use when the user wants 找边界, 思考可做的 idea, boundary testing, ablation planning, or to move from reading to concrete experiments.
---

# Research Boundary Planner

默认输出语言：中文。这个 skill 的目标不是“再总结一次论文”，而是从论文走到可执行研究计划。

## 何时使用

当用户希望基于论文或代码做以下事情时，使用这个 skill：

- 基线复现
- 边界测试
- 从现象提出可检验机理假设
- 设计改进路线
- 排消融优先级
- 做 4-8 周研究里程碑
- 提前搭论文图表与写作骨架

它合并两类稳定任务：

1. 思考可做的 idea
2. 找边界

## 输入归一化

至少整理出：

- 论文或代码链接 / 路径
- 主题
- 现有实验设定：数据集、指标、baseline
- 资源约束：GPU、时间、是否可联网、是否能运行代码
- 用户目标：复现、改进、投稿、组会、立项

如果缺信息：

- 用默认假设补齐并显式写出
- 再列一个“最小补充字段清单”

## 固定流程

### Phase 1. Baseline Reproduction Plan

先给出可运行的基线路径：

- 环境依赖
- 数据准备
- 训练 / 评测命令
- 预期产物
- 最可能失败点

如果已有 repo，优先结合代码实际结构，不要只写通用空话。

### Phase 2. Boundary Matrix

系统化设计至少 6 类边界测试，并给强度分级。优先使用 `references/boundary-test-matrix-template.md`。

边界轴可以包括：

- 数据规模
- 数据噪声
- 分布偏移
- 类别不平衡
- 模块移除
- 超参数敏感性
- 计算预算
- 推理时约束

### Phase 3. Phenomenon to Mechanism

从预期现象反推可检验机制：

- 观察到什么现象
- 背后可能机制是什么
- 如何设计最小验证实验
- 什么结果会推翻这个解释

### Phase 4. Improvement Routes

至少提出 3 条有动机的改进路线，每条都要写：

- 新假设
- 代码改动点位
- 训练开销
- 预期收益
- 最小实验闭环

如果用户要求保持原实验设置不变，就默认复用原数据集、指标和 baseline，只改方法。

### Phase 5. Ablation Priority

设计 12 组以上消融，并按优先级排序。优先使用 `references/ablation-priority-template.md`。

排序原则：

- 先验证主假设
- 再验证关键组件
- 最后做细节增益和鲁棒性

### Phase 6. Milestones and Deliverables

做 4-8 周时间表，明确：

- 每周目标
- 交付物
- 决策门槛
- kill / continue 条件

### Phase 7. Writing Skeleton

提前搭论文或汇报骨架：

- 要画哪些图
- 哪些表格最关键
- 摘要 / 引言 / 方法 / 实验各写什么

优先使用 `references/writing-outline-template.md`。

## 输出纪律

- 以命令、表格、伪代码和里程碑为主
- 不假装已有实验结果
- 若无法运行代码，就明确写“计划”而不是“结果”
- novelty 不靠形容词，要靠改动点和可验证假设

## 推荐输出骨架

最终至少包含：

1. 默认假设
2. 可运行基线
3. 边界测试矩阵
4. 机理假设与验证实验
5. 改进路线
6. 消融优先级
7. 4-8 周里程碑
8. 图表与写作骨架
9. 风险与可推广性
