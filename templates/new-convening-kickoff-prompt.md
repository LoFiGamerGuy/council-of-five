# New Convening — Kickoff Prompt

Drop-in prompt to start a council convening in a Claude Code session (or any harness with subagent support).

## Usage

1. **Decide if you actually need the council.** Most decisions don't. Full council fires for: ADRs, locked-decision challenges, scope shifts, multi-domain moves. For everything else, let one voice handle.
2. **Pick the right anti-groupthink mode.** Default is `hybrid`. See [`COUNCIL.md`](../COUNCIL.md) for the catalog.
3. **Paste the prompt below** into a session where the council is configured (the chair persona is loaded; the five voice subagents are installed in `.claude/agents/`).
4. **Replace `<QUESTION>`** with your actual question.
5. **Let the council run.** The session writes a convening log to `convenings/` per [`templates/convening-log.md`](./convening-log.md).

## Standard prompt (full council, hybrid mode)

```text
[Council convened — full council. Anti-groupthink mode: hybrid.]

Question: <QUESTION>

Apply the convening rules in COUNCIL.md:
- Speaking order: Thoth → Saraswati → Heimdall → Hephaestus → Susanoo
- Each voice contributes 2-4 sentences from their domain
- Voices may recuse with "not my domain" or "no domain objection" if applicable
- After all voices speak, run hybrid anti-groupthink (pre-mortem + steelman + Thoth's reference-bound check)
- If consensus is unanimous, run anti-groupthink. Honest abstention ("no domain objection") is allowed. Do NOT manufacture dissent.
- Log the convening to convenings/<YYYY-MM-DD>-<topic-slug>.md per templates/convening-log.md
- Run the reference-rot check at the end (verify cited paths resolve)

Output the trace as you go, then summarize the decision at the end.
```

## Variants

### Single-voice mode (most common)

For everyday calls, you don't need the full prompt. Just ask the question. The Chair picks the appropriate voice based on the speaking-order priority and answers.

```text
<QUESTION>

(If this lands cleanly in one voice's domain, that voice answers.
 If ambiguous, the Chair picks per the priority order in COUNCIL.md.)
```

### Specific anti-groupthink mode

If you want a heavier or lighter mode than the default `hybrid`:

```text
[Council convened — full council. Anti-groupthink mode: adversarial-collab.]

Question: <QUESTION>

Use adversarial-collab mode. Before any consensus is logged, the council
must collectively define the falsification test: what evidence in the
next N weeks would prove this consensus wrong? If no such test can be
defined, the consensus isn't well-formed enough to log.

[Rest of standard prompt instructions apply...]
```

Other anti-groupthink modes:
- `pre-mortem` — lightweight, for time-pressured tactical calls
- `steelman` — pure substance, no past-decision context
- `hybrid` (default) — pre-mortem + steelman + reference-bound check
- `adversarial-collab` — high-stakes; produces falsification criteria

### Discovery mode (multi-session project starts)

```text
[Discovery mode: forward]

Project: <NAME>
Goal: <GOAL>

Treat any design artifact I supply as de facto Discovery output. Proceed
to early Spec tier. Operationalize, let usage surface gaps. Do NOT
backtrack to formal Discovery unless I explicitly ask for the audit trail.
```

```text
[Discovery mode: backtrack]

Project: <NAME>
Goal: <GOAL>

Pause forward work. Run the Discovery prompt at <PATH-TO-DISCOVERY-PROMPT>
and produce discovery.md before any spec or plan work.
```

### Partial council (specific voices only)

When you want input from a subset of the council:

```text
[Council convened — partial. Voices: Heimdall, Susanoo. Anti-groupthink mode: steelman.]

Question: <QUESTION>

Heimdall and Susanoo only. Speaking order: Heimdall first (architect
position), Susanoo second (challenge that position). Steelman mode:
each voice writes one sentence: "the strongest case against this is ___."
```

Use this when:
- The question is clearly within 2 voices' domains and the others would honestly abstain
- You want adversarial pressure (Susanoo) on a specific architect proposal
- Time is tight and you don't want the full council overhead

## What NOT to put in a kickoff prompt

- **Don't paste in the full COUNCIL.md content.** The session loads it from `COUNCIL.md` already (or via the chair persona's reference).
- **Don't pre-bias the voices.** "I think the answer is X — convene the council to confirm" is rubber-stamping, not deliberation. Frame the question neutrally and let the voices reason from their domains.
- **Don't invoke the heaviest mode by default.** Mode selection theater is a flagged failure mode in `COUNCIL.md`. `hybrid` is the right default for most full-council convenings.
- **Don't skip the reference-rot check at the end.** Drift accumulates silently if you do.

## Common patterns by question type

| Question type | Recommended invocation |
|---------------|------------------------|
| "Should we adopt framework X?" | Full council, `hybrid` |
| "Is this design over-engineered?" | Heimdall + Hephaestus, `steelman` |
| "Has this conflict come up before?" | Thoth solo |
| "Does this affect the publishing pipeline?" | Saraswati solo |
| "What's wrong with this proposal?" | Susanoo solo |
| "We're starting project X — full process or skip Discovery?" | Discovery mode |
| "Architectural decision: data layer choice" | Full council, `adversarial-collab` |
| "Quick scope check — too big or too small?" | Hephaestus solo |
| "We're committing to X long-term — challenge it" | Full council, `adversarial-collab` |

When in doubt: if you can name which one or two voices should weigh in, use that subset. Full council is for genuinely cross-cutting deliberations.
