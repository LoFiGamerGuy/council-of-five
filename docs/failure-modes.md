# Failure Modes

The patterns that kill conventions. Each one is a failure mode I've encountered or that's predictable from the structure. Surface them, name them, and the discipline survives.

## Council theater

**Symptom:** Invoking five voices for one-voice work because "more rigorous."

**Why it happens:** Heavier feels safer. The full council is the council's most visible operation; using it for trivial questions feels diligent.

**Why it's a failure mode:** It burns tokens, time, and attention. Worse: when convening becomes routine for trivial questions, the signal of "this is a real convening" degrades. Future convenings carry less weight because all convenings are noise.

**Recovery:** Default to single-voice. Convene the full council only when one of the documented triggers fires (ADR, locked-decision challenge, scope shift, multi-domain move). When in doubt, single-voice. The full council is a tool, not a posture.

---

## Persona narration replacing actual deliberation

**Symptom:** Voices produce in-character flourish ("As Heimdall, I see the architectural shape of this question is...") without substance.

**Why it happens:** The persona names invite literary performance. Models default to "embodying the persona" when the prompt suggests it.

**Why it's a failure mode:** Performance crowds out substance. The persona is a *role*, not a character. Heimdall's value is the architectural perspective, not the in-character voice.

**Recovery:** Persona prompts emphasize *function* over *character*. The voice files in this repo are written to that standard — Heimdall is "the long-horizon designer," not "Heimdall the watcher of Asgard." If a voice's outputs are reading as in-character performance, edit the persona prompt to remove the literary framing and re-emphasize the functional role.

---

## Drift over long sessions

**Symptom:** After many turns in a session, the council starts to behave differently than the canonical methodology says it should. Speaking order shifts; tiebreaker rules get bent; honest abstention gets replaced with manufactured dissent.

**Why it happens:** Models lose calibration on the framework over a long session. The original `COUNCIL.md` content is in the prompt prefix but isn't being attended to as the active context grows.

**Why it's a failure mode:** Drift is silent. The council *thinks* it's still operating per the framework but actually isn't. Silent drift is worse than overt failure because it doesn't trigger correction.

**Recovery:**
- Periodic self-audit: at long-session boundaries, the chair re-reads `COUNCIL.md` and verifies recent convenings adhere to the structure.
- Convening log review: spot-check whether recent convenings cite the framework consistently. If they don't, drift is happening.
- Hard reset: in a fresh session with the original `COUNCIL.md` reloaded, run a calibration convening on a known-shape question. Compare to expected output.

---

## Reference rot

**Symptom:** A voice cites a file or decision ID that doesn't resolve, or that has changed since the cite.

**Why it happens:** References age. Files move. Decisions get amended. The council's references aren't automatically maintained.

**Why it's a failure mode:** A deliberation built on stale references is built on sand. The council *thinks* it's grounded in the cited material but isn't.

**Recovery:**
- Thoth's reference-bound check at convening close (mandatory in `hybrid` and `adversarial-collab` modes)
- Periodic reference audits across the council corpus (every N convenings, walk every reference, verify resolution)
- Convening log header includes a reference-rot check section — if it's missing, the convention isn't being followed

---

## Mode selection theater

**Symptom:** Defaulting to the heaviest mode (`adversarial-collab`, `backtrack`) when a lighter mode (`hybrid`, `forward`) fits.

**Why it happens:** Heavier modes feel more rigorous. The temptation is to over-invoke for safety.

**Why it's a failure mode:** Cost mismatched to question is friction. When the heaviest mode is the default, the council gets convened less often (because each convening is expensive), and avoiding the council on borderline questions costs more than the mode selection theater saves.

**Recovery:** Pick the lightest mode that adequately handles the situation. `hybrid` is the right default for most full-council convenings. Reach for `adversarial-collab` only when the decision is genuinely high-stakes with measurable downstream effects. Reach for `backtrack` only when audit trail is load-bearing.

---

## Convening log archaeology

**Symptom:** Convening logs are written but never read.

**Why it happens:** The discipline of writing the log feels like the work; reading old logs feels like overhead.

