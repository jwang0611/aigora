# AIgora Longform: Million-Character Novel Pipeline（百万字长篇流水线）

Longform mode extends Autopilot to webnovel-scale works — 100万字 and beyond — delivered as a
complete book. **It inherits `AUTOPILOT.md`; the sections below override it; everything not
mentioned here works exactly as in Autopilot.** Both tracks are supported: 文学向 and 网文向
(declared in the brief; see `references/core/quality-rubric.md`, Track Declaration).

**Triggers**: 长篇, 百万字, 网文长篇, 写长篇小说, long-form novel, webnovel, million-character
novel. Also: any work longer than ~30 chapters or ~5万字 must run on this pipeline.

## What Changes vs. Autopilot

| | Autopilot (short form) | Longform |
|---|---|---|
| Unit of everything | The draft | **The volume（卷）** — outlining, gating, blind review, ledger scope, compaction, git tags. Chapters are the drafting/commit unit; the book is only the delivery unit |
| Outline | Full scene-by-scene up front | **Progressive elaboration**: master outline at conception; each volume's outline written just-in-time |
| Memory | One continuity ledger | **Tiered memory with hard size caps** and a compaction protocol at every volume boundary |
| Critique | One blind review per draft | **Gate ladder** L0 (chapter) / L1 (volume) / L2 (book) — `references/core/longform-quality-gates.md` (authoritative) |
| Length policy | Natural length gated by quality | **Target scale is a hard brief constraint**; length is achieved in story arcs, never padding — EditorInChief's Scale Doctrine |
| Sessions | One sitting | **Resumable**: `progress.md` + git conventions make any fresh session continue deterministically |

Scale defaults: ~3,000字/章; 22–28 章/卷 (≈7–8.5万字, **hard cap 10万字/卷**); 12–14 卷 →
300+ chapters, 100万+字.

These norms are defaults for full-scale briefs. A brief may declare a smaller **pilot scale**
(e.g. 5万字/2卷 流程测试); the EditorInChief proportionally shrinks the 章/卷 norms and the
burn-rate baseline (logged in `decisions.md`). Gate mechanics, thresholds, and revision caps
never shrink with scale.

## Why This Architecture: The Token Budget（架构依据）

Conversion: 1 汉字 ≈ 1.5 tokens.

- **Full book**: 100万字 ≈ 1.5M tokens — exceeds any single context. Book-level review MUST be
  digest + sampling. This is a physical constraint, not a style choice.
- **Volume blind review**: a 7.5万字 volume ≈ 112k tokens + rubric ~3k + role cards ~4k + report
  headroom ~5k ≈ **~125k — fits a 200k context with 37% margin**. At the 10万字 cap: ≈157k,
  still fits — hence the cap. The volume is the largest reviewable unit.
- **Per-chapter drafting context** (constant regardless of book progress): the loading manifest
  below totals **~40,000字 ≈ 60k tokens** of input; with role cards and output, ~75k per chapter
  turn — chapter 312 costs the same as chapter 12.
- **Whole book, order of magnitude**: ~334 chapters × ~65k ≈ 22M input tokens drafting; 14
  volumes × 3 reviewers × 125k ≈ 5M review; plus revision rounds → **~30–40M tokens/book**.
  Consequences: never blind-review per chapter; load the stable pack (bible / style anchor /
  master outline) first for prompt-cache reuse; volume gates catch problems while the repair
  cost is 1 volume, not 14.
- **Book assembly review**: 14 digests (~53k) + registry/entities/timeline (~15k) + ~18 sampled
  chapters (~81k) ≈ **~150k — fits**. The full-text alternative is 10× over budget.

## The Pipeline

