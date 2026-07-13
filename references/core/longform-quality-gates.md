---
name: longform-quality-gates
description: >
  The authoritative gate ladder for AIgora long-form (LONGFORM pipeline) fiction: L0 per-chapter
  checks, L1 per-volume blind review, L2 book-level final review. Defines exhaustive reviewer
  packets, per-track lens tables, thresholds, quality debts, volume-lock, the editor's
  acceptance, and anti-degradation rules. Where numbers here differ from any other file, this
  file wins.
---

# Long-Form Quality Gates（长篇分级门控）

## Purpose

A 100万字 draft cannot be reviewed the way a short story is: the full text (~150万 tokens)
exceeds any single context, and a structural flaw discovered after a million characters costs
fourteen volumes to fix instead of one. The gate ladder moves quality control to where repair is
still cheap: **cheap checks per chapter, the real gate per volume, a digest-and-sampling review
for the assembled book.**

Applies to projects on the LONGFORM pipeline (see `/LONGFORM.md`). Short-form works keep the
single Stage-4 gate in `references/core/quality-rubric.md` unchanged.

## The Blindness Principle, Restated for Scale（品味盲评，账目明审）

The blind protocol exists so reviewers cannot inherit the draft's *justifications*. At volume
scale reviewers still need story-so-far context — so they receive the **reader-facing recap**
（读者向前情提要, `memory/reader-recap.md`）: only what a reader who binge-read the prior volumes
possesses. Events as experienced, character states as perceived, the open questions a reader is
consciously holding. No intent, no plans, no future events, no scores, no discussion history.

Everything that requires internal documents — promise schedules, budgets, ledgers — is checked by
**non-blind mechanical audits** run in parallel, whose findings enter the gate as Must Fix items.
Taste stays blind; bookkeeping doesn't need to be.

## L0 — Per-Chapter Check（章级检查）

Same drafting context, cheap, every chapter. Nothing scores, nothing escalates from L0; failures
are fixed immediately in-context.

1. **KnowledgeAuditor chapter-scope pass**: draft vs the active volume ledger + the cast's entity
   files + open promises (see `references/writing/knowledgeauditor.md`, Longform audit scopes).
2. **HookMaster checklist（网文轨 only, binary, no scoring）**:
   - Chapter ends on a true hook — paid or escalated within 3 chapters; no 狼来了 fake-outs.
   - Hook type not repeated more than 2 consecutive chapters（五型：悬念/危机/反转/期待/情感）.
   - ≥1 nameable 爽点 in every rolling 3-chapter window.
   - The chapter advances ≥1 registered thread.
