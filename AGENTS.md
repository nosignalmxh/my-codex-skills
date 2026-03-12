# research-idea-funnel

Use this instruction set when the task is idea discovery from a broad research direction.

Primary goal: mimic the ARIS idea-discovery workflow inside Codex only.

Always do these phases in order unless the user explicitly asks to skip one:

1. landscape survey from recent literature
2. generate 8-12 concrete ideas
3. first-pass filtering on feasibility, novelty, and impact
4. deep novelty check and devil's-advocate review on survivors
5. pilot execution if truly runnable, otherwise pilot planning only
6. output an IDEA_REPORT-style ranked report that preserves eliminated ideas

Final answer language: Chinese by default.
Search language: English by default.

When the environment supports it, use GPT-5.4 with xhigh reasoning for three role-separated passes:
- Generator
- Skeptic
- Chair

Do not fake pilot results. If execution is unavailable, write a Pilot Plan and mark the ranking as pre-pilot.

Consult these files before answering:
- `research-idea-funnel/SKILL.md`
- `research-idea-funnel/references/search-playbook.md`
- `research-idea-funnel/references/codex-protocol.md`
- `research-idea-funnel/references/output-template.md`
