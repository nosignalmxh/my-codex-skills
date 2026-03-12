# IDEA_REPORT template

Use this as the default final structure. Keep it close to the original ARIS report style.

# Research Idea Report

**Direction**: [user direction]
**Assumptions**: [brief assumptions if user context was sparse]
**Generated**: [date]
**Ideas evaluated**: [X generated → Y survived filtering → Z piloted or planned → W recommended]
**Status**: [pre-pilot / pilot-informed]

## Landscape Summary

Write 3-5 paragraphs covering:

- the main lines of work in the last 2 years
- what the field rewards right now
- recurring limitations or open tensions
- saturation vs open space
- your confidence in coverage: sufficient / moderate / partial

## Recommended Ideas (ranked)

### Idea 1: [title]
- **One-line thesis**: [one sentence]
- **Hypothesis**: [what you expect and why]
- **Why this gap exists**: [what prior work missed]
- **Closest prior work**: [1-3 papers or work families]
- **Novelty**: [score]/10 — [proceed / proceed with caution / abandon]
- **Feasibility**: [compute, data, implementation estimate]
- **Minimum experiment**: [exact cheap test]
- **Pilot result or plan**: [signal if run, otherwise concrete plan]
- **Strongest reviewer objection**: [best skeptical attack]
- **Most likely failure mode**: [what breaks first]
- **Contribution type**: [empirical / method / theory / diagnostic / systems / benchmark]
- **Why do this now**: [why it is worth resources]

### Idea 2: [title]
[same structure]

### Idea 3: [title]
[same structure]

[Continue as needed for 4-6 survivors]

## Eliminated Ideas

| Idea | Kill reason |
|------|-------------|
| [idea] | already done by [paper] |
| [idea] | too much compute for first signal |
| [idea] | obvious combination / weak delta |
| [idea] | even success would not matter enough |

## Pilot Experiment Results or Pilot Plan

If pilots were run:

| Idea | Budget | Key metric | Signal | Notes |
|------|--------|------------|--------|-------|
| [idea] | [time/gpu] | [metric] | [strong positive / weak positive / null / negative] | [notes] |

If pilots were not run:

| Idea | Proposed benchmark | Baseline(s) | Budget | Positive signal threshold |
|------|--------------------|-------------|--------|---------------------------|
| [idea] | [dataset/task] | [baseline] | [time/gpu] | [criterion] |

## Suggested Execution Order

1. [first idea and why]
2. [second idea and why]
3. [third idea and why]

## Next Steps

- [ ] run the first pilot
- [ ] deepen novelty check on the riskiest survivor if needed
- [ ] turn the top idea into a concrete experiment backlog

## Style rules

- final language should be Chinese unless the user asked otherwise
- keep paper names and benchmark names in English
- separate facts from hypotheses
- preserve uncertainty instead of smoothing it over
