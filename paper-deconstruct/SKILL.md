---
name: paper-deconstruct
description: deconstruct a research paper into reusable components, generate component cards and dependency graphs, explain one component in depth, and produce a full structured obsidian-friendly paper breakdown. use when the user wants 论文组件化解构, 单组件精讲, 全文结构化拆解, componentization, block-library extraction, or reverse-engineering of author choices.
---

# Paper Deconstruct

默认输出语言：中文。除非用户指定，否则使用适合 Obsidian 的 Markdown。

## 何时使用

当用户想把论文拆成可复用技术组件，而不是只做摘要式总结时，使用这个 skill。它合并了三类稳定任务：

1. 论文组件化解构
2. 单组件精讲
3. 全文结构化拆解

## 先判断工作模式

先把用户需求归一成以下三种模式之一：

- `full`: 需要从整篇论文得到组件 DAG、组件卡、全文拆解、组块库条目和研究重构路线
- `component`: 用户已经指定某一个组件，或提供了组件卡，只需要讲透这个模块
- `hybrid`: 先做全局组件化，再对 1-3 个关键组件补精讲

如果用户没有明确说明，默认使用 `hybrid`。

## 输入归一化

尽量整理出以下字段：

- 论文文本来源：PDF、网页、摘录、附录
- 任务目标：复现、理解、组块积累、找 idea
- 用户背景：领域、数学水平、是否已有组件库
- 关注范围：整篇、方法部分、实验部分、某一组件

如果缺信息：

- 明确标 `【未知】`
- 给出最小补充信息清单
- 但不要停止，先完成当前最保守、最可证据化的版本

## 固定流程

### Phase 1. 全局扫描

先提炼：

- 总问题是什么
- 论文真正的杠杆点是什么
- 章节骨架和 3-7 条核心 claim

所有 claim 尽量绑定到 Section / Figure / Table / Equation / Algorithm / Appendix。

### Phase 2. 组件化拆解

将论文拆成 8-25 个最小组件。组件标准：

- 一个组件只解决一个最小技术问题
- 继续拆会变成两个以上独立决策时，说明已经足够小
- 组件名称优先用“动词 + 名词”

每个组件必须输出组件卡。卡片字段使用 `references/component-card-template.md`。

同时输出：

- 组件依赖关系
- 关键路径
- 可选增强组件

### Phase 3. 逆向还原作者脚手架

将作者从直觉到方案收敛的过程拆成：

- 初始直觉
- 至少 3 个关键岔路点
- 每个岔路点可能失败的备选方案
- 最终为什么收敛到当前组件组合

这里必须显式区分：

- `【论文原文】`
- `【推断】`

### Phase 4. 单组件精讲

当模式是 `component` 或 `hybrid` 时，对关键组件补一轮精讲：

- 最小技术问题是什么
- 没有它会怎样失败
- 输入 -> 关键动作 -> 输出
- 公式与算法直觉
- 复现要点、常见坑、debug 方法
- 2 个最关键的 ablation / diagnostic

如果用户没有指定组件，优先选：

1. 关键路径上的瓶颈组件
2. 最容易复用的组件
3. 最容易误解的组件

### Phase 5. 全文结构化拆解

对整篇论文给出稳定的大纲化说明：

1. 核心思想和核心做法
2. 问题提出
3. 前人工作与缺口
4. 方法架构与出发点
5. 实验设计
6. 实验结果说明
7. 局限和未来方向
8. Mermaid 流程图
9. Python 伪代码
10. 附录作用
11. 读者最该注意的实现细节
12. 领域内其他可行思路

### Phase 6. 组块库输出

把论文沉淀成可复用条目：

- 组块库目录结构
- 5-12 个组块条目标题
- 可跨任务复用的组件
- 强依赖场景的组件

条目格式优先使用 `references/block-library-template.md`。

## 输出纪律

- 任何无法从原文确认的内容都标 `【未知】` 或 `【推断】`
- 不要把“全文总结”写成一大段散文
- 少用形容词，多写机制、依赖、失败模式
- 单组件精讲时，紧贴论文原文，不要脱离上下文泛讲
- 有图表或公式时，优先给锚点而不是空泛解释

## 推荐输出骨架

默认按 `references/obsidian-output-template.md` 组织最终回答。若用户只要组件卡或只要单组件精讲，则保留对应分块，删除无关章节。
