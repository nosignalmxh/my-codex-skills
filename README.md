# research-idea-funnel

`research-idea-funnel` is a Codex skill for turning a broad research direction into a structured idea-discovery workflow: landscape survey, 8-12 candidate ideas, aggressive filtering, claim-level novelty checks, devil's-advocate review, and pilot planning or lightweight pilot execution.

The repository supports two usage modes:

1. Install `research-idea-funnel/` as a standalone Codex skill.
2. Open the whole repository in Codex app and let the root `AGENTS.md` drive the workflow at the project level.

## Repository Layout

```text
.
├── AGENTS.md
├── README.md
└── research-idea-funnel/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
```

## Install as a Codex Skill

Replace `<github-user>` and `<repo>` after publishing the repository.

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo <github-user>/<repo> \
  --path research-idea-funnel
```

Or use the direct GitHub URL:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --url https://github.com/<github-user>/<repo>/tree/main/research-idea-funnel
```

Restart Codex after installation.

## Use in Codex App

### Mode 1: Open the repository and follow `AGENTS.md`

This is the most reliable mode when you want the full repo-level workflow. Open this repository in Codex app, then tell Codex to read `AGENTS.md` and follow the research idea funnel workflow.

### Mode 2: Invoke the installed skill directly

If you installed the skill, explicitly invoke `$research-idea-funnel` in your prompt so Codex uses the packaged skill instructions.

## What to Give the Skill

For best results, include these four things in your prompt:

1. What you roughly want to study.
2. Where you suspect the novelty might be.
3. Your constraints.
4. What output you want from the funnel.

Useful additions:

- what you do not want to do
- preferred paper type: method / systems / evaluation / application
- any papers, repos, baselines, or datasets you already have
- target venue level

## Usage Guide

### Research Idea Funnel 使用指南

## 什么时候用

当你只有一个粗略 research seed，而不是已经打磨好的研究问题时，用这个 workflow 最合适。它适合这类任务：

- 从一个宽泛方向出发做文献扫描
- 自动展开出 8-12 个候选想法
- 快速筛掉拥挤、不可做、或者意义不大的方向
- 对幸存想法做逐条 claim 的 novelty check
- 给出 top 2-3 个 pilot plan
- 最终输出一个保留“推荐想法 + 被淘汰想法”的 IDEA_REPORT

## 两种推荐用法

### 用法 1：作为 repo 级 workflow 使用

先在 Codex app 里打开这个仓库，然后直接说：

`Read AGENTS.md and follow the research idea funnel workflow in this repository.`

这种方式最稳，因为 Codex 会先读仓库根目录的 `AGENTS.md`，再按仓库里的 skill 资料展开。

### 用法 2：作为已安装 skill 使用

如果你已经把这个 skill 安装进 Codex，就显式调用：

`Use $research-idea-funnel ...`

这样 Codex 会直接加载 skill 包内的 `SKILL.md` 和 `references/`。

## 一个好 prompt 最好包含什么

最少给四类信息：

1. 你大概想做什么
2. 你猜测的新意在哪里
3. 你的现实约束
4. 你希望它输出什么

推荐补充：

- 你不想碰的方向
- 你偏好的论文类型
- 你手头已有的论文、repo、baseline、dataset
- 你想投的会议级别

## 最小可用 prompt

```text
Read AGENTS.md and use the research idea funnel workflow in this repository.

Seed idea:
I want to explore agent memory for long-horizon coding tasks.

Initial intuition:
Maybe current agent memory is too flat and loses task structure over long sessions.

Constraints:
- Prefer ideas that can be piloted cheaply
- No heavy training
- Focus on publishable but practical ideas

Please:
1. expand this into 8-12 candidate ideas,
2. narrow to the strongest survivors,
3. run novelty checks,
4. propose top 2-3 pilot plans,
5. output an IDEA_REPORT-style result.
```

## 适合“只有粗略 seed”的 prompt

```text
Read AGENTS.md and follow the research idea funnel workflow.

I only have a rough seed, not a polished research question.

Rough seed:
Use structured memory to improve coding agents on long-horizon tasks.

What I loosely believe:
- agents forget why earlier decisions were made
- flat summaries are not enough
- memory should preserve decisions, failed attempts, and task decomposition

What I want from you:
- turn this into a proper research landscape
- generate 8-12 concrete candidate ideas
- remove weak or crowded ideas
- do claim-by-claim novelty checks
- identify top 2-3 ideas worth piloting
- for each top idea, give minimal experiment design and likely failure modes
- produce a final IDEA_REPORT-style output
```

## 适合“已经有半成品方向”的 prompt

```text
Read AGENTS.md and use the repository's research idea funnel workflow.

Topic:
Coding agents with memory

Rough idea:
Instead of storing one rolling summary, build a hierarchical memory with:
- task graph memory
- decision memory
- failure memory
- codebase landmark memory

Desired angle:
I want ideas that are more novel than generic "agent memory" papers.

Constraints:
- avoid ideas that need large-scale pretraining
- prefer ideas that can be validated with a small pilot
- target top-workshop / lower-tier conference feasibility first

Please:
- scan the recent landscape,
- derive 8-12 candidate ideas,
- score them for novelty / feasibility / upside,
- eliminate weak ones with explicit reasons,
- propose top 2-3 pilots,
- output the result in IDEA_REPORT format.
```

## 一个很实用的提示原则

不要只说：

```text
帮我从这个粗略 idea 生成研究想法
```

更好的写法是：

```text
这是我的 seed idea、我的直觉、我的约束、我不想碰的方向。
请按 AGENTS.md 里的 funnel workflow 自动展开、筛选、查新，并给出 top pilots。
```

这样 Codex 更容易真正走完整个 funnel，而不是随便脑暴一串点子。

## 可以直接复制测试的版本

```text
Read AGENTS.md and follow the research idea funnel workflow in this repository.

I have only a rough research seed.

Seed:
Agent memory for long-horizon coding tasks.

My intuition:
Current coding agents rely too much on flat summaries and lose the structure of decisions, failed attempts, and task decomposition.

Constraints:
- no heavy training
- cheap pilot preferred
- prioritize ideas with real novelty, not just prompt engineering variants

Please:
- build the recent research landscape,
- generate 8-12 candidate ideas,
- eliminate weak/crowded ones,
- perform novelty checks,
- propose top 2-3 pilots,
- output a final IDEA_REPORT-style result.
```

## Publishing Checklist

Before making the repo public:

1. Create a GitHub repository and push this directory.
2. Add a license file that matches how you want others to reuse the skill.
3. Verify the install command works against the public repo.
4. Restart Codex and test `$research-idea-funnel` once.
