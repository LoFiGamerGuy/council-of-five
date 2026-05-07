# Convening NNN — <Topic>

**Date:** YYYY-MM-DD
**Convened by:** Chair
**Mode:** <full council | single voice | partial>
**Anti-groupthink mode:** <pre-mortem | steelman | hybrid | adversarial-collab | n/a>
**Trigger:** <ADR | locked-decision challenge | scope shift | multi-domain move | other>
**Stakes:** <low | medium | high>

---

## Question

<One-sentence framing of the question. If you can't write it in one sentence, the question isn't well-formed enough to convene on.>

## Voices participating

<List the voices that spoke. Mark recusals: "Saraswati — recused (single-domain question)".>

## Trace

### Thoth (Keeper)
<Two to four sentences. Memory check: have we already decided this? Does it collide with a locked decision? Cite specific files / ADRs / prior convenings.>

### Saraswati (Weaver)
<Two to four sentences. Cross-domain check: does this affect domains beyond the obvious one? Cite cross-domain-commitments.md sections if relevant.>

### Heimdall (Architect)
<Two to four sentences. Design shape given prior decisions and cross-domain reality.>

### Hephaestus (Smith)
<Two to four sentences. Smallest version that ships. Budget realistic? Three-cost-level analysis if useful.>

### Susanoo (Challenger)
<Two to four sentences. What is wrong? What assumption hasn't been named? Where would this fail?>

<Adjust the trace to reflect actual speaking — voices that recused don't appear here. Voices that contributed nothing substantive say "no domain objection" — that's honest abstention, NOT manufactured dissent.>

## Anti-groupthink output (mode: <chosen>)

<Skip this section if the call wasn't a unanimous-consensus moment. Otherwise:>

- **Pre-mortem** — <each voice's failure-mode hypothesis, or "no domain objection">
- **Steelman** — <each voice's strongest case against, or "no domain objection">
- **Reference-bound check** (Thoth) — <conflict with locked decisions / ADRs? yes / no / partial>

<Decision can be one of:>
- **Consensus held** — challenged, no substantive objection surfaced. Logged.
- **Consensus broken** — anti-groupthink surfaced a real objection. Re-deliberate.
- **Consensus held with condition** — challenged-and-held, but with a Susanoo-style hard condition that triggers if violated.

## Decision

<One paragraph max. The actual decision and its scope. If conditional, state the condition explicitly.>

## Follow-ups

- [ ] <Concrete action item with owner if possible>
- [ ] <Concrete action item>
- [ ] <Re-evaluation trigger — when do we revisit this decision?>

## Reference-rot check

<List the references cited above and note whether they resolved at convening time:>

- `<path>` ✓
- `<path>` ✓
- `<path>` ⚠ MISSING — <action taken>

---

## Template usage notes

- Filename: `<YYYY-MM-DD>-<topic-slug>.md` in `convenings/`
- Topic slug should be 2-4 words, hyphenated, descriptive (e.g., `convening-log-structure`, `add-saraswati-reference`, `wsl-bridge-upgrade`)
- Numbering (`Convening NNN`) is sequential — check the latest log to get the next number
- Total length should be ~50 lines for a typical convening; longer is OK for major architectural calls
- Honest abstention is non-negotiable: do not invent dissent or manufacture failure modes if a voice has nothing substantive
- Reference-rot check is mandatory; skip it and you let drift accumulate silently
