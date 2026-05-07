# Modes — Deep Dive

Two mode catalogs apply to council operation:

- **Anti-groupthink modes** — used when consensus needs structural challenge. Replaces "manufactured dissent."
- **Discovery modes** — used at the start of a multi-session project.

Modes are selectable per-call. The default selections handle most situations; override when the situation warrants.

---

## Anti-groupthink modes

Used **only when all five voices agree on a non-trivial call**. The premise: unanimous consensus on an important question is suspicious until tested. Not because consensus is wrong, but because the *path* to consensus might have been groupthink.

The modes vary by depth and cost. Pick the lightest one that adequately tests the consensus.

### `pre-mortem`

**Mechanism:** Each voice writes one sentence: *"It's six months out and this failed disastrously. From my domain, the failure was ___."*

**Source:** Klein, Gary. *"Performing a Project Premortem,"* Harvard Business Review, September 2007.

**Cost:** Low. Five sentences total.

**When to use:**
- Routine consensus checks where you want a quick failure-mode probe
- Time-pressured tactical calls where heavier modes are too expensive
- Decisions where the failure modes are likely well-known to each voice

**What it catches:** Failure-mode blindness. Each voice projects forward from their domain's typical failure patterns. If a voice can't name a plausible failure, that's information — either the proposal is unusually robust in that domain, or the voice doesn't have visibility.

**What it doesn't catch:** Silent reversion of prior decisions (Thoth's domain), groupthink that has consistent assumptions across domains (the failure modes might all share the same blind spot).

### `steelman`

**Mechanism:** Each voice writes one sentence: *"The strongest case against this, from my domain, is ___."*

**Cost:** Low. Five sentences total.

**When to use:**
- Pure substance questions where past-decision context isn't load-bearing
- When you want adversarial pressure but `pre-mortem`'s "imagine future failure" framing feels off
- When Susanoo is recused or unavailable and you want challenge from the other voices

**What it catches:** Weak proposals. The steelman forces each voice to engage with the *strongest* objection from their domain — not strawmen. If the strongest objection is weak, the proposal is robust in that domain.

**What it doesn't catch:** Failure modes the voices haven't *thought* about (which `pre-mortem` is better at surfacing because of its forward-projection framing).

### `hybrid` *(default)*

**Mechanism:** Pre-mortem + steelman + Thoth's reference-bound check (verify all cited references resolve and say what the proposal claims they say).

**Cost:** Medium. Roughly 15 sentences plus the reference walk.

**When to use:**
- **Default for ADR-level decisions, scope shifts, anything load-bearing.**
- When you want both failure-mode probing AND substance challenging
- When silent reversion is a plausible risk

**What it catches:** Failure-mode blindness AND silent reversion AND weak proposals AND reference rot. The combination is more thorough than any single component.

**Why this is the default:** most full-council convenings are load-bearing enough to warrant medium-cost discipline. `pre-mortem` alone is too narrow; `adversarial-collab` is too heavy for routine ADRs. Hybrid is the right size for most cases.

### `adversarial-collab`

**Mechanism:** The council collectively defines the falsification test BEFORE the consensus is logged: *"What evidence in the next N weeks would prove this consensus wrong?"* If the council can't define one, the consensus isn't well-formed enough to log.

**Source:** Kahneman, Daniel and Klein, Gary. *"Conditions for Intuitive Expertise: A Failure to Disagree,"* American Psychologist, 2009.

**Cost:** High. Requires full council engagement plus collaborative drafting of the falsification criteria.

**When to use:**
- **High-stakes commitments with measurable downstream effects**
- Decisions you'll be living with for 6+ months
- Anything that warrants an ADR with evidence-update criteria
- When you suspect the consensus might be premature but can't articulate why

**What it catches:** Consensus that *feels* right but isn't well-formed enough to be testable. Forcing the council to articulate "what would prove this wrong" surfaces decisions that are aspirations dressed as commitments.

