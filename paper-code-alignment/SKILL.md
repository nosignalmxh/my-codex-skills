---
name: paper-code-alignment
description: align a research paper with its codebase by scanning the repo, locating configs and training scripts, mapping paper modules to code modules, and auditing implementation or reproduction gaps. use when the user wants 结合代码读论文, 论文代码对齐, implementation verification, repo scanning, or reproducibility analysis.
---

# Paper Code Alignment

默认输出语言：中文。这个 skill 的重点不是讲论文，而是用代码验证论文。

## 何时使用

当用户同时给了论文和仓库，或者明确要求“结合代码读论文”“对齐论文模块和代码模块”“检查复现一致性”时，使用这个 skill。

## 必做工具协同

只要有本地仓库，就主动做 repo reconnaissance，不要停留在 prompt 级解释：

- 用 `rg --files` / `rg` 扫描目录
- 找入口脚本、训练脚本、评测脚本、配置文件、数据处理脚本
- 找模型定义、损失项、数据集注册、日志与结果文件

不要在没有代码证据时声称“仓库实现了论文中的 X”。

## 输入归一化

至少整理出：

- 论文文本或关键片段
- 仓库路径或代码链接
- 用户目标：理解实现、复现、审计一致性、定位 bug
- 是否允许运行命令或轻量实验

缺信息时：

- 标 `【未知】`
- 给出最小补充字段
- 继续做静态对齐分析

## 固定流程

### Phase 1. Repo Reconnaissance

先建立仓库地图：

- 顶层目录用途
- 训练 / 评测 / 推理入口
- 配置系统
- 数据处理路径
- checkpoints / logs / results 是否存在

优先使用 `references/repo-scan-checklist.md`。

### Phase 2. Paper-to-Code Map

把论文方法拆成模块，再逐一寻找代码对应物：

- 论文组件 / 算法阶段
- 对应文件、类、函数、配置键
- 关键参数
- 证据位置

表格结构使用 `references/paper-code-map-template.md`。

### Phase 3. Implementation Delta Audit

检查论文叙述与实际实现的差异：

- 论文写了但代码没实现
- 代码实现了但论文没强调
- 训练技巧、默认参数、工程化调整
- 替代实现路径

如果存在多个版本：

- 优先以官方 README 推荐路径和默认配置为主
- 明确标注不同脚本之间的差异

### Phase 4. Experiment Reproduction Audit

回答：

- 数据集如何准备
- 指标如何计算
- 训练命令是什么
- 关键随机性或环境依赖是什么
- 从 README 到跑通之间缺了哪些步骤

若用户允许运行命令，再补：

- 依赖检查
- 配置合法性检查
- 入口脚本 dry run 或 `--help`

### Phase 5. Final Alignment Verdict

最终给出：

- 哪些论文 claim 被代码直接支持
- 哪些实现细节是代码才暴露出来的
- 哪些地方仍无法确认
- 一份最小复现路径

## 输出纪律

- 代码引用尽量给到文件路径和行号
- 不把 README 文案当成实现证据
- 如果 repo 太大，先建立高置信度模块图，再深挖关键路径
- 区分“代码存在”和“代码实际被训练脚本调用”

## 推荐输出骨架

优先按 `references/reproduction-audit-template.md` 输出。如果用户只要 paper-to-code map，则保留对齐矩阵和关键差异即可。
