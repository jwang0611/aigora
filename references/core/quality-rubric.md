---
name: quality-rubric
description: >
  The quantified quality gate for AIgora fiction. A Core 4 of dimensions shared by all tracks,
  plus a Literary module (together: the classic six), ten points each. Defines scoring anchors,
  the short-form pass threshold (total ≥ 48/60, no dimension < 7), the revision loop (max 3
  rounds), the blind-scoring protocol, and the track declaration rules. The webnovel track module
  lives in `references/core/webnovel-rubric.md`; long-form (volume/book) gates live in
  `references/core/longform-quality-gates.md`.
---

# Quality Rubric（质量量表）

## Purpose

"Score if appropriate" cannot drive an automated pipeline. This rubric turns the Critique stage
into a measurable gate: a draft either passes and ships, or fails with a named weakest dimension
that the next revision round must target.

## Dimension Architecture: Core 4 + Track Module + Level Modules

Dimensions are organized in three layers so that two tracks（文学向 / 网文向）and multiple scales
(short story → 100万字 long-form) share one system:

- **Core 4** (all tracks, all scales): Structure, Character, Prose, Originality/De-AI.
- **Track module**: Literary（文学向）adds Emotional Impact + Thematic Depth — together with the
  Core 4 these are the classic six below, unchanged. Webnovel（网文向）adds 追读动力, 期待感,
  爽点节奏, 金手指与世界观, and recalibrates the Core 4 anchors —
  see `references/core/webnovel-rubric.md`.
- **Level modules** (long-form only): volume-level dimensions（卷结构、长线服务）scored at each
  volume gate, and book-level dimensions scored at final assembly. Literary-track anchors are in
  this file (below); webnovel-track anchors in `webnovel-rubric.md`. Gate mechanics are defined
  authoritatively in `references/core/longform-quality-gates.md`.

**For short-form literary work nothing changes**: six dimensions, total ≥ 48/60, every
dimension ≥ 7, max 3 revision rounds — exactly as before.

## Track Declaration（轨道声明）

- The track is declared in `brief.md`: `Track（轨道）: 文学向 / 网文向`.
- If the brief is silent, the EditorInChief infers the track from the ask and logs the inference
  in `decisions.md`.
- The track locks at Stage 0. A mid-book track change is a human escalation, never an
  EditorInChief decision.
- Reviewers load only their own track's rubric sheets. Webnovel dimensions are never scored on a
  literary work, and vice versa.

## The Core 4 Dimensions（literary anchors）

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

### 4. Originality / De-AI（原创性 / 去AI味）
Distance from both genre default and machine default.

- **4** — The premise or its execution could be autocompleted; hedged prose, symmetric paragraphs,
  emotion named rather than evoked (see `references/writing/aidetox.md`).
- **7** — The central conceit or its treatment is genuinely fresh; prose has idiosyncrasy and
  risk; no AI-tell survives a hostile read.
- **9** — A reader could not guess the premise from the first page, nor the ending from the
  premise—yet both feel inevitable afterward.

**Macro-scale note（过度确定 / over-closure）**: at volume/book scale the machine default is
not a bad sentence but perfect bookkeeping — every setup paid exactly, every symbol回收, every
account balanced, all chapters at one amplitude. "Nothing left open" is a defect of Originality
at scale, not a virtue of craft. (Counterweight mechanisms: `open-by-design` promise status;
the EditorInChief's Against Over-Closure mandate.)

## The Literary Module（文学模块）

### 5. Emotional Impact（情感冲击）
What the reader actually feels, and whether the story earns it.

- **4** — The reader understands what they are supposed to feel. Understanding is all that happens.
- **7** — At least one moment genuinely lands (tightness, held breath, rereading a line); the
  ending's feeling persists past the last paragraph.
- **9** — The story changes the reader's temperature; the emotion is complex (grief with relief,
  love with resentment), not a single note.

### 6. Thematic Depth（主题深度）
What the story knows; whether it thinks or merely gestures.

- **4** — The theme is a caption ("this is about memory"); the story illustrates rather than
  investigates it.
- **7** — The theme emerges from the plot's hard choices; the story complicates its own thesis at
  least once.
- **9** — The story earns an insight that cannot be paraphrased without loss; opposing readings
  are both supported and both painful.

## The Gate（short form）

| Verdict | Condition | Action |
|---------|-----------|--------|
| **PASS** | Total ≥ 48/60 AND every dimension ≥ 7 | Proceed to final assessment and export |
| **REVISE** | Anything less | Revision round targeting the weakest dimensions |
| **ESCALATE** | Still failing after 3 revision rounds | Stop; hand score history + diagnosis to the human |

The revision cap is not bureaucracy. Rounds 4+ historically trade voice for smoothness: scores on
Prose creep up while Originality decays. Three rounds, then a human.

**Long-form gates are different**: works on the LONGFORM pipeline are gated per volume and at
book assembly, with their own thresholds, revision caps, and quality-debt rules. Those gates are
defined authoritatively in `references/core/longform-quality-gates.md`; the tables there win over
anything implied here.

## Anti-Padding at Every Scale（反注水条款）

Anti-padding is per-scene, not per-book. At any target length every scene must earn its place; a
100万字 brief is met by more story — more arcs, more consequences — never by thinner prose.
Padding remains a scoring offense at every scale, and target scale is a brief constraint, not a
quality lever. (See the EditorInChief's Scale Doctrine: length is achieved in units of story
arcs, never sentences.)

