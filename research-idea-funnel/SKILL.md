---
name: research-idea-funnel
description: generate, filter, and rank research ideas from a broad direction using a codex-native idea funnel modeled on the aris idea-discovery workflow. use when the user wants literature mapping, 8-12 candidate ideas, feasibility and novelty filtering, devil's-advocate review, optional pilot planning or pilot execution, and an idea_report-style output that preserves both recommended and eliminated ideas.
---

# Research Idea Funnel v2

## Overview

Use this skill when the user gives a research direction rather than a finished idea and wants a workflow that behaves like the original ARIS idea-discovery pipeline. The target behavior is:

1. map the landscape from recent literature
2. brainstorm 8-12 concrete ideas
3. filter aggressively on feasibility, novelty, and impact
4. run deep novelty checks and devil's-advocate review on survivors
5. design cheap pilot experiments for the top 2-3 ideas, and execute pilots only if a runnable environment is actually available
6. output an `IDEA_REPORT`-style ranked report that keeps both winners and dead ends

Write the final answer in Chinese unless the user asks otherwise. Search in English unless the source is naturally in another language.

## Codex-only adaptation

The original ARIS workflow separates roles across Claude Code and Codex MCP. This skill deliberately removes that split and uses Codex only.

To stay close to the spirit of the original workflow, simulate three explicit passes with **GPT-5.4 at xhigh reasoning** whenever the host environment exposes that choice:

- **Generator pass**: generate and expand candidate ideas
- **Skeptic pass**: attack novelty, feasibility, and reviewer appeal
- **Chair pass**: reconcile evidence and produce the final ranking

Do not let one pass merely rubber-stamp the prior pass. Re-state the evidence and force each pass to justify its conclusions from the literature and constraints.

If the environment does not expose explicit model selection, still follow the same role-separated procedure and state that the workflow is **Codex-only, single-model simulated multi-pass**.

Consult `references/codex-protocol.md` for the exact pass structure and prompt patterns.

## Inputs to accept

Normalize any of the following into one working brief:

- a research direction or problem area
- optional keywords
- optional paper titles or links
- optional repo links
- optional notes on compute budget, data access, timeline, target venue, preference for methods vs findings, or whether pilot execution is allowed

If the user gives very little context, proceed with these defaults:

- venue target: workshop to mid-tier conference unless the user says top-tier
- compute target: moderate, roughly up to 8x 3090-class GPUs or a small cloud budget
- data target: public data preferred
- validation target: at least one cheap falsification experiment per top idea

State these assumptions briefly before proceeding.

## Workflow

Follow this sequence.

### Phase 1. Landscape survey

Map the area before inventing ideas.

Use `references/search-playbook.md` for concrete query tactics.

Minimum expectations:

- search the last 2 years of top venues in the relevant area
- search the last 6 months of arXiv or equivalent preprint sources
- use at least 5 distinct query formulations
- read abstracts and introductions for the top 10-15 papers when possible
- build a compact landscape map organized by sub-direction, mechanism, or evaluation style
- extract recurring limitations, future-work suggestions, contradictory findings, and untested assumptions

Explicitly note:

- what has been tried repeatedly
- what is crowded or saturated
- what structural gaps remain
- what kinds of results reviewers in this area seem to reward

Do not claim coverage is exhaustive. Mark the coverage as sufficient, moderate, or partial.

### Phase 2. Divergent idea generation

Run a **Generator pass** using GPT-5.4 xhigh.

Generate **8-12 concrete ideas**. For each idea, capture:

1. short title
2. one-sentence summary
3. core hypothesis
4. minimum viable experiment
5. expected contribution type: empirical finding / method / theory / diagnostic / benchmark / systems
6. risk level: low / medium / high
7. estimated effort: days / weeks / months
8. why this is not merely “apply X to Y”

Bias toward ideas that are:

- testable with moderate compute
- likely to produce a meaningful positive or negative result
- differentiated from the 10-15 papers in the survey
- sharp enough to be killed quickly if wrong

Quantity first, quality second. Do not collapse to only 3 ideas in this phase.

### Phase 3. First-pass filtering

Filter ruthlessly. The default target is to reduce **8-12 ideas to 4-6 survivors**.

For each idea, perform three quick screens:

1. **Feasibility screen**
   - estimate compute, data, implementation complexity, and dependency risk
   - eliminate ideas that obviously require unavailable data or impractical resources for the user's stated setup
   - by default, eliminate ideas likely to require more than about a week of uninterrupted GPU time before yielding any signal

