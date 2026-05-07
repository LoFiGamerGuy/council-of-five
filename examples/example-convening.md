# Convening 001 — Should we add a feature flag system to the project?

**Date:** 2026-05-07
**Convened by:** Chair
**Mode:** full council
**Anti-groupthink mode:** hybrid
**Trigger:** scope shift (introducing a new infrastructure layer)
**Stakes:** medium

---

## Question

Should we add a feature flag system to the project, or continue using environment variables for runtime configuration?

## Voices participating

All five voices participated. None recused.

## Trace

### Thoth (Keeper)

References checked: `docs/decisions.md` ✓, `docs/adr/` ✓, prior convening logs ✓.

No prior decision in scope. The closest prior decision is ADR-003 (env-var-driven configuration), which is still in force. Introducing a feature flag system would not contradict ADR-003 — feature flags are typically a layer *above* env vars, not a replacement — but it would add a new architectural surface that ADR-003 doesn't anticipate.

If the council adopts a feature flag system, the convening log produces an effective amendment to ADR-003's scope. Recommend explicit ADR for the new system rather than letting it evolve as a silent extension of ADR-003.

`silent_reversion_flagged: no`

### Saraswati (Weaver)

Cross-domain commitments file consulted (`cross-domain-commitments.local.md`, last updated 2026-04-15).

Domains touched: **Engineering** (primary), **Operations** (secondary — feature flags affect deployment workflows). No collisions with other domains.

The feature flag system would introduce a new artifact (the flag config) that operations would need to maintain. This is a non-trivial cross-domain commitment — engineering ships flags, operations manages them, and the boundary needs to be clear from day one. Not a blocker, but a coordination requirement.

`firewall_violations: none`
`collisions_flagged: 1 (eng/ops coordination)`

### Heimdall (Architect)

The architectural question isn't "feature flags or env vars" — it's "what kind of runtime configuration surface do we want long-term." Three shapes:

1. **Static config (current)** — env vars set at deploy time. Simple, audit-friendly, no runtime mutability.
2. **Feature flags** — runtime-mutable flags, typically with targeting (per-user, per-percentage, per-environment).
3. **Full configuration system** — config service with hot-reload, schema validation, audit trail.

The proposal as stated implies (2). But (2) is on a slope toward (3). If we adopt feature flags, the next request will be "can we target by user," then "can we audit who flipped what when," then we're at (3) without having decided to be there.

Recommend either committing to (2) explicitly with bounded scope (no per-user targeting in v1) OR going to (3) with eyes open. Drift between them is the failure mode.

References: ADR-003 (env-var configuration), `docs/specs/runtime-config.md` (none currently exists; would need to author one).

### Hephaestus (Smith)

Three-cost-level analysis:

| Shape | Build cost | Maintenance cost | Value |
|-------|------------|------------------|-------|
| **Minimum** (boolean flags only, file-based, no UI) | ~3 days | low (file edits + redeploy) | covers 80% of expected use |
| **Reasonable** (boolean + percentage flags, file-based, simple CLI to flip) | ~1 week | low-medium | covers 95% of expected use |
| **Maximum** (per-user targeting, web UI, audit log) | ~3-4 weeks | medium-high | covers 100% but most never used |

The "minimum" shape is a small enough investment that it can be reversed if it doesn't pay off. The "reasonable" shape is right-sized for the team's current scale. The "maximum" shape is over-engineered for current needs.

Recommend "reasonable" — boolean + percentage, file-based, simple CLI. Defer per-user targeting and web UI until there's a concrete use case requesting them.

`cost_estimate: 1 week engineering, low ongoing maintenance`

### Susanoo (Challenger)

Strongest case against this proposal: **feature flags are infrastructure debt that grows.**

Specifically:
1. Every feature flag added is a permanent code path that must be maintained until the flag is removed. Flags don't get removed; they accumulate. Within 18 months we'll have 50 flags, and removing any of them will be scary because we don't know what depends on them.
2. The "minimum" Hephaestus proposed will inevitably grow toward "maximum" because each request for a small feature ("just per-environment targeting") sounds reasonable in isolation.
3. There's a cheaper alternative we haven't seriously considered: using feature branches and progressive rollouts via deployment, rather than runtime flags. This handles 80%+ of "feature flag" use cases without adding the runtime configuration surface.

Honest assessment: the proposal has a real value (decoupling deploy from feature release), but the cost trajectory is worse than the proposal acknowledges. If we adopt feature flags, we should build in flag-removal hygiene from day one (every flag has a deletion deadline).

`substance_check: proposal does NOT survive challenge as currently scoped. Either tighten scope significantly OR consider feature-branch alternative seriously.`

## Anti-groupthink output (mode: hybrid)

### Pre-mortem

