# Writing Agents Index (19)

Fiction writing specialists. In fiction mode, Core 6 + 10 Writing Agents = minimum 16 per round.
In longform mode (`/LONGFORM.md`), SerialArchitect joins as a mandatory 7th writing agent;
HookMaster joins stage selections on the webnovel track（网文向）only.

## Mandatory (Always included in fiction mode)

| File | Agent | Role |
|------|-------|------|
| aidetox.md | AIDetox | Removes AI writing patterns, adds human texture |
| voicedistinctor.md | VoiceDistinctor | Ensures each character sounds distinct |
| knowledgeauditor.md | KnowledgeAuditor | Tracks who knows what, prevents knowledge violations |
| firstreader.md | FirstReader | Simulates naive reader experience |
| characterpsychologist.md | CharacterPsychologist | Analyzes character depth, contradictions, arcs |
| emotionmaster.md | EmotionMaster | Engineers emotional impact, catharsis |

## Stage-Based Selection (Choose 4 based on writing stage)

### Stage 1: Conception (构思阶段)
Triggers: idea, concept, 设定, 构思, 大纲, 世界观, 人物设计, outline, premise

| File | Agent | Role |
|------|-------|------|
| muse.md | Muse | Generates images, metaphors, creative sparks |
| worldbuilder.md | WorldBuilder | Designs worlds as interconnected systems |
| plotarchitect.md | PlotArchitect | Structures plot, turning points, arcs |
| relationshipmapper.md | RelationshipMapper | Maps character relationships and dynamics |

### Stage 2: Drafting (写作阶段)
Triggers: 写, 场景, 章节, 对话, draft, 初稿, scene, chapter, write

| File | Agent | Role |
|------|-------|------|
| dialoguemaster.md | DialogueMaster | Crafts distinct character voices, subtext |
| scenepainter.md | ScenePainter | Renders sensory detail, atmosphere |
| narrator.md | Narrator | Controls POV, distance, information flow |
| pacemaster.md | PaceMaster | Manages rhythm, tension, scene length |

### Stage 3: Revision (修订阶段)
Triggers: 修改, 修订, 润色, 检查, revise, edit, polish, rewrite

| File | Agent | Role |
|------|-------|------|
| prosepolisher.md | ProsePolisher | Sentence-level refinement, cuts flab |
| symbolweaver.md | SymbolWeaver | Designs/tracks symbolic layer, motifs |
| openinghook.md | OpeningHook | Optimizes beginnings, first impressions |
| pacemaster.md | PaceMaster | Adjusts rhythm, fixes drags and rushes |

## Longform Agents（长篇智能体）

| File | Agent | Role | When |
|------|-------|------|------|
| serialarchitect.md | SerialArchitect | Volume/book-scale architecture, promise registry, escalation ladders, cast management | Mandatory in longform mode (both tracks) |
| hookmaster.md | HookMaster | Chapter-end hooks, anticipation inventory, 爽点 cadence, golden three chapters | Webnovel track（网文向）only |

Webnovel-track stage selections (which picks HookMaster displaces) are defined in
`references/core/aigora-system.md`, Longform & Webnovel Variants.

## Speaking Order in Fiction Mode

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

## Agent Collaboration Map

```
Muse ──────→ WorldBuilder ──────→ PlotArchitect
  │              │                     │
  ↓              ↓                     ↓
ScenePainter  CharacterPsychologist  PaceMaster
  │              │                     │
  ↓              ↓                     ↓
Narrator ←── DialogueMaster ──→ RelationshipMapper
  │              │                     │
  ↓              ↓                     ↓
EmotionMaster  VoiceDistinctor    SymbolWeaver
  │              │                     │
  ↓              ↓                     ↓
FirstReader ←── ProsePolisher ──→ KnowledgeAuditor
  │              │                     │
  └──────────→ AIDetox ←──────────────┘
```