```
L0 BRIEF          brief.md with Track（文学向/网文向）and Target scale（e.g. 100万字/12卷 —
   ↓              hard constraint; "以上" suffix defines overshoot tolerance）
L1 CONCEPTION     Conception round → book/master-outline.md
   ↓              ★ EditorInChief locks: Core (premise, protagonist arc endpoint, ending
   ↓                direction), the volume map (1 paragraph + word budget + plot milestones per
   ↓                volume), 3–7 book-spine PROMISEs. Rows for volumes ≥3 marked PROVISIONAL
L2 VOLUME LOOP    for M = 1..K:
   V.OUTLINE        Just-in-time: depends-on digests + bible + master outline
   ↓                → volumes/vM/outline.md
   ↓                ★ EditorInChief locks vol-M outline; may amend PROVISIONAL rows (logged);
   ↓                  Core amendments only here (logged; ending-direction change → escalate);
   ↓                  runs the burn-rate check (Scale Doctrine)
   V.DRAFT          Chapter loop (serial default; sanctioned parallel variant — see Drafting
   ↓                Modes): draft per the loading manifest → update ledger → L0 check →
   ↓                update recap → update progress → git commit. Vol 1: EditorInChief drafts
   ↓                ch001 in the main context as the voice seed. Voice spot-check at ch ~13
   V.AUDIT          Seam audit first if any chapter was parallel-drafted; then fresh-context
   ↓                KnowledgeAuditor: full volume text vs volume ledger + entity files +
   ↓                timeline; verifies ledger completeness and reader-recap accuracy; computes
   ↓                burn-rate R from actual chapter word counts vs the volume's milestones
   V.REVIEW         L1 volume blind review (3 parallel fresh reviewers) + non-blind mechanical
   ↓                audits. Vol 1: ≤3 revision rounds; vols 2+: ≤2. Gates: longform-quality-gates.md
   V.COMPACT        Compaction protocol (below) ★ EditorInChief signs off; volume-lock（封卷）;
   ↓                git tag vM-compacted
L3 BOOK ASSEMBLY  L2 book review (blind structural + stratified samples + chunked sweep) +
   ↓              cross-volume promise closure + voice drift check. Must Fixes may target ANY
   ↓              volume → Retro-Edit protocol (below)
L4 EXPORT         Concatenate volumes → final/<title>.md (+ per-卷 files); final assessment
```

**Locking rules**: the **Core** locks at L1 CONCEPTION, amendable only at volume boundaries by
the EditorInChief (ending-direction changes escalate). A **volume outline** locks at V.OUTLINE;
in-volume beat deviations are allowed unless they change the volume's exit state (then
EditorInChief sign-off + an outline amendment note). A **compacted volume** is cold: retro-edits
only via the Retro-Edit protocol.

## Tiered Memory（分层记忆）

| Tier | Contents | Loading |
|------|----------|---------|
| **T0 stable** | story-bible, book/style-anchor, master-outline Core | Every drafting context, loaded first (prompt cache) |
| **T1 hot** | active volume outline + ledger, memory/recap, promise-registry `## Open` section, progress | Every drafting context |
| **T2 warm** | entity files, timeline, volume digests | Selectively, per the manifest rules |
| **T3 cold** | archived volume ledgers, prior chapter texts, critiques | **Never loaded**; consulted only by targeted single-file reads during audits |

### The Loading Manifest — drafting chapter N of volume M, load exactly this, nothing else

| Item | Size cap | ~Tokens |
|------|----------|---------|
| `progress.md` | 600字 | 1k |
| `story-bible.md` | 4,000字 | 6k |
| `book/style-anchor.md` | 1,500字 | 2k |
| `book/master-outline.md` — Core + promise spine + volume rows M−1/M/M+1 only | 2,000字 | 3k |
| `volumes/vM/outline.md` | 5,000字 | 8k |
| `volumes/vM/ledger.md` (worst case, volume end) | 10,000字 | 15k |
| `memory/promise-registry.md` — `## Open` section + current-volume milestone rows | 1,500字 | 2.5k |
| `memory/recap.md` | 1,000字 | 1.5k |
| Chapter N−1 full text | 3,000字 | 4.5k |
| Entity files for this chapter's cast (≤5 × 800字) | 4,000字 | 6k |
| Depends-on volume digests (≤3 × 2,500字) | 7,500字 | 11k |
| **Total** | **~40,000字** | **~60k** |

Selection rules: entity files come from the `cast:` field that every beat line in the volume
outline must carry; digests come from the `depends-on:` header of the volume outline (set by the
EditorInChief at V.OUTLINE, ≤3).

**NEVER load while drafting**: prior chapters other than N−1; archived ledgers; other volumes'
outlines; paid promises; raw critique reports. If a fact from a cold volume is needed and isn't
in the digests/entities/timeline, that's a compaction bug — fix the memory files, don't load the
cold source into drafting.