3. **Burn-rate line**: append one line to the volume ledger — cumulative 字数 written vs plot
   milestones consumed (consumed by the EditorInChief's burn-rate check at the volume boundary).

## L1 — Per-Volume Blind Review（卷级盲评：真正的门）

Runs at every volume boundary, after the volume audit (V.AUDIT) confirms the ledger and the
reader-facing recap are accurate.

### Reviewer packet（穷举式——未列出即禁止）

Each of the three reviewers receives ONLY:

1. The full volume text (≤10万字 by the volume size cap; fits a fresh reviewer context).
2. The reader-facing recap（`memory/reader-recap.md`）.
3. The rubric sheets for the declared track: Core 4 + track module + V1/V2
   (literary: `quality-rubric.md`; webnovel: `webnovel-rubric.md`).
4. The role cards for its lens (table below).
5. **R2 only**: `book/style-anchor.md` — published, gate-passed text, hence reader-facing and
   blindness-safe. R2 explicitly scores drift-from-anchor as part of Prose.

**Prohibited from every packet**: volume outlines, master outline, continuity ledgers, the
promise registry, entity files, `decisions.md`, prior score sheets or critiques.

### Lens table by track

Role-card paths: `challenger.md` is in `references/core/`; all others in `references/writing/`.

| Reviewer | Literary track（文学轨） | Webnovel track（网文轨） |
|----------|--------------------------|--------------------------|
| R1 naive / serial reader | `firstreader.md` | `firstreader.md` + `hookmaster.md`（追更读者：晚上11点会不会点下一章？哪里会弃书？）|
| R2 hostile craft critic | `challenger.md` + `aidetox.md` + `prosepolisher.md` | `challenger.md` + `aidetox.md`（+ style anchor）|
| R3 structural analyst | `plotarchitect.md` + `knowledgeauditor.md` | `serialarchitect.md` + `knowledgeauditor.md` |

Each reviewer returns per-dimension scores with one-line justifications plus a Must Fix / Should
Fix / Optional list. Median-of-3 per dimension is recorded in the volume's `scores.md`.

### Parallel non-blind mechanical audits（同一门，独立产出）

- **SerialArchitect registry audit**: every promise due this volume paid or formally deferred
  (with a logged reason); character-arc milestones hit; escalation-ladder position matches the
  master outline; cast introduction/retirement rates within policy; burn-rate within band.
- **KnowledgeAuditor recap accuracy check**: the reader-facing recap against the volume text —a
  wrong recap poisons every future review, so the recap is itself gated.

Any registry, ledger, or recap violation is an **unconditional Must Fix**, regardless of scores.

### Gate conditions（L1）

| Verdict | Literary（8 dims / 80） | Webnovel（10 dims / 100） | Action |
|---------|--------------------------|----------------------------|--------|
| **PASS** | Median total ≥ 60 AND no dimension < 6 AND zero Must Fix | Median total ≥ 75 AND no dimension < 6 AND zero Must Fix | **Volume-lock（封卷）**; record quality debts; run V.COMPACT; proceed |
| **REVISE** | Anything less | Anything less | Targeted revision of weakest dimensions; re-score with fresh reviewers |
| **Cap** | Volume 1: 3 rounds. Volumes 2+: 2 rounds | Same | See over-cap handling |

- **Quality debts（质量债）**: any dimension passing at exactly 6 is recorded as a debt in
  `scores.md`. Max 2 debts per volume. The same dimension may not be in debt in two consecutive
  volumes (the second occurrence forces a fix before the volume can lock). Any dimension in debt
  in 3 volumes total triggers a mandatory targeted craft round during the **next** volume's
  drafting — feed-forward correction, never retro-polish.
- **Over-cap handling**: failing on a dimension floor (< 6) or on a Must Fix → **escalate to
  human**. Failing on total only, with total ≥ 72% of maximum → the EditorInChief may exercise a
  logged **editor's acceptance（主编验收）**, at most once per 3 volumes; otherwise escalate.
- **Golden-three-chapters gate（黄金三章门, Volume 1, 网文轨）**: R1 must explicitly answer
  "would a store-browsing reader click chapter 4?" — a No is a Must Fix regardless of scores.
- **Revision scope rule**: L1 revisions act only on the current volume's reports. Reviewer
  remarks about earlier volumes become notes to the EditorInChief — never auto-applied.

## L2 — Book-Level Final Review（书级终审）

Runs at book assembly (LONGFORM stage L3). The full text never enters one context. Three
components, then one gate:

### 1. Blind structural review

Three fresh reviewers each receive: the reader-facing recap chain for all volumes, the volume
gate history (verdicts only — no reports, no scores), and the book-level rubric module for the
declared track (B1–B6). They score the six book dimensions.

### 2. Stratified sampled deep reads

Each reviewer additionally receives a distinct, non-overlapping chapter sample scored on the
Core 4: fixed picks (chapters 1–3; the first and last chapter of every volume; the middle
chapter of the middle volume; the final 3 chapters) split across the three reviewers, plus 5
random chapters each. If late-book Core-4 medians fall more than 1.5 points below early-book
medians → **drift flag（漂移旗）** → targeted revision of the flagged region only.

### 3. Chunked consistency sweep（分卷链式扫描, non-blind, mechanical）

Sequential fresh-context KnowledgeAuditor passes, one volume per pass, each auditing volume k's
text against the cumulative memory snapshot through k (digests + entity files + timeline +
promise registry). Plus a VoiceDistinctor spot-check of one dialogue-heavy chapter per volume for
top-5-cast voice drift. All violations = Must Fix.

### Gate conditions（L2）

**PASS** requires ALL of:
- Book dimensions (median-of-3): total ≥ 48/60 AND every dimension ≥ 7.
- Zero sweep Must Fix outstanding.
- No unresolved drift flag.
- **Promise closure ≥ 95%**: registered promises paid, or abandoned with a logged EditorInChief
  decision; the webnovel track may mark ≤ 3 promises "deferred-to-sequel" with a logged rationale.

L2 revision is always **targeted** — named volumes/chapters, entering locked volumes only via the
Retro-Edit protocol (`/LONGFORM.md`). Max 2 rounds, then escalate to the human with the full
score history and the EditorInChief's diagnosis.

## Anti-Degradation Rules（抗劣化）

- **Why caps shrink at scale**: the short-form observation — round 4 trades voice for smoothness
  — compounds across 10+ volumes. What kills voice is total revision exposure, not per-round
  count. Hence 3 rounds for volume 1 (the storefront), 2 thereafter.
- **Volume-lock（封卷）**: on L1 PASS a volume locks. It reopens ONLY for (a) Must Fix continuity
  items surfaced by later L0/L1/L2, or (b) an EditorInChief-logged minimal-diff retcon required
  by a commissioned arc. Explicitly forbidden: reopening to chase scores, to harmonize style, or
  to apply later reviewers' taste to earlier volumes.
- **Ripple check（涟漪检查）**: every reopened edit gets a KnowledgeAuditor audit of the diff
  against the ledger and downstream digests; the touched volume's digest is regenerated; locked
  text is never re-scored.
- **Debts are paid forward**: quality debts are fixed in the next volume's drafting, never by
  polishing locked text.
- **Voice defenses**: R2 anchor comparison at every L1; mid-volume drift spot-check (chapter ~13
  of each volume, anchor + 2 recent excerpts only); L2 early/late sample delta; VoiceDistinctor
  sweep. Anchor re-baselining is EditorInChief-only, volume boundaries only, logged.

## Score Sheet Formats

Volume gate（`volumes/vM/scores.md`）:

```
# Score Sheet — [Title] vol M, round N（track: 文学/网文）

| Dimension | R1 | R2 | R3 | Median |
|-----------|----|----|----|--------|
| Core 4 rows ... |
| Track module rows ... |
| Volume Arc | ... |
| Serial Service | ... |
| **Total (of medians)** | | | | **NN/80 or NN/100** |

**Verdict**: PASS / REVISE (weakest: dimension) / ESCALATE
**Quality debts recorded**: <dimension @6, ...>
**Must Fix carried forward**: ...
**Mechanical audits**: registry PASS/FAIL, recap PASS/FAIL, burn-rate R=N.NN
```

Book gate: same shape over B1–B6 (/60) plus the sampled Core-4 tables, drift-flag status, sweep
findings, and promise-closure percentage.

## Relationship to Other Files

| File | Relationship |
|------|--------------|
| `/LONGFORM.md` | The pipeline this ladder gates; defines V.AUDIT, V.COMPACT, Retro-Edit, memory files |
| `quality-rubric.md` | Core 4 + literary module + literary level anchors |
| `webnovel-rubric.md` | Webnovel Core-4 recalibration + track module + webnovel level anchors |
| `editor-in-chief.md` | Owns every verdict; Scale Doctrine, burn-rate check, editor's acceptance |
| `serialarchitect.md` / `hookmaster.md` | The non-blind auditor / the L0 checklist owner |