2. **Quick novelty screen**
   - do 2-3 targeted searches per idea
   - check whether the idea is already done, is an obvious combination, or is crowded by near-duplicates
   - do not do the full novelty protocol yet; save that for survivors

3. **So-what screen**
   - if the idea succeeds, does it change how people think or build systems?
   - if the idea fails, is the negative result still worth learning?

Keep an explicit eliminated-ideas table with the kill reason.

### Phase 4. Deep validation on survivors

For each surviving idea, run two stronger checks.

#### 4A. Full novelty check

Use the procedure in `references/search-playbook.md` and mirror the original ARIS novelty-check discipline:

- extract **3-5 core claims** per idea
- for each claim, run at least **3 query formulations**
- explicitly inspect recent work from 2024-2026 when relevant
- identify the **closest prior work** and the exact delta
- decide whether the difference is structural, procedural, evaluative, or merely rhetorical
- assign a **novelty score out of 10** and a **recommendation**: proceed / proceed with caution / abandon

Be brutally honest. False novelty claims waste the most time.

#### 4B. Devil's-advocate review

Run a **Skeptic pass** using GPT-5.4 xhigh. For each surviving idea, force answers to:

- what is the strongest reviewer objection?
- what hidden assumption is most likely to break the idea?
- what is the minimum experiment that would actually satisfy a skeptical reviewer?
- what result would falsify the idea quickly?
- is this publishable for a good reason, or merely interesting?

After that, run a **Chair pass** using GPT-5.4 xhigh to reconcile:

- your own ranking
- the Generator pass enthusiasm
- the novelty evidence
- the Skeptic pass objections

Select the top 2-3 ideas for pilot planning or pilot execution.

### Phase 5. Pilot experiments or pilot plans

This phase should stay close to the original workflow, but never fake execution.

For each top 2-3 idea:

1. define the cheapest pilot that could produce positive or negative signal
2. target 30 minutes to 2 hours on 1 GPU when execution is available
3. define the success metric before the run
4. define what counts as null, weak positive, strong positive, or negative signal

Then choose one of two modes.

#### Mode A. Pilot execution allowed and actually runnable

Only execute pilots if all of these are true:

- the user explicitly wants execution or has provided code/data context
- the environment can really run the pilot
- the experiment is cheap enough to be reasonable in the current session

If you execute, keep the pilots small and parallelizable. Re-rank the top ideas using the empirical signal.

#### Mode B. No runnable environment or execution not requested

Do **not** pretend pilots were run.

Instead produce a **Pilot Plan** with:

- exact minimal experiment for each top idea
- dataset or benchmark
- baseline(s)
- metric(s)
- time budget
- decision threshold for positive signal

Mark the final ranking as **pre-pilot** if no actual pilot result exists.

### Phase 6. Output an IDEA_REPORT-style final answer

Use `references/output-template.md`.

The report must always include:

- direction and assumptions
- ideas evaluated counts: X generated → Y survived → Z piloted or planned → W recommended
- landscape summary
- recommended ideas ranked
- eliminated ideas with kill reasons
- pilot experiment results **or** pilot plan
- suggested execution order
- next steps

Keep paper titles, benchmark names, and method names in English when needed.

## Decision rules

Follow these rules strictly.

- The user gives a **direction**, not a final thesis. Your job is to generate the ideas.
- Quantity first, then ruthless filtering.
- A good negative result can be publishable. Prefer ideas where either outcome teaches something important.
- Always estimate compute and data requirements.
- “Apply X to Y” is usually weak unless the application reveals non-obvious structure or surprising findings.
- Preserve dead ends in the report. Eliminated ideas are part of the value.
- If coverage is partial, say so. If novelty is uncertain, raise the risk level.
- If the direction is badly underspecified, narrow it yourself once, state assumptions, and continue.
- Never write fake pilot numbers.
- Never claim novelty without naming the closest prior work.

## Default deliverable style

Unless the user asks for something else, keep the answer concise but decision-oriented.

The default outcome is a Chinese report with:

- a 3-5 paragraph landscape summary
- 4-6 deeply validated survivors, with the top 2-3 emphasized
- explicit novelty and feasibility judgments
- a dead-ends table
- a pilot plan or pilot result section
- one concrete recommendation for what to prototype first

## Resources

- `references/search-playbook.md`: search tactics, novelty protocol, saturation signals, and feasibility checks
- `references/codex-protocol.md`: how to simulate the original multi-role behavior inside Codex using GPT-5.4 xhigh
- `references/output-template.md`: IDEA_REPORT-style structure for the final answer

If this repository is opened directly in Codex app rather than installed as a standalone skill, the root `AGENTS.md` provides a shorter project-level entrypoint.
