---
name: paper-review-audit
description: audit a paper like a strong reviewer with claim-evidence-falsify tables, stepwise red-teaming, and comparison against field consensus or active controversy. use when the user wants 强批判审稿报告, 分步红队, 共识与争议对比, rigorous criticism, reviewer-style questions, or evidence-disciplined paper auditing.
---

# Paper Review Audit

默认输出语言：中文。默认站在严格 reviewer 视角，优先证据纪律而不是“讲懂”。

## 何时使用

当用户要的是审断、挑错、证据对齐、拒稿理由、反驳点或 reviewer workflow，而不是摘要讲解时，使用这个 skill。

它合并三类稳定任务：

1. 强批判审稿报告
2. 分步红队
3. 行业共识与争议对比

## 先判断输出模式

- `full-review`: 一次性产出完整 reviewer 报告
- `stepwise-redteam`: 严格按步骤推进，每次只做一步并询问是否进入下一步
- `consensus-compare`: 在 reviewer 审计基础上，再与真实文献中的主流共识和争议对比

如果用户没有指定，默认 `full-review`。如果用户明确说“逐步来”，使用 `stepwise-redteam`。

## 输入归一化

整理出：

- 论文原文、附录、代码、补充材料
- 用户是否允许联网或需要外部文献对比
- 目标粒度：整篇、某个 claim、方法部分、实验部分

如果缺内容：

- 标 `论文未提及 / 无法从原文确认`
- 不要补全作者意图

## 核心原则

### 证据纪律

所有关键结论都尽量绑定：

- Section
- Figure
- Table
- Equation
- Appendix
- 代码位置（若提供）

明确区分：

- `原文可证据化事实`
- `你的批判性推理`

### 每条批判都要可检验

每个 weakness、替代解释或质疑，都至少给一个最小验证方式：

- 实验
- 反例
- 推导检查
- 对照设计

## 固定流程

### Phase 1. Claim Map

从 Abstract / Introduction / Conclusion 提取 5-10 条最重要 claim，写成可证伪句式，并建立台账。表头优先使用 `references/reviewer-report-template.md`。

### Phase 2. Evidence Stress Test

对每条 claim 检查：

- 证据是否直接
- 证据是否必要且充分
- 是否有混杂因素
- 最小反例是什么
- weakest link 在哪里

### Phase 3. Method and Theory Audit

补全 2-3 个最关键公式或推导的中间步骤，并检查：

- 结论依赖哪些假设
- 假设一旦不成立会如何崩
- 论文是否明确讨论适用范围

### Phase 4. Experiment Alignment Audit

逐组实验回答：

- 这组实验在验证哪条 claim
- baseline 是否足够强
- 调参预算、训练时长、数据预处理是否可比
- 缺了哪些消融、失败案例、显著性或敏感性分析

### Phase 5. Alternative Explanations

至少给出 3 个能解释结果的替代机制，并为每个机制设计最小对照实验。优先使用 `references/red-team-checklist.md` 的问题清单。

### Phase 6. Consensus and Controversy Compare

只有在用户明确允许联网、或明确要求外部文献对比时，才执行这一步：

- 找出该论文延续了哪些主流共识
- 哪些结论正处于争议中
- 最近文献里是否有相反证据或负面结果

输出时严格分开：

- 论文原文的说法
- 真实文献支持的说法
- 尚无定论的争议点

优先使用 `references/consensus-controversy-template.md`。

### Phase 7. Reviewer Verdict

最后给出 reviewer 风格结论：

- Strengths，最多 3 条，必须具体
- Weaknesses，必须有证据指向
- Questions to Authors，至少 8 个，并标明影响哪个 claim
- 最终建议：Accept / Weak Accept / Weak Reject / Reject

## Stepwise Red Team 模式

如果是 `stepwise-redteam`，强制按以下顺序：

1. Claim Map
2. Evidence Stress Test
3. Alternative Explanations and Control Experiments
4. Reject Draft and Possible Rebuttal

每次只输出当前步骤，结尾必须问是否进入下一步。

## 输出纪律

- 严禁“作者可能想表达”
- 严禁编造外部论文或引用
- 若没有外部文献支持，就明确写 `未检索到可靠文献`
- 不要把批判写成情绪化评价，重点是 weakest link 和 falsification path
