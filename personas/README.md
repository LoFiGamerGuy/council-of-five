# Persona Templates

Six persona files that operationalize the Council of Five in Claude Code (or any harness with subagent support).

```
personas/
├── README.md                  ← you are here
├── chair-template.md          ← global agent persona (the orchestrator)
├── heimdall.md                ← Architect voice
├── susanoo.md                 ← Challenger voice
├── hephaestus.md              ← Smith voice
├── thoth.md                   ← Keeper voice
└── saraswati.md               ← Weaver voice
```

## How to install

### Chair persona

Copy `chair-template.md` to your global Claude Code config — typically `~/.claude/CLAUDE.md` (or merge with an existing global persona). The Council of Five section is the load-bearing part for council operation.

```bash
# Fresh install
cp personas/chair-template.md ~/.claude/CLAUDE.md

# Merge with existing persona — open both files and combine the council section
```

### Voice subagents

Drop the five voice files into your Claude Code agents directory:

```bash
# Per-project (recommended — keeps the council scoped to projects that use it)
mkdir -p .claude/agents/
cp personas/heimdall.md personas/susanoo.md personas/hephaestus.md \
   personas/thoth.md personas/saraswati.md \
   .claude/agents/

# Or globally (council available in every project)
mkdir -p ~/.claude/agents/
cp personas/{heimdall,susanoo,hephaestus,thoth,saraswati}.md \
   ~/.claude/agents/
```

The Chair will invoke the appropriate voice (or convene the full council) based on the question and the rules in [`COUNCIL.md`](../COUNCIL.md).

## Customization

Each voice file is a starting template. Customize them for your operating model:

- **Domain language.** If you don't have ADRs, replace "ADR" with whatever your equivalent is ("design decisions," "architectural commitments," "RFCs").
- **Tools.** The default tool set is `Read, Grep, Glob` — read-only. The voices return positions; the chair handles persistence. If your workflow needs a voice with write access (rare), add it explicitly and consider whether that voice should still recuse on execution work.
- **Model tier.** Default is `opus` (top tier) for the architect and challenger; mid-tier is reasonable for the smith and keeper. Calibrate to your token budget.
- **References.** Each voice template has a "References" section pointing at files the voice should consult. Replace the placeholders with paths to your actual reference material.

## Conventions across all voice files

- **YAML frontmatter** — `name`, `description`, `tools`, `model`. Claude Code parses these to register the subagent.
- **Persona section** — what the voice is, what it isn't, what it recuses on.
- **Domain rules** — load-bearing constraints on what the voice considers and how.
- **References** — read-only paths the voice consults.
- **Mode-aware behavior** — how the voice responds in each anti-groupthink mode.
- **Output format** — structured text the chair can append to a convening transcript.
- **Honest abstention return path** — the canonical `"no domain objection"` response when the voice has nothing substantive to add.

These conventions are uniform across all five voices for orchestration consistency.

## Testing the install

After installing, run a low-stakes test convening:

```
[Council convened — full council. Anti-groupthink mode: hybrid.]

Question: Should we add a `lint` step to our CI pipeline?
```

You should see:
1. Each voice respond in speaking order
2. Some voices honestly abstain ("no domain objection") because the question is small
3. The chair synthesize and write a convening log

If the voices don't fire, check that Claude Code recognizes the agents (`/agents` command) and that the YAML frontmatter is valid.
