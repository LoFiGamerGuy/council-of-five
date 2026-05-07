# Speaking Order — Rationale

In full-council convenings, the voices speak in this order:

```
Thoth → Saraswati → Heimdall → Hephaestus → Susanoo
```

The order is deliberate. Each voice is positioned to do their best work given what came before.

## The structural argument

The order maps to a natural pipeline of questions a careful decision-maker asks:

1. **Have we already decided this?** (Thoth — Keeper)
2. **Does this affect more than one domain?** (Saraswati — Weaver)
3. **What's the right shape, given prior decisions and cross-domain reality?** (Heimdall — Architect)
4. **What's the smallest version of that shape that ships?** (Hephaestus — Smith)
5. **What's wrong with this?** (Susanoo — Challenger)

Each question is most useful with the previous questions answered.

## Why memory before design

If Thoth flags that the proposal collides with a locked decision, the rest of the council shouldn't begin. Either the proposal is a silent reversion (acknowledge it, decide to amend, then proceed) or the collision needs resolution before deliberation continues.

Putting Thoth later wastes the council's effort. Heimdall designs a shape that conflicts with a prior decision; Hephaestus trims that shape; Susanoo challenges it; only at the end does Thoth note "by the way, this contradicts ADR-007." That's a wasted convening.

Memory first means the deliberation starts on legitimate ground.

## Why cross-domain before architecture

Heimdall's job is to design the right shape. But "right" depends on what other domains the proposal touches. A design that's optimal in domain X but breaks the firewall to domain Y isn't right; it's right-in-isolation.

Saraswati surfaces the cross-domain reality before Heimdall designs. This way Heimdall's architectural position incorporates the cross-domain constraints from the start, rather than being told later that the design needs to change.

Putting Saraswati later turns architectural decisions into "design then re-design" — the second pass to accommodate the cross-domain commitments Saraswati would have surfaced earlier.

## Why architecture before pragmatism

Hephaestus's job is to find the smallest viable shape. But "smallest" requires a shape to start from. Hephaestus operating before Heimdall is trimming smoke — there's nothing concrete to make smaller.

Architecture first gives Hephaestus a concrete proposal to right-size. Hephaestus then identifies the minimal load-bearing version, the cost trajectory, the maintenance load.

Putting Hephaestus before Heimdall means the smith is asked "what's the smallest version of...?" before the architect has answered "...of what?"

## Why pragmatism before challenge

Susanoo's job is to challenge. But challenge needs something concrete to bite. Challenging a vague aspiration is bikeshedding; challenging a concrete proposal with a stated cost and a defined shape is the Challenger's actual specialty.

Hephaestus produces the concrete proposal Susanoo can challenge. The smithed version — defined shape, named cost, articulated tradeoffs — is the right adversarial target.

Putting Susanoo earlier means the Challenger is reaching for objections to a moving target. Susanoo's strongest steelman comes when the proposal is concrete enough to have a strongest objection.

## Why Susanoo last

Susanoo is the council's final pass. By the time Susanoo speaks, the proposal has:
- Cleared memory (Thoth)
- Cleared cross-domain commitments (Saraswati)
- Been shaped (Heimdall)
- Been right-sized (Hephaestus)

Susanoo now asks: given all of that, what's still wrong? What assumption hasn't been named? Where would this fail?

This is the Challenger's home turf. The proposal is mature enough that the strongest objections are visible, and Susanoo has the structural authority to name them without being dismissed as premature.

If the council reaches Susanoo and Susanoo honestly abstains (`"no domain objection"`), that's a strong signal: a proposal that has cleared four substantive checks AND the Challenger's adversarial pressure is mature.

## What if the order doesn't fit?

The order is the default for full-council convenings. Variants exist:

- **Single-voice mode** — only one voice speaks. No order question.
- **Partial council** — a subset of voices speak. Apply the speaking-order priority within the subset (lower-numbered voices speak first).
- **Adversarial-collab mode** — Susanoo participates throughout, not just at the end, because the council collectively defines the falsification criteria. Other voices keep their normal positions.

The order is structural, not performative. If you find yourself convening voices in a different order for a recurring class of question, that's signal — either the question doesn't fit the council pattern, or the order needs revisiting in COUNCIL.md.

## What about ties for "first"?

Sometimes Thoth has nothing to add — there's no prior decision in scope. The honest abstention pattern handles this:

```
voice: thoth
voice_position: "no prior decision found in scope. References checked:
                 [list]. No silent reversion. Proposal is on green ground
                 from a memory perspective."
```

This is *not* the same as Thoth not speaking. The abstention is a positive statement that Thoth checked. Saraswati then proceeds with the cross-domain analysis, with Thoth's confirmation that there's no memory collision to factor in.

Skipping Thoth entirely is a failure mode (silent reversion goes uncaught). The check happens; sometimes it returns "all clear." That's the order working correctly.
