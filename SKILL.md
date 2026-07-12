---
name: aigora-agents
description: >
  AIgora intellectual dialogue, fiction writing, and game design system. Core 6 agents (Diverger, Literature 
  Reviewer, Yes And, Logician, Challenger, Synthesizer) with fixed speaking order. Gatekeeper for fiction 
  writing stage transitions. EditorInChief + quality rubric for Autopilot (fully automated) fiction mode. 
  17 Writing Agents for fiction mode. 6 Game Design Agents for game design mode. 
  Plus 82 specialist agents: Thinkers (17), Writers (26), Philosophers (22), Researchers (17). 
  Triggers: AIgora, 召唤, 讨论, 小说, 写作, fiction, dialogue, 游戏设计, Game Design, 自动写作, autopilot.
---

# AIgora Discussion System

## CRITICAL: Read Core Rules First

Before any AIgora discussion, **MUST READ**: `references/core/aigora-system.md`

---

## Core Agents

### Discussion Agents (6 - Always Required)

| Agent | Role | Order | File |
|-------|------|-------|------|
| **Diverger** | Opens possibility space | 1st (fixed) | `references/core/diverger.md` |
| **Literature Reviewer** | Provides evidence foundation | Flexible | `references/core/literature-reviewer.md` |
| **Yes And** | Builds and connects | Flexible | `references/core/yes-and.md` |
| **Logician** | Analyzes argument structure | Flexible | `references/core/logician.md` |
| **Challenger** | Pressure-tests everything | 2nd to last (fixed) | `references/core/challenger.md` |
| **Synthesizer** | Closes the round | Last (fixed) | `references/core/synthesizer.md` |

### Process Control Agents (Fiction Mode Only)

| Agent | Role | When | File |
|-------|------|------|------|
| **Gatekeeper** | Controls stage transitions, surfaces key decisions | At stage transitions | `references/core/gatekeeper.md` |
| **EditorInChief** | Author-proxy: answers Gatekeeper decisions in Autopilot mode, logs rationale | Autopilot mode only | `references/core/editor-in-chief.md` |

Gatekeeper is NOT a discussion participant. It appears only at stage transitions to ensure the user makes critical decisions before proceeding. In **Autopilot mode**, the EditorInChief answers in the user's place and every decision is logged (see below).

### Speaking Order

```
User Input
    ↓
[1] Diverger (opens directions, states inclination)
    ↓
[Flexible] Literature Reviewer + Yes And + Logician + Specialists/Writing Agents
    ↓
[2nd to last] Challenger (questions everything)
    ↓
[Last] Synthesizer (consensus, disagreement, next steps)
```

---

## Game Design Mode

**Triggers**: 游戏设计, Game Design, 游戏机制, 玩法设计, game mechanics, game balance, 游戏平衡

When game design mode activates: **Core 3 (Diverger, Challenger, Synthesizer) + Game Design 6 = 9 agents**

### Game Design Agents (6) — `references/gamedesign/`

| Order | Agent | Role | File |
|-------|-------|------|------|
| 2nd | **Visionary** | Defines and guards core experience | `references/gamedesign/visionary.md` |
| 3rd | **MechanicSmith** | Designs concrete rules and systems | `references/gamedesign/mechanicsmith.md` |
| 4th | **Economist** | Balances numbers and resources | `references/gamedesign/economist.md` |
| 5th | **Psychologist** | Analyzes player motivation and emotion | `references/gamedesign/psychologist.md` |
| 6th | **Breaker** | Finds exploits and edge cases | `references/gamedesign/breaker.md` |
| 7th | **Producer** | Evaluates feasibility and priorities | `references/gamedesign/producer.md` |

### Game Design Speaking Order

```
User Input (game idea or problem)
    ↓
[1] Diverger — opens possibility space
    ↓
[2] Visionary — defines core experience
    ↓
[3] MechanicSmith — proposes mechanics
    ↓
[4] Economist — analyzes balance
    ↓
[5] Psychologist — analyzes player feelings
    ↓
[6] Breaker — finds exploits
    ↓
[7] Challenger — questions logic
    ↓
[8] Producer — evaluates feasibility
    ↓
[9] Synthesizer — integrates and concludes
```

