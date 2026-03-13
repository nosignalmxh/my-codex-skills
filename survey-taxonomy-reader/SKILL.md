---
name: survey-taxonomy-reader
description: read a survey paper by building a taxonomy, unified notation table, representative-method comparison, and math-first deep dives. use when the user wants 阅读综述, taxonomy extraction, 统一符号表, 代表方法对比, benchmark summaries, or a reusable survey study template.
---

# Survey Taxonomy Reader

默认输出语言：中文。默认把综述读成“taxonomy + 统一符号 + 代表方法对比”，而不是逐段复述。

## 何时使用

当用户在读 survey / review / tutorial 类论文，想快速建立领域结构，再对代表方法做数学或机制层面的精读时，使用这个 skill。

它合并两种稳定模式：

1. 课程式综述精读
2. 数学优先的统一建模阅读

## 先判断工作模式

- `guided`: 按章节带读，每次只讲一个部分，适合交互式学习
- `full-map`: 一次性输出 taxonomy、符号表、代表方法表、benchmarks、挑战与未来方向
- `math-first`: 背景最少化，集中在统一形式化、损失函数、推导和统计假设

未指定时默认 `full-map`。

## 输入归一化

整理出：

- survey 文本
- 领域名称
- 用户重点：taxonomy、方法、数学、应用、benchmarks
- 是否要按交互式一步步推进

缺信息时：

- 对领域名或应用背景标 `【未知】`
- 但仍先构建 taxonomy 主树

## 固定流程

### Phase 1. Scope and Definitions

先说明：

- 这篇综述覆盖的问题边界
- 核心术语及其定义
- 综述试图解决的核心认知负担

### Phase 2. Taxonomy Build

输出 taxonomy 树或 Mermaid 思维导图，并解释：

- 作者是按数据模态、算法假设、任务场景还是应用链路分类
- 这个分类有没有明显遗漏或混叠

优先使用 `references/taxonomy-template.md`。

### Phase 3. Notation Standardization

统一符号表，至少整理：

- 输入空间
- 输出空间
- 参数
- 隐变量
- 分布
- 目标函数和正则项

优先使用 `references/notation-table-template.md`。

### Phase 4. Representative Method Comparison

从每个大类挑 2-3 个代表方法，比较：

- 核心假设
- 目标函数
- 优化方式
- 复杂度
- 数据需求
- 可解释性

使用 `references/method-comparison-template.md`。

### Phase 5. Math-First Deep Dive

如果用户偏数学，重点做：

- 统一问题形式化
- 省略推导的补全
- 近似推断 / 优化技巧
- 隐含统计假设及其失效后果

独立公式用 LaTeX 单独成行，不放进代码块。

### Phase 6. Datasets, Benchmarks, and Evaluation

总结：

- 常用 benchmark
- 常用指标
- 指标偏统计意义还是偏应用意义
- 该领域默认的实验比较习惯

### Phase 7. Challenges and Reading Plan

给出：

- 当前挑战
- 作者提出的未来机会
- 综述遗漏的重要工作或盲区
- 建议继续深挖的代表论文列表

## Guided 模式

如果用户要求“一次只讲一个部分”，按以下顺序：

1. 宏观概览与定义
2. Taxonomy
3. 代表方法
4. 数据与基准
5. 挑战与未来
6. 总结与批判

每次只输出一个部分，结尾问是否进入下一部分。

## 输出纪律

- 不把 survey 当作事实终点，必要时指出作者分类的局限
- 不要把应用背景讲得过长，重点放在结构和统一形式化
- 如果用户有明确领域，例如计算生物或 NLP，可以适度补领域语义，但不要牺牲统一模板
