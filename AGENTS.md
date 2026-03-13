# my-codex-skills

This repository is a multi-skill Codex pack for paper reading, reviewer-style auditing, paper-code alignment, survey reading, boundary planning, and broad research ideation.

When this repository is open in Codex:

1. Match the user request to the smallest relevant skill folder.
2. Read that skill's `SKILL.md` first.
3. Load only the reference files linked from that skill.
4. Default final-answer language is Chinese unless the user asks otherwise.
5. Mark unsupported statements as `【未知】` and inference as `【推断】`.

## Skill Routing

- `paper-deconstruct`
  Use for 论文组件化解构、单组件精讲、全文结构化拆解、组块库沉淀。

- `paper-review-audit`
  Use for 强批判审稿、分步红队、Claim-Evidence-Falsify 审计、共识与争议对比。

- `paper-code-alignment`
  Use for 结合代码读论文、repo scan、配置定位、训练脚本审计、复现路径检查。

- `survey-taxonomy-reader`
  Use for 阅读综述、taxonomy 抽取、统一符号表、代表方法对比、数学优先精读。

- `research-boundary-planner`
  Use for 找边界、从论文走到改进路线、消融计划、里程碑和写作骨架。

- `research-idea-funnel`
  Use for 从宽泛 research direction 出发，生成、筛选、查新并排序 ideas。

## Composition Rules

- Prefer one skill per task.
- Only combine skills when the user explicitly asks for a chained workflow.
- Safe chains:
  - `paper-deconstruct` -> `paper-review-audit`
  - `paper-deconstruct` -> `paper-code-alignment`
  - `paper-deconstruct` -> `research-boundary-planner`

## Tooling Notes

- For repo inspection, prefer `rg --files` and `rg`.
- For external literature comparison, rely on primary sources.
- Do not claim a paper-code match without direct file-level evidence.