---

## Fiction Writing Mode

**Triggers**: 小说, 故事, 剧本, 虚构写作, novel, story, screenplay, fiction, creative writing, character, world-building, plot, scene, dialogue, revision

When fiction mode activates: **Core 6 + Writing 10 + Gatekeeper = minimum 17 agents per round**

### Fiction Writing Pipeline

Fiction writing follows a structured pipeline with Gatekeeper controlling stage transitions:

```
┌─────────────────────────────────────────────────────────────┐
│  Stage 0: DIRECTION                                         │
│  User provides initial idea/request                         │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  Stage 1: CONCEPTION                                        │
│  Core 6 + Writing Agents (Muse, WorldBuilder, etc.)        │
│  Output: Possible directions, themes, characters            │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  ★ GATEKEEPER: Conception → Detailed Outline               │
│  Surfaces decisions:                                        │
│  - Story core (what is this really about?)                 │
│  - Emotional target (what should reader feel?)             │
│  - Ending direction (how does this resolve?)               │
│  WAITS for user confirmation                                │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  Stage 2: DETAILED OUTLINE                                  │
│  Core 6 + Writing Agents                                    │
│  Output: Scene structure, character arcs, key moments       │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  ★ GATEKEEPER: Detailed Outline → Drafting                 │
│  Surfaces decisions:                                        │
│  - Structure confirmation                                   │
│  - Key scenes/dialogue to include                          │
│  - POV and tone                                            │
│  WAITS for user confirmation                                │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  Stage 3: DRAFTING                                          │
│  Core 6 + Writing Agents (DialogueMaster, ScenePainter...)  │
│  Output: Complete first draft                               │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  Stage 4: CRITIQUE                                          │
│  All agents review the draft                                │
│  Output: Issues identified, revision suggestions            │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  ★ GATEKEEPER: Critique → Revision                         │
│  Presents revision checklist:                               │
│  - Must fix (critical issues)                              │
│  - Should fix (recommended)                                │
│  - Optional (polish)                                       │
│  WAITS for user to accept/adjust                            │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  Stage 5: REVISION                                          │
│  Execute accepted changes                                   │
│  Output: Final draft + score                                │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  ★ GATEKEEPER: Final Assessment                            │
│  - Completion status                                        │
│  - Score (structure, emotion, language, etc.)              │
│  - Brief evaluative comment                                │
└─────────────────────────────────────────────────────────────┘
```

### Gatekeeper Decision Points

Gatekeeper asks about **real decisions**, not trivial choices:

| Stage Transition | Must Ask | Don't Ask |
|------------------|----------|-----------|
| Conception → Outline | Story core, emotional target, ending direction | Word count, formatting |
| Outline → Drafting | Structure confirmation, key moments, POV | Style minutiae |
| Critique → Revision | Accept/reject revision items | Grammar details |

If user says "continue" or "你决定", Gatekeeper proceeds with the direction favored in discussion.

### Autopilot Mode（全自动模式）

**Triggers**: 自动写作, 全自动小说, autopilot, "write it autonomously"

**MUST READ before running**: `AUTOPILOT.md` (pipeline), `references/core/editor-in-chief.md`
(author-proxy), `references/core/quality-rubric.md` (quality gate).

The same fiction pipeline runs end-to-end without waiting for the user:

| Manual mode | Autopilot mode |
|-------------|----------------|
| Gatekeeper waits for user at checkpoints | **EditorInChief** decides; rationale logged to `decisions.md` |
| Vague final score | Rubric gate: total ≥ 48/60, every dimension ≥ 7, max 3 revision rounds |
| Same-context critique | 3 **blind parallel reviewers** (fresh contexts/subagents), median scores |
| Memory = conversation | Project files: `projects/<slug>/` (story bible, outline, continuity ledger) |

Human is consulted ONLY on: gate failure after 3 revision rounds, value-laden material,
decisions the brief reserves, or the brief itself. Everything else is decided and logged.

### Writing Agents (17) — `references/writing/`

#### Mandatory (6 - Always included)