Every cap above has a named compaction rule (below, or the file's own template). **A hot file
over its cap blocks the next chapter until compacted.**

## Drafting Modes: Serial and Parallel（串行与并行起草）

**Serial is the default.** Ledger-as-memory guarantees continuity only when chapter N loads
chapter N−1's final text plus the up-to-date ledger. Field-tested consequence of skipping this:
non-monotonic water levels, contradictory retellings of the same departure, dropped chapter-end
cliffhangers — caught only by the blind-review safety net, which is salvage, not a guarantee.

**Parallel drafting is a sanctioned variant** (EditorInChief-logged per volume in
`decisions.md`). It trades drafting latency for a mandatory audit pass and residual seam risk.
Conditions — all four, or parallel is forbidden for that volume:

1. **Beat contracts**: the volume outline carries per-beat `entry:`/`exit:` physical-state
   contracts（时辰/倒计时、地点、在场者、关键物理量如水位、关键道具持有）plus a volume-level
   **单调量声明** (quantities that may only rise or only fall across the volume). No contracts,
   no parallel.
2. **Manifest delta**: each parallel drafter replaces the "Chapter N−1 full text" manifest row
   with its own beat's contracts + both adjacent beats' contracts (already inside `outline.md`).
   Everything else loads unchanged. Vol 1 only: ch001's full text (the voice seed) loads in the
   style-anchor slot until the anchor exists.
3. **Ledger merge**: each drafter returns chapter text + that chapter's ledger lines; the main
   context merges the lines in chapter order, then runs the L0 check per chapter post-merge.
   Commits stay one-per-chapter, in order.
4. **Seam audit** (below) runs before V.AUDIT, mandatorily.

### The Seam Audit（接缝审计）

Mandatory whenever ANY chapter was drafted without loading its predecessor's final text. Run by
KnowledgeAuditor (main context or a fresh subagent) over the assembled volume + the outline's
beat contracts; findings are fixed in-context before V.AUDIT. Four checks:

1. **Entry/exit alignment**: every chapter's opening state matches the previous chapter's
   closing state, and both match the beat contracts.
2. **Monotonic quantities**: every declared 单调量 (water levels, countdowns, dates) never
   regresses across the chapter sequence.
3. **Repeated-event consistency**: any event narrated or referenced in ≥2 chapters (departures,
   handovers, deaths) agrees on its facts — vehicle, time, participants, objects.
4. **Hooks resolve-or-carry**: every chapter-end hook is either resolved or explicitly picked up
   by the next chapter; no dropped cliffhangers.

## The Compaction Protocol（V.COMPACT — run when volume M passes its gate）

Executed by the EditorInChief + KnowledgeAuditor, in order:

1. **Write `memory/digests/vol-M-digest.md`** (hard cap 2,500字): chapter-cluster plot summary;
   exit state (where/when/who-knows-what); character deltas; new world rules; hooks planted for
   later volumes; one line — "what this volume did for the book."
2. **Ledger triage** — every line of `volumes/vM/ledger.md` gets exactly one disposition: unpaid
   `PROMISE:` → `memory/promise-registry.md` with a `[vM chNNN]` origin tag; still-load-bearing
   facts (per master-outline forward references) → the relevant entity file or timeline; live
   `KNOWS:` states → entity files; everything else stays in place.
3. **Mark the ledger archived**: prepend the ARCHIVED header (never load; future facts live in
   digest/entities/registry; retro-edit amendments go in its Amendments section — the same
   amendment pattern proven in `projects/2026-07-slow-room/continuity-ledger.md`).
4. **Update entity files**: append an `## End of vol M` state block (location, physical state,
   knowledge, relationships, open wants). Over 800字 → merge the oldest volume blocks into one
   "through vol X" block.
5. **Update `memory/timeline.md`**: one line per chapter-cluster, with in-story dates.
6. **Rewrite `memory/reader-recap.md`** (≤8,000字, rolling compression): as for a reader who
   binge-read volumes 1..M — events as experienced, character states as perceived, the "读者悬而
   未决的问题" list. Strip rule: no intent, no plans, no future events, no scores, no discussion
   history. Rolling compression reuses prior recap text — verify every fact a revision or
   retro-edit changed against the final text, never against the previous recap.
7. **Conservation + cap check** (KnowledgeAuditor): unpaid-promise count in the archived ledger
   == newly added registry entries; every entity appearing in ≥3 chapters of vol M has an entity
   file; **and a blocking cap audit — measure (never eyeball; `wc -m`) every memory file against
   its cap: digest ≤2,500字, style-anchor ≤1,500字, reader-recap ≤8,000字, recap ≤1,000字,
   entity ≤800字 each, progress ≤600字. Any over-cap file is compressed before compaction signs
   off — step 8 is blocked until this audit is green.** (Field data: without the mechanical
   check, the first live run shipped digests at 2× their cap.)
8. EditorInChief logs the compaction in `decisions.md`; commit + tag `vM-compacted`.

Paid promises are marked ✓ and moved to the registry's `## Paid` section (never loaded during
drafting).

