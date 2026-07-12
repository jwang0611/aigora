# AIgora Autopilot: Automated Novel-Writing Pipeline（全自动小说流水线）

Autopilot mode turns AIgora's fiction pipeline into an automated system: the human writes a short
brief (or nothing at all), and the pipeline runs end-to-end—conception, outline, drafting,
blind critique, revision—gated by a quantified rubric, with the **EditorInChief** agent standing
in for the author at every checkpoint. Humans are pulled in only at defined escalation points.

**Triggers**: 自动写作, 全自动小说, autopilot, "write a novel autonomously"

## What Changes vs. Manual Fiction Mode

| | Manual mode | Autopilot mode |
|---|---|---|
| Gatekeeper checkpoints | Wait for the user | Answered by **EditorInChief** (`references/core/editor-in-chief.md`), decisions logged |
| Quality judgment | Vague final score | **Quality rubric gate** (`references/core/quality-rubric.md`): ≥48/60, no dimension <7, ≤3 revision rounds |
| Critique | Same-context agents | **Blind parallel reviewers** in fresh contexts (subagents) |
| Memory | Conversation context | **Project files on disk** (story bible, outline, continuity ledger) |
| Human involvement | Every stage transition | Only at escalation (see below) |

## The Pipeline

```
Stage 0  BRIEF        Human writes brief.md (or EditorInChief self-briefs from a one-line ask)
   ↓
Stage 1  CONCEPTION   Core 6 + conception agents discuss directions (main context)
   ↓                  ★ EditorInChief decides: story core, emotional target, ending direction
Stage 2  OUTLINE      Scene-by-scene structure, character arcs → outline.md, story-bible.md
   ↓                  ★ EditorInChief decides: structure, POV, key moments
Stage 3  DRAFTING     Chapter loop (below); continuity-ledger.md updated after every chapter
   ↓
Stage 4  CRITIQUE     3 blind reviewers score the full draft in parallel (fresh contexts)
   ↓                  ★ Rubric gate: PASS → Stage 5 / REVISE → targeted revision, re-score (≤3) /
   ↓                    ESCALATE → human
Stage 5  FINAL        Global consistency pass, final assessment, export to final/
```

### The Chapter Loop (Stage 3)

For each chapter:

1. **Draft** in the main context, drafting agents active (DialogueMaster, ScenePainter, Narrator,
   PaceMaster), with `story-bible.md` + `outline.md` + `continuity-ledger.md` loaded—**not** the
   full text of prior chapters. The ledger, not the context window, is the memory.
2. **Update the ledger**: every fact established (who knows what, dates, injuries, objects,
   promises made to the reader) is appended to `continuity-ledger.md`.
3. **Quick check** (cheap, same context): KnowledgeAuditor pass against the ledger.

Full blind critique happens once per draft (Stage 4), not per chapter—per-chapter blind review
burns tokens on prose that later chapters may force you to cut anyway. Exception: for works
longer than ~10 chapters, run an interim blind review at the midpoint.

## Project Directory Layout

Every novel lives in `projects/<yyyy-mm>-<slug>/`:

```
projects/2026-07-example/
├── brief.md               # The human's ask + any reserved decisions ("ask me before X")
├── conception.md          # Stage 1 discussion record
├── decisions.md           # EditorInChief's decision log (every checkpoint, with rationale)
├── story-bible.md         # World rules, characters, voice notes — stable reference
├── outline.md             # Scene-by-scene structure
├── continuity-ledger.md   # Running fact ledger, appended per chapter
├── chapters/              # Working drafts, one file per chapter
├── critiques/             # Raw blind-review reports, per round
├── scores.md              # Median score sheets, per round
└── final/                 # The finished novel + final assessment
```

Templates for these files are in `projects/_template/`.

## Blind Critique (Stage 4)

Run three reviewers **in parallel, in fresh contexts** (in Claude Code: three `Agent` calls in one
message; on claude.ai without subagents: three separate conversations, or at minimum three
strictly separated passes). Each receives only the draft + the rubric + its role card(s):

| Reviewer | Lens | Role cards to load |
|----------|------|--------------------|
| R1 Naive reader | Where did I feel something? Where did I skim? | `references/writing/firstreader.md` |
| R2 Hostile craft critic | AI-tells, prose flab, unearned emotion | `references/core/challenger.md`, `references/writing/aidetox.md`, `references/writing/prosepolisher.md` |
| R3 Structural analyst | Causality, continuity, knowledge violations | `references/writing/plotarchitect.md`, `references/writing/knowledgeauditor.md` |

Each reviewer returns: per-dimension scores with one-line justifications, plus a Must Fix /
Should Fix / Optional issue list. Median scores go to `scores.md`; the EditorInChief applies the
gate and picks revision targets.

**Why blind**: reviewers who watched the draft being written inherit its justifications. Fresh
contexts catch what the room can no longer see.

## Human Touchpoints（人工介入点）

The system asks for a human in exactly four cases—otherwise it never blocks:

1. **Escalation after 3 failed revision rounds** — human gets score history + diagnosis + options.
2. **Value-laden material** — content requiring the author's own moral/political judgment
   (see EditorInChief's escalation list).
3. **Reserved decisions** — anything the brief marks "ask me first."
4. **The brief itself** — optional; a one-line theme (or even "you pick") is a valid brief.

Recommended (not required) human review: read `decisions.md` and the final draft after delivery.
Everything is logged precisely so oversight can happen *after* the fact instead of blocking
*during* it.

## Running It

### In Claude Code (recommended — real parallel subagents)

```
用 AIgora Autopilot 写一篇小说。Brief：<主题/或"你来定">。
项目目录：projects/<slug>/。评审阶段用并行子代理盲评。
```

Claude Code will: read this file + the role cards, run Stages 0–3 in the main context, fan out
Stage 4 to three parallel subagents, loop revisions under the rubric gate, and commit artifacts.

### On claude.ai (skill upload, single context)

Same trigger phrase. Without subagents, the three blind reviews degrade to three *sequential,
role-isolated* passes—still scored against the rubric, still gated. Expect slightly softer
critique; consider pasting the draft into a fresh conversation for R2.

### Manual override at any time

Say "切换手动模式" / "switch to manual" and the Gatekeeper resumes waiting for you at checkpoints.
Say "继续自动" to hand the pen back to the EditorInChief.

## Failure Modes to Watch

- **Rubric gaming**: revisions that chase the weakest score by flattening voice. The gate's
  "no dimension < 7" plus the Originality dimension exist to catch this; the 3-round cap ends it.
- **Ledger drift**: skipping ledger updates "just this chapter" is how chapter 7 contradicts
  chapter 2. The chapter loop is not optional.
- **Committee prose**: applying every reviewer suggestion. The EditorInChief accepts and rejects;
  rejection reasons go in `decisions.md`.
