# Contributing

The Council of Five is opinionated methodology. The opinions are deliberate. Contributions that align with the methodology are welcome; contributions that fundamentally rework it will likely be declined unless they argue convincingly for the change.

## What's most welcome

In rough priority order:

1. **Corrections.** If COUNCIL.md or any persona template has an error, say so. The methodology is opinionated; opinions can be wrong.
2. **War stories.** Real "we tried convening for X, here's what happened" anecdotes that surface a strength or weakness of the framework.
3. **Persona refinements.** If you've used a voice (Heimdall, Susanoo, etc.) extensively and discovered that the prompt could be tighter or the recusal rule clearer, propose the refinement.
4. **Mode additions.** A new anti-groupthink mode or discovery mode that clearly fills a gap the existing four (anti-groupthink) or two (discovery) don't cover. The bar is high — argue convincingly.
5. **Harness adapters.** Persona definitions adapted for harnesses other than Claude Code (Cursor, Codex, Aider, custom). Open an issue first to discuss the shape.
6. **Translations.** If you'd like to translate the README or COUNCIL.md to another language, open an issue first.

## What will likely be declined

- **A sixth voice.** Five is the deliberate count. The case for adding one would have to be very strong (a domain that none of the existing five cover, that is so common it justifies a permanent voice rather than ad-hoc consultation).
- **Renaming the voices in the canonical methodology.** Heimdall / Susanoo / Hephaestus / Thoth / Saraswati are kept as the canonical names. You're free to use different names in your own implementation; the canonical names stay because they're recognizable and have established connotations.
- **Removing the Chair.** The Chair is the orchestrator. Without a Chair, the council has no convener. Some implementations might want the Chair to be implicit (just the user); that's fine in your fork, but the canonical methodology keeps it explicit.
- **Replacing the speaking order.** The order is justified in [docs/speaking-order.md](./docs/speaking-order.md). Counter-arguments are welcome but should engage with the rationale.
- **Mandating a specific harness or framework.** The Council of Five works in Claude Code, in any harness with subagent support, and in bare LLM use as five sequential prompts. Tying it to one harness would limit adoption.

## How to contribute

### For corrections and small refinements:

1. Open a PR with the fix
2. In the PR description, briefly say what changed and why
3. That's it

### For new content (modes, persona refinements, harness adapters):

1. Open an issue first describing what you want to add
2. We'll discuss whether it fits and how it should be scoped
3. Then open a PR with the content

### For war stories:

Post them as issues or PRs depending on whether they're sharing or proposing changes. The most credible content in this kind of methodology is "we tried X, here's what happened" — concrete experiences carry more weight than theoretical arguments.

## Style conventions

- **Short sentences.** "X happens because Y" beats "It is the case that X happens, which is attributable to Y."
- **Concrete over abstract.** When discussing failure modes or successes, name the specific situation.
- **No hype.** "Game-changing," "revolutionary," "unprecedented" — banned.
- **Honest about limits.** The methodology has real limits (latency, cost, requires harness support). Don't oversell.
- **Cite sources.** When borrowing concepts (Klein on pre-mortem, Kahneman & Klein on adversarial collaboration), credit them.

## Format expectations

- **Markdown** for all documentation
- **Mermaid** for diagrams (renders natively on GitHub)
- **CC BY 4.0 license** applies to all contributions
- **Internal links use relative paths** (e.g., `[COUNCIL.md](./COUNCIL.md)` not absolute URLs to GitHub)

## Code of conduct

- Disagree with ideas, not people
- Ask before assuming bad faith
- Thank people who correct your mistakes

## Maintainer

Ryan Gosnell — [GitHub @LoFiGamerGuy](https://github.com/LoFiGamerGuy)

---

*This file is CC BY 4.0 licensed, same as the rest of the repo.*
