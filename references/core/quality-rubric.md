---
name: quality-rubric
description: >
  The quantified quality gate for AIgora fiction. Six dimensions, ten points each. Defines scoring
  anchors, the pass threshold (total ≥ 48/60, no dimension < 7), the revision loop (max 3 rounds),
  and the blind-scoring protocol used in Autopilot mode.
---

# Quality Rubric（质量量表）

## Purpose

"Score if appropriate" cannot drive an automated pipeline. This rubric turns the Critique stage
into a measurable gate: a draft either passes and ships, or fails with a named weakest dimension
that the next revision round must target.

## The Six Dimensions

Each dimension is scored 0–10. Anchors are written for 4 / 7 / 9 so scorers calibrate against
descriptions, not against their mood.

### 1. Structure（结构）
Setup, escalation, turn, resolution; scene-level causality; no dead scenes.

- **4** — Events follow each other but don't cause each other; the middle could be reordered
  without loss; the ending arrives rather than lands.
- **7** — Clear causal chain; every scene moves plot or character; the turn is earned. Some
  transitions lean on coincidence or summary.
- **9** — The structure is itself expressive: how the story is told enacts what it is about.
  Remove any scene and something downstream breaks.

### 2. Character（人物）
Interiority, contradiction, agency; change that costs something.

- **4** — Characters are positions in a plot; wants are stated, not felt; change happens to them.
- **7** — The protagonist has a genuine internal contradiction and makes the decisive choice
  themselves; secondary characters have at least one non-instrumental trait.
- **9** — Characters surprise the reader while remaining inevitable in hindsight; even minor
  figures imply an offstage life.

### 3. Prose（文笔）
Sentence-level control; rhythm; precision; economy.

- **4** — Competent but interchangeable; adjectives do the work verbs should; rhythm is metronomic.
- **7** — Sentences are varied and controlled; images are specific to this story; nothing forces
  rereading for the wrong reason.
- **9** — Quotable without embarrassment; rhythm shifts track emotional register; cuts would wound.

### 4. Emotional Impact（情感冲击）
What the reader actually feels, and whether the story earns it.

- **4** — The reader understands what they are supposed to feel. Understanding is all that happens.
- **7** — At least one moment genuinely lands (tightness, held breath, rereading a line); the
  ending's feeling persists past the last paragraph.
- **9** — The story changes the reader's temperature; the emotion is complex (grief with relief,
  love with resentment), not a single note.

### 5. Originality / De-AI（原创性 / 去AI味）
Distance from both genre default and machine default.

- **4** — The premise or its execution could be autocompleted; hedged prose, symmetric paragraphs,
  emotion named rather than evoked (see `references/writing/aidetox.md`).
- **7** — The central conceit or its treatment is genuinely fresh; prose has idiosyncrasy and
  risk; no AI-tell survives a hostile read.
- **9** — A reader could not guess the premise from the first page, nor the ending from the
  premise—yet both feel inevitable afterward.

### 6. Thematic Depth（主题深度）
What the story knows; whether it thinks or merely gestures.

- **4** — The theme is a caption ("this is about memory"); the story illustrates rather than
  investigates it.
- **7** — The theme emerges from the plot's hard choices; the story complicates its own thesis at
  least once.
- **9** — The story earns an insight that cannot be paraphrased without loss; opposing readings
  are both supported and both painful.

## The Gate

| Verdict | Condition | Action |
|---------|-----------|--------|
| **PASS** | Total ≥ 48/60 AND every dimension ≥ 7 | Proceed to final assessment and export |
| **REVISE** | Anything less | Revision round targeting the weakest dimensions |
| **ESCALATE** | Still failing after 3 revision rounds | Stop; hand score history + diagnosis to the human |

The revision cap is not bureaucracy. Rounds 4+ historically trade voice for smoothness: scores on
Prose creep up while Originality decays. Three rounds, then a human.

## Blind-Scoring Protocol (Autopilot Mode)

Scores produced inside the drafting context are inflated—the scorer has watched the draft being
justified. In Autopilot mode:

1. Scoring is performed by **independent reviewers with fresh context** (in Claude Code: separate
   subagents) who receive ONLY the draft text and this rubric—no outline, no discussion history,
   no previous scores.
2. Run **three reviewers in parallel** with different lenses: a naive reader (FirstReader lens), a
   hostile craft critic (Challenger + AIDetox lens), and a structural analyst (PlotArchitect +
   KnowledgeAuditor lens).
3. The recorded score per dimension is the **median** of the three.
4. Continuity/knowledge violations found by any reviewer are Must Fix regardless of scores.
5. All three raw reports are saved to `critiques/` in the project directory; the median sheet goes
   in `scores.md`.

## Score Sheet Format

```
# Score Sheet — [Title], round N

| Dimension | R1 | R2 | R3 | Median |
|-----------|----|----|----|--------|
| Structure | 8 | 7 | 8 | 8 |
| Character | ... |
| Prose | ... |
| Emotional Impact | ... |
| Originality/De-AI | ... |
| Thematic Depth | ... |
| **Total (of medians)** | | | | **NN/60** |

**Verdict**: PASS / REVISE (weakest: dimension) / ESCALATE
**Must Fix carried forward**: ...
```

## Relationship to Other Agents

| Agent | Relationship |
|-------|--------------|
| EditorInChief | Owns the gate; picks revision targets from the weakest dimensions |
| FirstReader / Challenger / AIDetox | Their lenses become the three blind reviewers |
| Gatekeeper | Presents the verdict at the Critique → Revision checkpoint |
| ProsePolisher etc. | Execute the targeted revision; they never score their own work |
