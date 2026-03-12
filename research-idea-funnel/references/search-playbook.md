# Search playbook v2

Use this file for literature mapping, novelty checks, and feasibility-aware filtering.

## Source priority

Prefer sources in this order:

1. official papers and proceedings: arXiv, conference proceedings, journals, project pages
2. official repos when they clarify implementation or evaluation details
3. benchmark and survey papers
4. strong secondary summaries only to accelerate field mapping

Do not treat social posts as novelty evidence.

## Minimum coverage targets

For a standard idea-discovery run, try to identify:

- 10-15 papers directly relevant to the topic
- recent top-venue papers from the last 2 years
- preprints from the last 6 months when the area is fast-moving
- at least 2-5 neighboring or adjacent lines of work that could collapse a novelty claim

Coverage goal is not completeness. Coverage goal is to avoid obvious reinvention.

## Required query families

Use at least 5 distinct query formulations across these families.

### 1. Topic mapping

- "[topic] survey 2024 OR 2025 OR 2026"
- "recent advances in [topic]"
- "[topic] benchmark"
- "[topic] limitations"
- "[topic] future work"

### 2. Venue-focused search

- "[topic] NeurIPS OR ICML OR ICLR OR ACL OR EMNLP"
- "site:arxiv.org [topic] 2025"
- "site:openreview.net [topic] ICLR 2026"

### 3. Gap discovery

- "failure cases of [method family]"
- "robustness of [method family]"
- "cost latency memory tradeoff [method family]"
- "underexplored [topic]"
- "open problems in [topic]"

### 4. Novelty collapse search

- "[idea phrase]"
- "[task] with [mechanism]"
- "closest prior work [idea phrase]"
- "related work [mechanism] [task]"
- "ablation [mechanism] [task]"

### 5. Cross-domain transfer search

- "[mechanism] in [source subfield]"
- "[target subfield] with [mechanism]"
- "why not use [mechanism] for [target subfield]"

## Landscape map requirements

Before generating ideas, produce an internal landscape map with:

- sub-directions and representative papers
- dominant mechanisms or assumptions
- common datasets or benchmarks
- recurring limitations and future-work notes
- contradictions between papers
- signs of crowding or saturation
- under-tested assumptions and diagnostic gaps

## First-pass filtering protocol

For each generated idea, do three quick screens.

### Feasibility

Estimate:

- compute cost
- data availability
- implementation complexity
- dependency risk
- whether the first informative signal is achievable quickly

Kill ideas that require unavailable data or obviously excessive compute for the user's setup.

### Quick novelty

Do 2-3 targeted searches. Mark kill reasons such as:

- already done almost exactly
- too close to a known family of papers
- obvious combination with weak delta
- naming novelty only

### So-what test

Ask:

- if it works, does anyone care?
- if it fails, does anyone still learn something?
- would a reviewer call this incremental?

## Full novelty-check protocol

Apply this only to surviving ideas.

### Phase A. Extract key claims

For each idea, identify 3-5 claims that would need to be novel.

Typical claim types:

- the mechanism itself is new
- the problem framing is new
- the evaluation lens is new
- the finding is surprising or changes practice
- the systems tradeoff is not already well-known

### Phase B. Multi-query search per claim

For each claim:

- run at least 3 query formulations
- search both narrow terminology and adjacent terminology
- inspect recent 2024-2026 work when relevant
- find the closest papers, not just vaguely related papers

### Phase C. Delta analysis

For each closest paper, decide whether the difference is:

- structural
- procedural
- evaluative
- rhetorical only

If the delta is mostly rhetorical, novelty risk should be high.

### Phase D. Novelty report fields

For each idea, produce:

- core claims
- closest prior work table
- overall novelty score out of 10
- recommendation: proceed / proceed with caution / abandon
- suggested positioning if the idea is still worth doing

## Saturation signals

Be cautious when you see several of these:

- many near-identical titles or setups
- mature surveys already naming the obvious gaps
- benchmark gains shrinking to tiny increments
- industrial or systems papers already covering the practical angle

When saturation is high, narrow the framing rather than inventing another generic method.

## Pilot-planning rules

The top 2-3 ideas should each get a cheap pilot design.

Default target:

- 30 minutes to 2 hours on 1 GPU
- single seed
- smallest plausible dataset split or scale
- success threshold specified before execution

If no pilot can be designed cheaply, lower the idea's rank unless the user explicitly wants moonshots.

## Brutal honesty rules

- false novelty is worse than no novelty
- “apply X to Y” is usually weak
- if the method is not novel but the finding could be, say so
- if the idea is crowded but the evaluation angle is fresh, frame it that way instead of overselling method novelty
