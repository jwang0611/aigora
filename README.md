# AIgora: Multi-Agent Intellectual Dialogue System

AIgora is a structured multi-agent discussion framework for Claude that transforms single-model conversations into rich intellectual dialogues with multiple specialized perspectives.

## Why AIgora?

Large language models excel at generating fluent text, but struggle with genuine intellectual depth. A single model tends to:
- Converge too quickly on "reasonable" answers
- Avoid productive tension between perspectives
- Miss blind spots in its own reasoning

AIgora addresses this by orchestrating **multiple agent personas** with distinct cognitive roles, creating structured dialogue where ideas are explored, challenged, and synthesized—not just generated.

## Core Architecture

### The Fixed Speaking Order

AIgora enforces a deliberate speaking order that mirrors how productive intellectual discourse unfolds:

```
User Input
    ↓
[1] Diverger ────────── Opens possibility space (always first)
    ↓
[Flexible Zone] ─────── Literature Reviewer, Yes And, Logician, Specialists
    ↓
[N-1] Challenger ────── Pressure-tests everything (always second-to-last)
    ↓
[N] Synthesizer ─────── Closes the round (always last)
```

**Why this order matters:**
- **Diverger first**: Prevents premature convergence. The discussion must open before it can narrow.
- **Challenger second-to-last**: All material must be on the table before the pressure test.
- **Synthesizer last**: Nothing follows synthesis within a round—it prepares the next iteration.

### The Core Agents

| Agent | Cognitive Role | Key Behavior |
|-------|---------------|--------------|
| **Diverger** | Opens possibility space | Explores lateral, vertical, cross-domain, and contrary directions. States inclination after mapping terrain. |
| **Literature Reviewer** | Provides evidence foundation | Grounds discussion in existing knowledge, research, and precedents. |
| **Yes And** | Builds and connects | Finds productive combinations. Extends ideas constructively. |
| **Logician** | Analyzes argument structure | Examines validity, identifies fallacies, clarifies reasoning chains. |
| **Challenger** | Pressure-tests everything | Questions assumptions, stress-tests arguments, offers alternatives. |
| **Synthesizer** | Closes the round | Extracts claims, identifies consensus/disagreement, prepares next steps. |
| **Gatekeeper** | Controls stage transitions (Fiction mode) | Surfaces key decisions, ensures user confirms before proceeding. |

### Three Specialized Modes

**General Discussion Mode** (default)
- Core 6 + topic-relevant specialists
- For: Philosophy, policy analysis, complex decisions

**Fiction Writing Mode** (triggers: 小说, story, character, scene...)
- Core 6 + 10 Writing Agents + Gatekeeper (flow control)
- Mandatory: AIDetox, VoiceDistinctor, KnowledgeAuditor, FirstReader, CharacterPsychologist, EmotionMaster
- Stage-based: Conception / Drafting / Revision agents
- **5-stage pipeline with 3 Gatekeeper checkpoints**

**Game Design Mode** (triggers: 游戏设计, game mechanics, balance...)
- Core 3 (Diverger, Challenger, Synthesizer) + 6 Game Design Agents
- Visionary → MechanicSmith → Economist → Psychologist → Breaker → Producer

**Autopilot Mode** (triggers: 自动写作, autopilot) — see `AUTOPILOT.md`
- The fiction pipeline, fully automated: the **EditorInChief** agent answers every Gatekeeper
  checkpoint in the author's place, logging each decision with rationale to `decisions.md`
- Quantified quality gate (`references/core/quality-rubric.md`): 6 dimensions × 10 points,
  pass at ≥ 48/60 with no dimension < 7, max 3 revision rounds
- Blind critique by 3 parallel fresh-context reviewers (subagents in Claude Code), median scores
- On-disk project memory: `projects/<slug>/` (story bible, outline, continuity ledger, chapters)
- Humans are consulted only on: gate failure after 3 rounds, value-laden material, decisions the
  brief reserves, or the brief itself

## Fiction Writing Pipeline

Fiction writing follows a structured pipeline with **Gatekeeper** controlling stage transitions:

```
┌─────────────────────────────────────────────────────────────┐
│  Stage 1: CONCEPTION                                        │
│  Core 6 + Writing Agents explore directions                 │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  ★ GATEKEEPER                                               │
│  Asks: What is the story about? What should reader feel?   │
│  WAITS for user decision                                    │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  Stage 2: DETAILED OUTLINE                                  │
│  Structure, scenes, character arcs                          │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  ★ GATEKEEPER                                               │
│  Asks: Structure confirmed? Key moments? POV?              │
│  WAITS for user decision                                    │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  Stage 3: DRAFTING                                          │
│  Complete first draft                                       │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  Stage 4: CRITIQUE                                          │
│  All agents review and identify issues                      │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  ★ GATEKEEPER                                               │
│  Presents: Must fix / Should fix / Optional                │
│  WAITS for user to accept                                   │
└─────────────────────┬───────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────────────┐
│  Stage 5: REVISION + FINAL ASSESSMENT                       │
│  Execute changes, score, export file                        │
└─────────────────────────────────────────────────────────────┘
```