**Why it's a failure mode:** The whole point of logs is consultation at re-convening. Logs that aren't read don't prevent silent reversion. They become artifacts, not load-bearing references.

**Recovery:**
- Hard rule: any related re-convening MUST consult prior convening logs. If consultation discipline lapses, the convention dies.
- Periodic audit: check whether recent convenings cite prior convening logs. If they don't, either the convenings are unrelated (fine) or consultation has degraded (fix).
- Susanoo's veto pattern: at convening 005 (or whatever your fifth-ish convening is), review whether logs are earning their keep. If they aren't, either fix the consultation pattern or stop writing them.

---

## Manufactured dissent

**Symptom:** A voice produces objections that aren't substantive, just to populate an anti-groupthink output.

**Why it happens:** The mode prompt asks for an objection. The voice doesn't have one. Generating a placeholder feels like compliance.

**Why it's a failure mode:** Manufactured dissent corrupts the signal. Honest abstention (`"no domain objection"`) is structural; manufactured objection is noise. Future convenings can't distinguish real concerns from filler.

**Recovery:** Honest abstention is the only valid escape. The persona prompts in this repo make this explicit and require the voice to name the categories considered. If a voice consistently manufactures objections, edit the persona prompt to strengthen the abstention pattern.

---

## The chair as one of the voices

**Symptom:** The chair takes a strong position in deliberation rather than orchestrating.

**Why it happens:** The chair has opinions. The temptation to weigh in is real.

**Why it's a failure mode:** When the chair becomes a participant, the council's structure breaks. The chair can't be both moderator and contestant.

**Recovery:** The chair orchestrates. If the chair has a position, that position is recorded as the user's position (the chair acts as user proxy). The council deliberates; the chair adopts; if the chair's position diverges from the council's, the override is logged.

---

## Skipping voices because "they wouldn't have anything to add"

**Symptom:** The chair convenes a "partial" council, omitting voices the chair predicts will honestly abstain.

**Why it happens:** Saving time and tokens. If Thoth would clearly abstain (genuinely new design work), why convene Thoth?

**Why it's a failure mode:** The chair's prediction of "would honestly abstain" is sometimes wrong. Voices catch things the chair doesn't expect. Systematically skipping voices because of predicted abstention is a slow degradation toward "the chair only convenes voices the chair already agrees with."

**Recovery:** For full-council triggers (ADRs, locked-decision challenges, scope shifts, multi-domain moves), convene the full council. The cost of including a voice that genuinely abstains is small (`"no domain objection"` is one line); the cost of skipping a voice that would have caught something is large.

For non-trigger questions, single-voice mode is correct, but the choice of *which* voice should be guided by the speaking-order priority, not by chair preference.

---

## "It worked once so it must always work"

**Symptom:** A particular convening pattern produced a great outcome; the chair starts using that pattern as default for similar-feeling questions.

**Why it happens:** Pattern reinforcement. Success calibrates toward repeating what worked.

**Why it's a failure mode:** Patterns are context-specific. The pattern that worked for one decision might be inappropriate for the next decision that "looks similar." Without re-evaluating the situation, the chair anchors on the prior pattern when fresh deliberation would surface different needs.

**Recovery:** At each convening, evaluate the situation fresh: which voices' domains are touched, which mode fits, what the right question is. Use prior conventions as priors, not commitments. When something is genuinely different about this question, adjust.

---

## Diagnosis pattern

When you suspect the council is failing, check in this order:

1. **Are convenings happening?** If the council isn't being convened when triggers fire, that's not a council failure mode — that's not using the council. Calibrate convening triggers.
2. **Is the speaking order being followed?** If voices are speaking out of order, drift is happening.
3. **Are voices honestly abstaining when appropriate?** If every voice has a substantive position on every question, manufactured dissent is happening.
4. **Are convening logs being consulted at re-convening?** If not, the logs are archaeology.
5. **Are references being checked?** If reference rot is silent, eventually a major decision will be built on stale ground.
6. **Are mode selections matching question stakes?** Mode selection theater is the most subtle failure mode.

The council survives by the discipline being maintained. None of the mechanisms are self-enforcing. Periodic explicit audit is the only protection.