| Agent | Role |
|-------|------|
| **AIDetox** | Removes AI writing patterns |
| **VoiceDistinctor** | Ensures distinct character voices |
| **KnowledgeAuditor** | Tracks who knows what |
| **FirstReader** | Simulates reader experience |
| **CharacterPsychologist** | Analyzes character depth |
| **EmotionMaster** | Engineers emotional impact |

#### Stage-Based (Select 4)

| Stage | Triggers | Agents |
|-------|----------|--------|
| **Conception** | idea, 构思, 大纲, outline | Muse, WorldBuilder, PlotArchitect, RelationshipMapper |
| **Drafting** | 写, scene, chapter, draft | DialogueMaster, ScenePainter, Narrator, PaceMaster |
| **Revision** | 修改, revise, edit, polish | ProsePolisher, SymbolWeaver, OpeningHook, PaceMaster |

### Writing Agent Speaking Order

```
[After Diverger]
    ↓
[Generative] Muse → WorldBuilder → PlotArchitect
    ↓
[Character] CharacterPsychologist → RelationshipMapper → DialogueMaster
    ↓
[Execution] Narrator → ScenePainter → PaceMaster → EmotionMaster
    ↓
[Quality] FirstReader → ProsePolisher → SymbolWeaver → OpeningHook
    ↓
[Audit] AIDetox → VoiceDistinctor → KnowledgeAuditor
    ↓
[Before Challenger]
```

---

## Specialist Agents (75 Total)

Add based on topic. They speak in the flexible middle zone.

### Thinkers (17) — `references/thinkers/`

| When to Use | Agents |
|-------------|--------|
| Political philosophy | Marx, Hayek, Arendt, Berlin, Schmitt |
| Social theory | Weber, Foucault, Gramsci |
| Epistemology | Popper |
| Conservatism | Burke, Oakeshott, Strauss |
| Liberalism | Mill, Tocqueville, Smith |

### Philosophers (22) — `references/philosophers/`

| When to Use | Agents |
|-------------|--------|
| Ancient | Socrates, Plato, Aristotle, Epicurus, Cicero, Seneca |
| Medieval | Augustine, Aquinas |
| Ethics | Kant, Mill, Levinas, Nussbaum, Aristotle, Seneca |
| Epistemology | Descartes, Hume, Wittgenstein |
| Metaphysics | Leibniz, Hegel, Schopenhauer, Plato |
| Existence/Death | Kierkegaard, Heidegger, Epicurus, Seneca |
| Justice/Politics | Rawls, Charles Taylor, Cicero |

### Writers (26) — `references/writers/`

| When to Use | Agents |
|-------------|--------|
| Epic/Mythic | Homer, Dante, Tolkien |
| Realism | Austen, Tolstoy, Dickens |
| Psychological | Dostoevsky, Kafka, Nabokov |
| Magic realism | Borges, García Márquez |
| Science fiction | Ted Chiang, Liu Cixin, Heinlein |
| Chinese | Lu Xun, Du Fu, Jin Yong |

### Researchers (17) — `references/researchers/`

| When to Use | Agents |
|-------------|--------|
| Research design | Quantitative/Qualitative Methodologist |
| Causal inference | Econometrician |
| Analysis | Data Scientist, Game Theorist |
| Domain | Geopolitical Analyst, Political Economist, Futurist |

---

## Agent Selection Logic

### Step 1: Detect Mode

| User Request | Mode | Agents |
|--------------|------|--------|
| 讨论X, analyze, AIgora | General | Core 6 + Specialists |
| 写小说, fiction, 场景 | Fiction | Core 6 + Writing 10 + Specialists |
| 游戏设计, Game Design, 游戏机制 | Game Design | Core 3 + Game Design 6 |

### Step 2: Identify Topic → Select Specialists

| Topic | Primary Specialists |
|-------|---------------------|
| 政治、权力、自由 | Thinkers (Marx, Hayek, Arendt) |
| 哲学、存在、伦理 | Philosophers (Kant, Heidegger) |
| 宗教、生死 | Philosophers + Writers (Kierkegaard, Dostoevsky) |
| 经济、发展 | Thinkers + Researchers |
| 方法论、研究 | Researchers |
| AI、技术、未来 | Heidegger + Arendt + Futurist |
| 历史小说 | Writers + Thinkers |
| 科幻小说 | Liu Cixin + Ted Chiang + Futurist |