### What Gatekeeper Asks

Gatekeeper asks about **real decisions**, not trivial choices:

| Stage | Must Ask | Don't Ask |
|-------|----------|-----------|
| Conception → Outline | Story core, emotional target, ending | Word count, formatting |
| Outline → Drafting | Structure, key moments, POV | Style minutiae |
| Critique → Revision | Accept/reject items | Grammar details |

## Agent Philosophy

### Agents Have Views

Unlike neutral "perspectives," AIgora agents are **opinionated**:
- Diverger states where it thinks the treasure lies
- Challenger means what it says—not playing devil's advocate
- Specialists embody genuine intellectual positions

### Agents Interact

Direct dialogue is encouraged:
- Challenger may disagree with Diverger's inclination
- Specialists can build on or critique each other
- Synthesizer assesses argument quality (not just summarizes)

### Constraints Breed Depth

The fixed order and role boundaries create productive constraints:
- Diverger can't critique (that's Challenger's job)
- Synthesizer can't add new ideas (only works with what's on table)
- Each agent does one thing deeply, not everything superficially

## 82 Specialist Agents

Beyond the Core agents, AIgora includes specialist agents organized by domain:

| Category | Count | Examples |
|----------|-------|----------|
| **Thinkers** | 17 | Marx, Hayek, Arendt, Foucault, Weber, Popper... |
| **Philosophers** | 22 | Plato, Aristotle, Kant, Heidegger, Wittgenstein... |
| **Writers** | 26 | Homer, Dostoevsky, Borges, Liu Cixin, Jin Yong... |
| **Researchers** | 17 | Econometrician, Game Theorist, Futurist... |

Specialists are selected based on topic relevance and speak in the flexible middle zone.

## How to Get the Best Results

> **AIgora is a discussion partner, not an automation tool.**

### 1. Engage in the Discussion

AIgora works best when you treat it as an intellectual dialogue:
- **React to agent perspectives**: "I agree with Challenger's point about X, but..."
- **Push back**: "The Synthesizer missed the core tension here"
- **Add your own ideas**: "What if we approached it from Y angle?"

### 2. Make Your Decisions Clear

At Gatekeeper checkpoints, you must decide:
- What is the **core** of this story/argument/design?
- What **emotion** should the reader feel?
- What is the **main tension** you want to explore?

**Bad**: "Just pick something reasonable"  
**Good**: "I want to explore the tension between connection and authenticity"

### 3. Don't Skip the Process

The structured pipeline exists for a reason:
- **Conception** → establishes what you're building
- **Outline Review** → confirms direction before detailed work
- **Critique** → catches problems before final polish

### 4. Iterate, Don't One-Shot

AIgora is designed for multi-round dialogue. One-shot prompts produce generic results. Extended dialogue produces distinctive work.

---

## Usage Examples

### General Discussion
```
User: Summon AIgora to discuss "Is AI alignment a solvable problem？"

[Claude detects: General mode]
[Agents: Core 6 + Specialists (Popper, Wittgenstein, Futurist)]
```

### Fiction Writing
```
User: Design a Sci-Fi world view about the social differentiation after mind uploading for me.

[Claude detects: Fiction mode, Conception stage]
[Agents: Core 6 + Writing 10 + Gatekeeper + Specialists (Liu Cixin, Ted Chiang)]
```

### Game Design
```
User: Summon a game design Aigora to discuss whether the randomness of this card game is too high.

[Claude detects: Game Design mode]
[Agents: Core 3 + Game Design 6]
```

## Installation

1. Download the `aigora-agents` folder
2. Place it in your Claude skill directory: `/mnt/skills/user/aigora-agents/`
3. The skill will auto-activate on trigger phrases

## Trigger Phrases

| Language | Triggers |
|----------|----------|
| Chinese | 召唤AIgora, 讨论, 小说, 写作, 游戏设计, 自动写作 |
| English | AIgora, dialogue, fiction, creative writing, game design, autopilot |

## Design Principles

**1. Structure Over Freedom**
Rigid speaking order creates space for genuine exploration. Agents can't do everything, so they do their role deeply.

**2. Tension Over Consensus**
Challenger exists to prevent premature agreement. Disagreement is mapped, not resolved.

**3. Substance Over Performance**
Agents don't perform their roles theatrically—they embody distinct cognitive functions.

**4. Iteration Over Completion**
Each round ends with "next steps." The Synthesizer prepares the ground; the user decides where to go.

## Customization

You can:
- Add custom specialist agents in `references/`
- Modify agent definitions to suit your needs
- Create new modes (e.g., Legal Analysis, Academic Review)

## Credits

AIgora was developed by Zhang Xiaoyu (张笑宇) as part of research into AI-assisted intellectual discourse.

The name "AIgora" combines "AI" with "Agora"—the ancient Greek public gathering space where citizens debated ideas.

## License

CC BY-NC 4.0 (Creative Commons Attribution-NonCommercial 4.0)

You can freely use, share, and adapt this work for non-commercial purposes with attribution.

---

*"The goal is not to make Claude smarter, but to make Claude think in more dimensions."*
