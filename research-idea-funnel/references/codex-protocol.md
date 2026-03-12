# Codex protocol v2

Use this file to make the Codex-only workflow behave more like the original ARIS split-role pipeline.

## Core principle

The original workflow uses one model to execute and another to criticize. In Codex-only mode, simulate that separation explicitly using multiple passes.

Whenever the environment allows model selection, prefer **GPT-5.4** with **xhigh reasoning** for all three passes.

## Pass 1. Generator

Purpose: divergent ideation grounded in the landscape survey.

Input should include:

- user direction
- constraints
- landscape map
- recurring limitations
- structural gaps

Prompt pattern:

"You are a senior ML researcher brainstorming publishable research ideas. Generate 8-12 concrete ideas. For each include short title, one-sentence summary, core hypothesis, minimum viable experiment, contribution type, risk, estimated effort, and why it is not merely apply-X-to-Y. Be creative but grounded."

## Pass 2. Skeptic

Purpose: attack each survivor like a harsh but useful reviewer.

Input should include:

- top surviving ideas
- quick novelty findings
- feasibility notes

Prompt pattern:

"Play devil's advocate on these ideas. For each idea, identify the strongest reviewer objection, hidden assumption, likely failure mode, novelty weakness, minimum experiment that would actually convince a skeptical reviewer, and whether the result would matter if positive or negative. Rank the ideas for actual research investment, not for beauty on paper."

## Pass 3. Chair

Purpose: reconcile enthusiasm and criticism.

Input should include:

- Generator output
- Skeptic output
- novelty report
- pilot plan or pilot results

Prompt pattern:

"You are acting as an area chair deciding which ideas deserve resources. Re-rank the ideas based on novelty, feasibility, cheap falsification path, reviewer appeal, and expected empirical signal. Preserve eliminated ideas and explain kill reasons. Output an IDEA_REPORT-style recommendation."

## Anti-self-delusion rules

To keep the three passes meaningfully separated:

- do not ask the Skeptic to merely critique the ranking; ask it to re-derive the objections from evidence
- do not let the Chair inherit the Generator ranking by default
- if the Skeptic finds a likely prior work collision, the Chair must either downgrade the idea or explicitly defend the delta
- when evidence is missing, raise risk instead of filling in with optimism

## When actual pilot execution is possible

If the environment truly has runnable code, data, and enough budget, the Chair should re-rank after pilot signals arrive.

Signal labels to use:

- strong positive
- weak positive
- null
- negative
- not run

Do not fabricate numbers. If there was no run, say `not run` and keep the report pre-pilot.
