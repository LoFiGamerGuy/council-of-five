# Tiebreakers — Disagreement Math

When voices disagree substantively, the council needs a resolution mechanism. Voting is the fallback; structured deliberation is preferred.

This file documents the math, the edge cases, and the human-tiebreaker pattern.

## The default: log disagreement, don't vote

Disagreement is **logged**, not voted (unless the tiebreaker math triggers).

The convening log captures the disagreement explicitly. The decision section names which position the chair adopted, with reasoning. Future re-convenings have the trail.

This is the right default because:
- Voting compresses information. The minority position contains signal that the majority didn't surface.
- Forcing a binary outcome on every disagreement converts deliberation into politics.
- The chair has authority to adopt either position; the council advises.

Voting is only triggered when the disagreement is substantive enough that the chair can't responsibly adopt either position without explicit resolution.

## When the tiebreaker math triggers

The math fires when:

- The disagreement is on a **substantive call** (not a stylistic preference, not a minor framing)
- The chair has determined that adopting one position over the other materially changes the decision
- The deliberation has run its course (additional discussion isn't surfacing new information)

Each of those conditions is a chair judgment. The council doesn't vote on whether to vote; the chair decides.

## The math

When the tiebreaker fires, the math depends on how many voices disagreed and how many remain to vote:

| Disagreeing | Non-participants | Resolution |
|-------------|------------------|------------|
| **2** | 3 | Majority vote (no tie possible — 3 votes can't tie) |
| **3** | 2 | 2-non-participant vote; tie → user tiebreaks |
| **4** | 1 | 1 non-participant casts deciding vote |
| **5** | 0 | User tiebreaks (council fully split) |

The structure: the disagreeing voices have already taken their positions. Non-participating voices vote on which position to adopt. When the vote can deadlock (3-way split with even non-participants), the user breaks the tie.

## The user override

The user can override **any** council outcome at any time. Including:
- A unanimous council consensus (the user has information the council doesn't)
- A council vote (the user has authority the council doesn't)
- A council deliberation in progress (the user can pull rank)

Override is the user's prerogative, not the council's failure mode. The council exists to surface considered positions; the user weighs them and decides.

When the user overrides, the convening log records:
- The council's recommended position
- The user's chosen position
- (Optional) the user's brief reasoning

The reasoning is optional because not every override needs justification. Sometimes the user has private context the council can't access. Recording the override without the reasoning is fine; the trail still exists.

## Edge cases

### Recusals

A recused voice doesn't vote. If Thoth recuses (no prior decision in scope) and the remaining four voices split 2-2:

| Disagreeing | Non-participants | Resolution |
|-------------|------------------|------------|
| **4** (with one recused) | 0 | User tiebreaks |

The recusal doesn't make the recused voice a non-participant for tiebreaker purposes — they're already off the floor.

### Honest abstentions

An honest abstention (`"no domain objection"`) is **not** a vote and is **not** a recusal. It means the voice considered the question and has nothing substantive to add. For tiebreaker math, treat the voice as a non-participant in the disagreement but available to vote on the tiebreaker.

Example: 2 voices disagree, 1 honestly abstained, 2 are non-participants → 3 voices vote (the abstainer + 2 non-participants).

### When the chair is part of the disagreement

The chair orchestrates but doesn't vote in the council math. The chair's role is to determine when the tiebreaker fires, structure the vote, and adopt the resolution.

If the chair has a strong personal position that disagrees with the council majority, the chair can override (using the user-override mechanism — the chair is acting as user proxy). But the chair should distinguish "I'm overriding the council" from "the council voted." Conflating them corrupts the trail.

### Escalation to a higher-tier model

If the council deadlock involves a question where one voice's position would benefit from a more capable model than the default, the chair can escalate:

- Re-invoke the deadlocked voice(s) on a higher-tier model (cross-family if the deadlock looks Anthropic-blind-spot-shaped)
- Add the escalated position to the convening transcript
- Re-run the tiebreaker with the escalated position

Escalation is rare. Most deadlocks are about framing or values, not capability — and capability escalation doesn't resolve framing disputes. Use escalation when the deadlock is genuinely "my domain analysis on this is at the limit of my model's reasoning depth."

## What "substantive disagreement" means

The bar for triggering the tiebreaker is "would adopting one position over the other materially change the decision?"

Examples that **don't** clear the bar:
- Two voices recommend slightly different framings of the same approach
- One voice prefers more detail in the convening log; another prefers less
- Aesthetic preferences about how the deliberation reads

Examples that **do** clear the bar:
- One voice says "ship it"; another says "this isn't ready"
- One voice says "use approach A"; another says "approach B is fundamentally better and A will need reworking within 6 months"
- One voice flags a hard firewall violation that another voice disputes

When in doubt, the chair errs toward NOT triggering the math — log the disagreement, adopt one position with reasoning, move on. Triggering the math is reserved for "I genuinely can't responsibly choose between these without resolution."

## What gets logged

The convening log records:

- **Each voice's position** (already required by the standard log format)
- **Whether the tiebreaker math fired** (yes / no)
- **If yes:** which voices voted on the tiebreaker, what the tally was, what the resolution was
- **If user-tiebreak:** the user's chosen position, optionally the reasoning

This trail matters for re-convenings. A future deliberation can see "we were split on this last time; here's how it resolved; here's what happened" — preventing both silent reversion and rote repetition of the prior tiebreaker.

## Failure modes

- **Voting on everything.** If the council votes on routine framing decisions, the convening becomes politics. Vote only on substantive deadlock.
- **The chair voting in council math.** The chair orchestrates; the chair doesn't vote. (The chair can override using the user-override mechanism, but that's distinct from voting.)
- **Treating the user override as the council's failure.** The override is a feature. The council surfaces positions; the user has more context.
- **Manufactured tiebreaker resolution.** Voting where the actual answer is "we need to keep deliberating, this isn't ready" — sometimes a deadlock is signal that the question isn't well-formed enough to resolve. Postpone, refine the question, re-convene.
