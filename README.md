# Council of Five

A multi-perspective decision framework for AI-assisted engineering and strategy work. Five distinct voices — Architect, Challenger, Smith, Keeper, Weaver — convened by a Chair when a decision genuinely warrants more than one perspective. Most of the time, only one voice speaks. The discipline is in knowing when to convene the full council.

This repo is a methodology, a set of templates, and a working pattern for Claude Code (or any agent harness that supports subagents). It works alongside but is independent of any specific project.

## What this is

The Council of Five is a **prompt-time pattern**, not a long-running process. When an agent operates inside this framework, it consults five distinct voices for high-stakes decisions and lets one voice handle most everything else.

The five voices:

| Voice | Domain | When they speak |
|-------|--------|-----------------|
| **Architect** *(Heimdall)* | Long-horizon system design, ADRs, structural commitments | New design work; cross-cutting changes |
| **Challenger** *(Susanoo)* | Red-team, dissent, assumption-naming | Wherever consensus needs testing |
| **Smith** *(Hephaestus)* | Pragmatism, smallest-thing-that-ships, time/budget | Scope decisions; "is this worth building" |
| **Keeper** *(Thoth)* | Decision memory, locked decisions, silent-reversion detection | Anything that might collide with prior commitments |
| **Weaver** *(Saraswati)* | Cross-domain synthesis, collision detection | Multi-domain moves; portfolio-level decisions |

Convened by **the Chair** — your global agent persona that orchestrates and acts. The council advises; the chair acts.

The voice names come from mythological figures across cultures (Norse, Japanese, Greek, Egyptian, Hindu) chosen for thematic resonance. Keep them, rename them, or use the role names directly — your call.

## Why this exists

Single-agent multi-step reasoning has a structural blind spot: the agent that proposes a plan is not well-positioned to red-team it. Adding a second pass for critique helps. Adding *five* passes, each from a different perspective, with explicit anti-groupthink discipline, catches errors that no single perspective surfaces.

Most multi-agent frameworks parallelize *execution*. This framework parallelizes *perspective*. They serve different needs. See [docs/lore.md](./docs/lore.md) for the deeper rationale.

## Quick start

### 1. Decide if you actually need this

Most decisions don't warrant the full council. Single-voice mode is the default. Full council fires only on:

- Architectural decisions (ADRs, locked-decision challenges)
- Scope shifts that touch multiple domains
- Decisions where the cost of being wrong is high enough to justify five passes

For everything else, let one voice handle. See [docs/speaking-order.md](./docs/speaking-order.md) for the selection logic.

### 2. Set up the Chair persona

Your chair is the orchestrator — typically your global Claude Code persona (`~/.claude/CLAUDE.md`). Copy [`personas/chair-template.md`](./personas/chair-template.md) and adapt it to your operating model. The Council of Five section in that template is the load-bearing part.

### 3. Set up the five voices as Claude Code subagents

Drop the persona files into your Claude Code agents directory:

```bash
# Per-project (recommended)
mkdir -p .claude/agents/
cp personas/heimdall.md personas/susanoo.md personas/hephaestus.md \
   personas/thoth.md personas/saraswati.md \
   .claude/agents/

# Or globally
cp personas/{heimdall,susanoo,hephaestus,thoth,saraswati}.md \
   ~/.claude/agents/
```

The chair will invoke the appropriate voice (or convene the full council) based on the question.

### 4. Adapt the cross-domain commitments file

The Weaver (Saraswati) needs a reference file describing your active commitments across domains. Copy [`templates/cross-domain-commitments.md`](./templates/cross-domain-commitments.md) to your repo root and fill in your domains. Personal data goes in `cross-domain-commitments.local.md` (gitignored), public structure in `cross-domain-commitments.md` (tracked).

### 5. Convene the council

Use the kickoff prompt in [`templates/new-convening-kickoff-prompt.md`](./templates/new-convening-kickoff-prompt.md). The session writes a convening log per [`templates/convening-log.md`](./templates/convening-log.md).

## Repo structure