### Step 3: Load Agent Files

Read all selected agent files from `references/` before discussion.

---

## Example Configurations

### Example 1: General Discussion
**"召唤AIgora讨论AI for good"**

```
Core 6 + Specialists (5):
- Heidegger (技术批判)
- Arendt (行动与公共领域)
- Nietzsche (价值重估)
- Levinas (他者伦理)
- Futurist (情景分析)

Total: 11 agents
```

### Example 2: Fiction - Conception Stage
**"帮我设计一个科幻小说的世界观"**

```
Core 6 + Writing 10 + Specialists:
- Mandatory 6: AIDetox, VoiceDistinctor, KnowledgeAuditor, FirstReader, CharacterPsychologist, EmotionMaster
- Stage 4: Muse, WorldBuilder, PlotArchitect, RelationshipMapper
- Specialists: Liu Cixin, Ted Chiang

Total: 18 agents
```

### Example 3: Fiction - Revision Stage
**"帮我润色这个章节的对话"**

```
Core 6 + Writing 10:
- Mandatory 6: AIDetox, VoiceDistinctor, KnowledgeAuditor, FirstReader, CharacterPsychologist, EmotionMaster
- Stage 4: ProsePolisher, SymbolWeaver, OpeningHook, PaceMaster

Total: 16 agents
```

### Example 4: Game Design
**"召唤游戏设计AIgora，讨论诗人PK游戏的随机性问题"**

```
Core 3 + Game Design 6:
- Diverger, Challenger, Synthesizer
- Visionary, MechanicSmith, Economist, Psychologist, Breaker, Producer

Total: 9 agents
```

---

## Discussion Format

### General Mode
```
## AIgora: [Topic]

**参与者**: Core 6 + [Specialists]

### Diverger
[Opens possibility space]

### Literature Reviewer / Yes And / Logician
[Flexible order, evidence and building]

### [Specialist 1], [Specialist 2]...
[Domain expertise]

### Challenger
[Pressure-tests everything]

### Synthesizer
- Core Claims: ...
- Consensus: ...
- Disagreements: ...
- Next Steps: ...
```

### Fiction Mode
```
## AIgora Fiction: [Task]

**Stage**: Conception / Drafting / Revision
**参与者**: Core 6 + Writing 10 + [Specialists]

### Diverger
[Opens creative directions]

### Writing Agents (by order)
[Muse → WorldBuilder → ... → AIDetox]

### Challenger
[Tests the creative choices]

### Synthesizer
[Consolidates decisions, identifies open questions]
```

### Game Design Mode
```
## 游戏设计AIgora: [Topic]

**参与者**: Core 3 + Game Design 6

### Diverger
[Opens possibility space]

### Visionary
[Defines core experience]

### MechanicSmith
[Proposes concrete mechanics]

### Economist
[Analyzes numbers and balance]

### Psychologist
[Analyzes player emotions]

### Breaker
[Attempts to break the design]

### Challenger
[Questions logic and assumptions]

### Producer
[Evaluates feasibility and priority]

### Synthesizer
**共识：**
- ...

**分歧：**
- ...

**下一步：**
- ...
```

---

## Quick Reference: File Locations

| Category | Index | Count |
|----------|-------|-------|
| Core System | `references/core/aigora-system.md` | 1 |
| Autopilot Pipeline | `AUTOPILOT.md` | 1 |
| Core 6 | `references/core/` | 6 |
| Gatekeeper | `references/core/gatekeeper.md` | 1 |
| EditorInChief | `references/core/editor-in-chief.md` | 1 |
| Quality Rubric | `references/core/quality-rubric.md` | 1 |
| Project Templates | `projects/_template/` | 4 |
| Game Design | `references/gamedesign/index.md` | 6 |
| Writing | `references/writing/index.md` | 17 |
| Thinkers | `references/thinkers/index.md` | 17 |
| Philosophers | `references/philosophers/index.md` | 22 |
| Writers | `references/writers/index.md` | 26 |
| Researchers | `references/researchers/index.md` | 17 |
| **Total Agents** | | **114** |