## Long-Form Level Modules — Literary Track Anchors

Scored in addition to the Core 4 + Literary module at the gates defined in
`longform-quality-gates.md`. Webnovel-track anchors for the same dimensions are in
`webnovel-rubric.md`.

### Volume dimensions（卷级维度，scored at every volume gate）

**V1. Volume Arc（卷结构）**
- **4** — The volume is a pocket of chapters: no volume-level question, no turn; it ends wherever
  the chapter count ran out.
- **7** — The volume opens a volume-level question, turns in the middle, and closes with a climax
  that resolves it while leaving a book-level thread pulling forward; delete this volume and what
  follows breaks.
- **9** — The volume's arc meshes with the book's arc: its climax is simultaneously a step-change
  in the book-level stakes, and the volume's shape itself carries meaning.

**V2. Serial Service（长线服务）**
- **4** — An island volume: advances no book-level thread, plants nothing, or contradicts what
  came before.
- **7** — Advances at least one book-level thread, pays every promise that came due this volume,
  plants ≥2 setups for later volumes, zero contradictions with prior volumes.
- **9** — This volume rewrites the reader's understanding of earlier volumes (reread value); due
  promises are paid above expectation.

### Book dimensions（书级维度，scored at book assembly, 6 × 10）

**B1. Macro Structure（卷级结构）**
- **4** — Volumes could be reordered or deleted; the middle third sags; climaxes repeat at the
  same intensity.
- **7** — Every volume is load-bearing; volume climaxes escalate; no sagging middle; the whole is
  a single causal architecture.
- **9** — The book's macro shape is itself expressive; the sequence of volume arcs enacts the
  theme.

**B2. Promise Payoff（伏笔兑现）**
- **4** — Major setups forgotten or paid perfunctorily; the reader's held questions dissolve
  rather than resolve.
- **7** — ≥95% of registered promises paid or explicitly, consciously released; the major
  promises pay on schedule and in proportion to their buildup.
- **9** — Payoffs braid: late payoffs recontextualize early ones; in hindsight every plant looks
  inevitable, none looked like a plant.
- *Caveat: 9 rewards braiding, not total closure. Promises marked `open-by-design`（有意留白,
  EditorInChief-logged）count as consciously released; a ledger that balances to zero at every
  level is itself a machine tell (see the Originality macro-scale note).*

**B3. Character Continuity（人物长线）**
- **4** — Characters reset between volumes; growth is stated, then ignored; late-book behavior
  contradicts early-book psychology without cause.
- **7** — Arc milestones are hit; change is cumulative and each step costs something; no
  flanderization of the supporting cast.
- **9** — Ten volumes of change feel like one life: the person at the end contains every prior
  version, and the reader can feel the distance traveled.

**B4. Tension Curve（张力曲线）**
- **4** — Tension repeats one note at one amplitude; stakes inflate without deepening; the reader
  acclimatizes and stops feeling it.
- **7** — Tension deepens and complexifies across volumes rather than merely repeating louder;
  rest volumes are placed deliberately; the final movement is the book's true peak.
- **9** — The curve is felt in the body across a million characters: each escalation re-prices
  everything before it, and the quietest chapter late in the book carries more charge than the
  loudest chapter early.

**B5. Cast Management（阵容管理）**
- **4** — Characters accumulate without control; introductions blur; people vanish without
  explanation and return without memory.
- **7** — Introduction rate is controlled; exits are explicit; returning characters are
  remembered by text and reader alike.
- **9** — The cast breathes as a system: every named figure earns their page-time, and the social
  world feels larger than the pages shown.

**B6. Resolution（收束）**
- **4** — The ending resolves the last volume, not the book; the premise's oldest debts go
  unpaid.
- **7** — The ending pays the premise-debt of the whole book: the questions of volume one are
  answered by the person the protagonist became, and the feeling persists past the last page.
- **9** — The ending is both unguessable from the premise and, in hindsight, the only ending the
  book was ever paying for — at full million-character weight.
- *Caveat: full-weight resolution does not require closing every account at the same amplitude;
  an earned incompleteness is compatible with — often necessary for — a 9.*

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
4. Continuity/knowledge violations found by any reviewer enter the gate as **Must Fix** items
   regardless of scores — gate-blocking until resolved by EditorInChief adjudication (verified
   against the text, and against ground truth where checkable; applied, or 驳回'd with logged
   evidence), **never auto-applied**. Long-form semantics: `longform-quality-gates.md`, Must Fix
   semantics.
5. All three raw reports are saved to `critiques/` in the project directory; the median sheet goes
   in `scores.md`.

**Long-form variant**: at volume gates the "draft text" is the volume text plus the reader-facing
recap（读者向前情提要）— and nothing else; at book assembly it is digests + samples. The exact
reviewer packets, per-track lens tables, and thresholds are in `longform-quality-gates.md`.

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

Long-form volume sheets append the volume dimensions (and, on the webnovel track, replace the
Literary module with the webnovel module — sheet totals per `longform-quality-gates.md`).

## Relationship to Other Agents

| Agent | Relationship |
|-------|--------------|
| EditorInChief | Owns the gate; picks revision targets from the weakest dimensions |
| FirstReader / Challenger / AIDetox | Their lenses become the three blind reviewers |
| SerialArchitect / HookMaster | Long-form & webnovel lenses; see `longform-quality-gates.md` |
| Gatekeeper | Presents the verdict at the Critique → Revision checkpoint |
| ProsePolisher etc. | Execute the targeted revision; they never score their own work |