**What it produces:** A decision record with built-in falsification criteria. When the criteria fire (or don't), you have a structured signal about whether to revisit.

**Costly failure mode:** "We can't think of what would prove this wrong" treated as evidence the decision is robust. That's actually evidence the decision isn't well-formed — fix the formulation, then re-test.

### Default selection logic

| Situation | Mode |
|-----------|------|
| Routine consensus check | `hybrid` |
| Time-pressured tactical call | `pre-mortem` |
| Pure substance question, no past-decision context | `steelman` |
| Anything that warrants an ADR | `adversarial-collab` |

When in doubt, use `hybrid`. Erring toward heavier modes is mode selection theater — the heaviest mode "feels" most rigorous, but rigor mismatched to the question is its own failure mode.

### The honest abstention rule (applies to all modes)

If a voice has nothing substantive to add, the canonical response is `"no domain objection"`. This is structural, not performative. Manufactured dissent is forbidden.

The pattern:

```
voice: <name>
voice_position: "no domain objection — proposal survives challenge from
                 [list of categories considered]"
```

The categories list is required for honest abstention. Without it, the abstention reads as "I didn't check." With it, the abstention is a positive statement that the voice considered the relevant categories and found nothing.

---

## Discovery modes

Used at the start of a multi-session project. The user picks, or the chair picks per the heuristics.

The Discovery question: do we need formal Discovery (the four-tier methodology's Discovery → Spec → Plan → Execute), or can we proceed directly from a user-supplied design artifact?

### `forward` *(default)*

**Mechanism:** Treat any user-supplied design artifact as de facto Discovery output. Proceed to early Spec tier. Operationalize, let usage surface gaps.

**When to use:**
- The user has clear answers to the Discovery questions
- A structured Discovery process would mostly produce post-hoc rationalization of decisions already made
- Most common case for experienced practitioners

**What it skips:** The audit trail of "here's what we considered, here's what we decided, here's why." If the user genuinely knows the answers, the audit trail adds bureaucratic overhead without adding decision quality.

**What it risks:** The user *thought* they had clear answers but actually had three unstated assumptions. `forward` mode operationalizes those assumptions; usage surfaces them eventually. Sometimes this is fine; sometimes it costs a re-architecture.

### `backtrack`

**Mechanism:** Pause forward work. Open a fresh session at the project directory, run the Discovery prompt, produce `discovery.md`. Re-derive the design artifact from it.

**When to use:**
- Audit trail is load-bearing (regulatory, compliance-touchy projects)
- The user signals genuine uncertainty about the design they handed over
- The project is high-stakes enough that a wrong start is costly to recover from
- Past projects of this shape have benefited from formal Discovery

**What it costs:** Time. Discovery typically takes one focused session. Spec, Plan, Execute follow.

**What it produces:** A clean audit trail. The decisions in `spec.md` and `plan.md` trace back to questions answered in `discovery.md`. When the project is later challenged ("why did you decide X?"), the trail is there.

### Default selection logic

| Situation | Mode |
|-----------|------|
| User supplied a coherent design artifact | `forward` |
| User said the skip was unintentional and wants to see what Discovery would surface | `backtrack` |
| Project is high-regulatory or compliance-touchy | `backtrack` (for the trail) |
| Past projects of similar shape have benefited from Discovery | `backtrack` |
| Most other cases | `forward` |

### Mode invocation syntax

```
[Discovery mode: forward]
[Discovery mode: backtrack]
```

Place this at the top of the kickoff prompt for a new project.

### What `forward` is not

`forward` mode does NOT mean "skip the chair's normal session-start discipline." The chair still re-reads context, checks for handoff docs, identifies divergences from established architecture. `forward` only changes the Discovery → Spec sequencing.

What `forward` skips is the *separate session* dedicated to Discovery. The chair still asks the implicit Discovery questions ("what's the goal? what's in scope? what's out of scope? what would success look like?") — they just get answered in the design artifact the user supplied, not in a fresh `discovery.md`.

If the user-supplied design artifact doesn't answer those questions, the chair flags it and recommends `backtrack`.

---

## Mode selection theater

A flagged failure mode in `COUNCIL.md`: picking the heaviest mode just because heavier feels more rigorous.

Examples:
- Defaulting to `adversarial-collab` for routine ADRs that `hybrid` would handle
- Defaulting to `backtrack` Discovery when the user has clearly thought through the design
- Convening the full council for single-voice questions because "more perspective is more rigorous"

The cost is real: heavier modes consume tokens, time, and attention. Mode mismatched to the question is friction, not rigor. A council that defaults to its heaviest tools is a council that will be invoked less often, and avoiding the council on borderline questions costs more than mode selection theater saves.

The heuristic: pick the lightest mode that adequately handles the situation. If you find yourself reaching for the heaviest mode "to be safe," check whether the situation actually warrants it.