## Resumability（断点续写）

`progress.md` (cap 600字) is **overwritten as the final step of every atomic action**. A fresh
session reads it FIRST, then loads the manifest for the stated next action — that pair makes
resume deterministic. Contents:

```
# Progress — <题名>
**Mode**: LONGFORM autopilot   **Track**: 网文向
**Stage**: L2 V.DRAFT (vol 07, next: ch 163)
**Last completed**: ch162 drafted+ledgered+recapped (commit <sha>)
**Next action**: draft ch163 per volumes/v07/outline.md beat 12
**Volume states**: v01–v06 COMPACTED | v07 DRAFTING 12/25 | v08+ UNOUTLINED
**Open Must Fixes**: MF-09 (from v06 L1) ...
**Pending escalations / reserved decisions**: none
**Gate history**: v01 PASS r1 | ... | v06 PASS r2
```

**Git conventions**: one commit per chapter (chapter file + ledger + recap + progress:
`vol07-ch163: draft 章名`); tags `vM-outline-locked`, `vM-draft-complete`, `vM-gate-pass`,
`vM-compacted`. Retro-edits commit as `retro(v03-ch054): reason [MF-12]`.

Tags are **best-effort**: some remotes reject tag pushes. A failed tag push is logged and
skipped — never retried in a loop, never blocks the pipeline. The authoritative gate history is
`progress.md` (the Gate history line) + `decisions.md`; tags are a convenience index only.

## Retro-Edit Protocol（回溯修订）

Editing a locked (compacted) volume is allowed only against (a) a recorded Must Fix or (b) an
EditorInChief-logged minimal-diff retcon required by a commissioned arc. Every retro-edit commit
MUST update, in the same commit, all four of:

1. the archived ledger's **Amendments** section,
2. the volume's **digest**,
3. every affected **entity file**,
4. **`memory/reader-recap.md`** — whenever the edit changes any reader-visible fact. The recap
   is fed to every downstream blind reviewer; one stale value poisons every future review
   (field case: a date fixed in locked text survived in the recap and generated a false
   contradiction report one volume later). If no reader-visible fact changed, note
   `recap: no impact` in the commit message.

This quadruple-update（四联更新）is what keeps memory truthful after edits to cold volumes.
KnowledgeAuditor then runs the ripple check (diff vs ledger + downstream digests +
reader-recap). Locked text is never re-scored.

## Voice-Drift Control（声纹漂移控制）

- **`book/style-anchor.md`** (cap 1,500字): three canonical passages (~300–500字 each — one
  narration, one dialogue, one scene/action) selected by the EditorInChief from gate-passed
  volume-1 chapters, plus the bible's "things this story never does" list and 3 named AI-tells
  this book is prone to. Loaded in every drafting context. Re-baselined only by the
  EditorInChief, only at volume boundaries, logged.
- **Hooks**: R2 scores drift-from-anchor at every L1; mid-volume spot-check at chapter ~13
  (fresh subagent, anchor + 2 recent excerpts only — a FAIL inserts a targeted style pass before
  the volume continues); L2 early/late sample delta + VoiceDistinctor sweep.

## Project Directory Layout

Templates in `projects/_template/longform/`. Every longform novel lives in
`projects/<yyyy-mm>-<slug>/`:

```
projects/2027-01-example/
├── brief.md                   # Ask + Track + Target scale + reserved decisions
├── conception.md              # L1 discussion record
├── decisions.md               # EditorInChief decision log
├── progress.md                # Resume manifest — overwritten every atomic action
├── story-bible.md             # Stable reference (cap 4,000字)
├── book/
│   ├── master-outline.md      # Core + promise spine + volume map (budgets, milestones,
│   │                          #   LOCKED|PROVISIONAL status per row)
│   └── style-anchor.md        # Voice anchor (cap 1,500字)
├── memory/
│   ├── entities/              # char-<名>.md, faction-<名>.md, loc-<名>.md (cap 800字 each)
│   ├── promise-registry.md    # Four tables: promises / arc milestones / escalation ladder /
│   │                          #   motif ledger. Drafting loads ## Open only
│   ├── timeline.md            # One line per chapter-cluster, in-story dates
│   ├── recap.md               # Drafting recap — rolling, overwritten per chapter (cap 1,000字)
│   ├── reader-recap.md        # Reader-facing 前情提要 for reviewers (≤8,000字)
│   └── digests/               # vol-01-digest.md ... (cap 2,500字 each)
├── volumes/
│   └── v01-<卷名slug>/
│       ├── outline.md         # Volume arc, entry/exit state, depends-on:, beats with cast:
│       ├── ledger.md          # Volume-scoped; ARCHIVED + Amendments after compaction
│       ├── scores.md          # L1 sheets, quality debts
│       ├── critiques/         # Raw blind reports per round
│       └── chapters/          # 001-<题名>.md ... (GLOBAL chapter numbering)
└── final/                     # Assembled book (<title>.md, per-卷 files), blind book
                               #   reviews (L2-review-R1.md .. R3.md), final-assessment.md
```

## Quality Gates

The gate ladder — L0 per-chapter, L1 per-volume, L2 book-level — with reviewer packets, lens
tables, thresholds, quality debts, volume-lock, and anti-degradation rules is defined
authoritatively in **`references/core/longform-quality-gates.md`**. Track rubrics:
`references/core/quality-rubric.md` (literary) and `references/core/webnovel-rubric.md`
(webnovel). Length policy, burn-rate, and the Arc Commissioning Loop: the Longform Addendum in
`references/core/editor-in-chief.md`.

Stage→agent bindings follow `references/core/aigora-system.md` with the longform additions:
**SerialArchitect** (`references/writing/serialarchitect.md`) is mandatory whenever longform mode
is active; **HookMaster** (`references/writing/hookmaster.md`) joins drafting/revision on the
webnovel track.

## Human Touchpoints（人工介入点）

Autopilot's four cases, plus the Longform Addendum's four (see `editor-in-chief.md`):

5. Budget crisis (burn-rate out of band twice running, or the ending can't fit the budget).
6. A volume over its revision cap on a dimension floor or Must Fix.
7. An unresolved drift flag after targeted revision.
8. A mid-book track change.

## Running It

### In Claude Code (recommended — real parallel subagents)

```
用 AIgora Longform 写一部长篇小说。Brief：<主题>；Track：网文向；目标规模：100万字以上，12卷。
项目目录：projects/<slug>/。卷级评审用并行子代理盲评。
```

Resume at any time with: "继续写 projects/<slug>" — the session reads `progress.md` and picks up
at the recorded next action.

### On claude.ai (single context)

Same triggers. Blind reviews degrade to sequential role-isolated passes (as in `AUTOPILOT.md`);
expect softer critique. The memory architecture works unchanged — it lives on disk, not in
context.

## Failure Modes to Watch

- **Ledger-triage skipping**: compacting a volume without dispositioning every ledger line is
  how volume 9 contradicts volume 2. The conservation check exists to catch this — run it.
- **Digest bloat**: a 4,000字 digest "to be safe" breaks the loading budget three volumes later.
  Caps are load-bearing; compress harder instead.
- **PROVISIONAL-row ossification**: treating the conception-time sketch of volume 11 as locked.
  Provisional rows exist to be rewritten at every volume boundary as the book teaches you what
  it is.
- **Retro-edit without the 四联更新**: an edit to a cold volume that skips the
  ledger-amendment/digest/entity/reader-recap update makes every future audit — and every
  future blind review — lie.
- **Contract-free parallel drafting**: drafting chapters concurrently without beat contracts +
  the seam audit silently downgrades "continuity guaranteed by the ledger" to "continuity
  salvaged by blind review". The parallel variant's four conditions (Drafting Modes) are a
  package, not à la carte.
- **Padding to budget**: the burn-rate check surfacing R < 0.8 is an instruction to cut threads
  or commission story — never to inflate scenes. The rubric scores padding as a defect at every
  scale.