```
council-of-five/
├── README.md                    ← you are here
├── COUNCIL.md                   ← canonical methodology (load-bearing)
├── CHAIR-DISCIPLINE.md          ← chair handoff principles
│
├── personas/
│   ├── README.md                ← how to use the persona templates
│   ├── chair-template.md        ← global chair persona template
│   ├── heimdall.md              ← Architect voice
│   ├── susanoo.md               ← Challenger voice
│   ├── hephaestus.md            ← Smith voice
│   ├── thoth.md                 ← Keeper voice
│   └── saraswati.md             ← Weaver voice
│
├── templates/
│   ├── convening-log.md         ← template for new convening logs
│   ├── new-convening-kickoff-prompt.md
│   └── cross-domain-commitments.md
│
├── docs/
│   ├── speaking-order.md        ← rationale for the speaking sequence
│   ├── modes.md                 ← anti-groupthink + discovery modes deep dive
│   ├── tiebreakers.md           ← disagreement and tiebreaker math
│   ├── failure-modes.md         ← council theater, persona narration, etc.
│   └── lore.md                  ← naming rationale and design history
│
└── examples/
    └── example-convening.md     ← one fully-worked example end-to-end
```

## When NOT to use this

- **Trivial decisions.** Most calls don't warrant five voices. The overhead is more than the value.
- **Time-critical hotfixes.** Five voices add latency. When seconds matter, single agent + careful review is faster.
- **Decisions where you already know the answer.** The council surfaces blind spots; if you have none on this question, you're paying for ceremony.
- **Pure execution work.** Writing code, drafting prose, running tests — the chair operates solo here. The council steps back entirely.

## Compared to other multi-agent patterns

This is *complementary* to plan/execute/judge ([share-ai-engineering-patterns 03](https://github.com/LoFiGamerGuy/share-ai-engineering-patterns/blob/main/03-multi-agent-workflows/plan-execute-judge.md)) and reflection loops, not competing.

- **Plan / execute / judge** parallelizes *execution* — three roles, one task, sequential pipeline.
- **Reflection loops** add a single critic to a single generator.
- **Council of Five** parallelizes *perspective* — five voices, one decision, structured deliberation.

You'd typically use plan/execute/judge for *building*, the council for *deciding*. Many projects use both: convene the council to decide direction, then dispatch plan/execute/judge to build.

## Compatibility

- **Claude Code** — first-class support via subagent definitions in `.claude/agents/`. Tested.
- **Other harnesses with subagents** (Cursor, Codex, custom) — should work; persona definitions translate. The convening orchestration may need harness-specific adaptation.
- **Bare LLM use** — the methodology is harness-independent. You can run convenings as five sequential prompts in a single chat session if you have to. The discipline is the value, not the orchestration.

## Author and license

Designed and built by **Ryan Gosnell** ([@LoFiGamerGuy](https://github.com/LoFiGamerGuy)).

Licensed under [CC BY 4.0](./LICENSE) — share, adapt, build on; just credit the source.

## Related public repos

This repo is part of a small family of public reference material on agentic engineering. Each has both a source repo and a live site.

- **[share-ai-engineering-patterns](https://github.com/LoFiGamerGuy/share-ai-engineering-patterns)** &middot; [live catalogue →](https://lofigamerguy.github.io/share-ai-engineering-patterns/) — Practitioner's reference for building with AI agents: patterns, infrastructure, tradeoffs. The Council of Five is a *complementary* multi-agent pattern to the plan/execute/judge and reflection-loop patterns documented there. CC BY 4.0.
- **[reference-library-methodology](https://github.com/LoFiGamerGuy/reference-library-methodology)** &middot; [live →](https://lofigamerguy.github.io/reference-library-methodology/) — System for building a queryable, AI-readable technical reference library. Useful when the council needs to consult a corpus of source material across deliberations. MIT licensed.
- **[five-register-design-system](https://github.com/LoFiGamerGuy/five-register-design-system)** &middot; [live gallery →](https://lofigamerguy.github.io/five-register-design-system/) — Design system for the artifacts agentic work produces. MIT licensed.
- **[terminal-stack](https://github.com/LoFiGamerGuy/terminal-stack)** — Opinionated terminal kit for Git Bash on Windows.
- **[dotfiles](https://github.com/LoFiGamerGuy/dotfiles)** — Personal dotfiles.

More repos in this family will be released over time.

---

*Five voices, one chair, structured perspective. Council of Five · v1.0 · May 2026.*
