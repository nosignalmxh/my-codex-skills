# my-codex-skills

这是一个可同步到 GitHub 的 Codex skill 仓库，当前包含 6 个技能包：

| Skill | 作用 |
| --- | --- |
| `paper-deconstruct` | 把论文拆成组件卡、依赖图、组块库和 Obsidian 结构化笔记 |
| `paper-review-audit` | 产出 reviewer 风格的 claim-evidence-falsify 审稿报告和红队审计 |
| `paper-code-alignment` | 结合代码仓库读论文，对齐模块、配置、训练脚本和复现路径 |
| `survey-taxonomy-reader` | 读取综述，生成 taxonomy、统一符号表和代表方法对比表 |
| `research-boundary-planner` | 从论文走到边界测试、改进路线、消融优先级和写作骨架 |
| `research-idea-funnel` | 从宽泛方向出发做 idea 生成、筛选、查新和 pilot 规划 |

## Repository Layout

```text
.
├── AGENTS.md
├── README.md
├── paper-code-alignment/
├── paper-deconstruct/
├── paper-review-audit/
├── research-boundary-planner/
├── research-idea-funnel/
└── survey-taxonomy-reader/
```

## Install One Skill Into Codex

发布到 GitHub 后，可以按 skill 路径单独安装。

示例：安装 `paper-deconstruct`

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo <github-user>/<repo> \
  --path paper-deconstruct
```

其他 skill 只需要替换 `--path`：

- `paper-review-audit`
- `paper-code-alignment`
- `survey-taxonomy-reader`
- `research-boundary-planner`
- `research-idea-funnel`

也可以直接给 GitHub tree URL：

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --url https://github.com/<github-user>/<repo>/tree/main/paper-review-audit
```

## Use In Codex

安装后可直接在 prompt 里显式调用：

- `Use $paper-deconstruct ...`
- `Use $paper-review-audit ...`
- `Use $paper-code-alignment ...`
- `Use $survey-taxonomy-reader ...`
- `Use $research-boundary-planner ...`
- `Use $research-idea-funnel ...`

## Notes

- 每个 skill 都是独立可安装目录，核心说明在 `SKILL.md`
- 模板和固定输出结构放在各自的 `references/`
- 仓库根目录的 `AGENTS.md` 只负责多 skill 路由，不替代具体 skill 内的工作流