- **Thoth:** "It's six months out. We adopted feature flags as a small infrastructure layer; flag count grew to 30; nobody remembers why half of them exist; removing flags became scary because of dependency uncertainty."
- **Saraswati:** "It's six months out. Engineering ships flags freely; operations didn't get the coordination it needed; flags get flipped in production by people who don't fully understand the downstream effects."
- **Heimdall:** "It's six months out. We adopted (2); usage drifted toward (3); we're now operating a half-built configuration service with none of the audit, validation, or schema guarantees that (3) would have provided."
- **Hephaestus:** "It's six months out. We built the 'reasonable' shape; per-user targeting was added in month three; web UI was added in month five; we're at maximum cost without the deliberate choice to be there."
- **Susanoo:** *no domain objection — pre-mortem is structurally what I'd say in steelman; honest abstention to avoid double-counting.*

### Steelman

- **Thoth:** "The strongest case against is: we have no prior decision recommending feature flags, and the closest prior decision (ADR-003) was deliberately conservative about runtime mutability."
- **Saraswati:** "The strongest case against is: this introduces a cross-domain coordination requirement that hasn't been agreed to with operations."
- **Heimdall:** "The strongest case against is: feature flags are a slippery slope to a half-built configuration service. Either don't start, or commit to the full thing with eyes open."
- **Hephaestus:** "The strongest case against is: feature branches + progressive deployment cover 80%+ of the use cases without the runtime configuration surface."
- **Susanoo:** *(restated above)* "Feature flags are infrastructure debt that grows."

### Reference-bound check (Thoth)

ADR-003 ✓ — still in force; current proposal would amend its scope; recommend explicit new ADR rather than implicit amendment.

`silent_reversion_flagged: no` (the proposal does not silently revert ADR-003)

## Decision

**Consensus: held with hard condition.**

Adopt the "reasonable" shape (boolean + percentage flags, file-based, simple CLI) **with the following hard conditions:**

1. **Flag deletion deadlines.** Every flag added MUST have a deletion deadline (typically 90 days). Flags that miss their deadline trigger a review.
2. **Scope lock.** No per-user targeting in v1. No web UI. Adding either requires a new convening.
3. **Operations coordination.** Before implementation begins, document the eng/ops boundary in `docs/specs/feature-flags.md`. Operations confirms.
4. **Authoring an ADR.** Adoption produces a new ADR explicitly amending ADR-003's runtime mutability stance. Without the ADR, this convening is silent amendment — flagged failure mode.
5. **Re-evaluation trigger.** Convening 005 (or three months from now, whichever first) reviews flag count and removal rate. If flags are accumulating without being removed, the system is failing — discontinue or restructure.

Susanoo's hard condition (#1) is the load-bearing one. Without flag deletion hygiene, the proposal's six-month failure mode (Thoth's pre-mortem) is near-certain.

## Follow-ups

- [ ] Author ADR-019 amending ADR-003 (Owner: Heimdall + Chair, this week)
- [ ] Document eng/ops coordination boundary in `docs/specs/feature-flags.md` (Owner: Saraswati + Chair, before implementation)
- [ ] Implement minimum viable feature flag system per Hephaestus's "reasonable" shape (Owner: Hephaestus + executor, ~1 week)
- [ ] Set re-evaluation trigger: convening 005 OR 90 days, whichever first
- [ ] Add flag deletion hygiene to the implementation: every flag tracked with creation date + deletion deadline

## Reference-rot check

- `docs/decisions.md` ✓
- `docs/adr/ADR-003-env-var-configuration.md` ✓
- prior convening logs ✓ (convenings/ is empty — this is convening 001)
- `cross-domain-commitments.local.md` ✓
- `docs/specs/runtime-config.md` ⚠ MISSING — to be authored as part of follow-ups

---

## Notes on this example

- **Why the example was a feature flag system:** common, concrete, and the council's full apparatus (memory check, cross-domain check, architectural shape, pragmatic sizing, adversarial challenge) all have clear targets.
- **Why "consensus held with hard condition" rather than "consensus held":** the proposal as initially framed had real risks (Susanoo's challenge was substantive). The hard condition (flag deletion hygiene) is the load-bearing addition that makes the proposal robust.
- **Why honest abstention by Susanoo in pre-mortem:** the steelman section captures Susanoo's substantive challenge. Restating it in pre-mortem would be double-counting. Honest abstention with reasoning is the correct response.
- **Why an ADR follow-up:** without the ADR, this convening would be a silent amendment of ADR-003. Explicit amendment is mandatory for locked-decision changes.
- **Why a re-evaluation trigger:** every "consensus held with hard condition" should have a trigger that re-examines the decision. Without one, hard conditions decay into soft suggestions.

This example is illustrative. Real convenings vary in length, depth, and shape. The structure (header → question → voices → anti-groupthink → decision → follow-ups → reference check) is consistent.
