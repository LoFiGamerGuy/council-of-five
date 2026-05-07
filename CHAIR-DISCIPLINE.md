# Chair Discipline

The Chair is the orchestrator. The council advises; the Chair acts. This file documents the discipline the Chair applies when handing work between sessions, between voices, and between the council's deliberation and the actual work being done.

The full discipline includes registry management, falsification clocks, and amendment protocols that emerge in long-running multi-session use. This file covers the load-bearing principles. The rest is for you to develop as your usage matures.

## The four-step pre-handoff protocol

When the Chair authors any handoff (a kickoff prompt, a convening summary that an executor will act on, an instruction that crosses a session boundary), four steps apply:

### 1. Authoritative read

Every dependency named in the handoff must be read **this session**. Reading-from-memory is not reading. The voices may be wrong about what a referenced file currently says; check.

This is the single most common Chair failure mode. The Chair "remembers" what a file said three sessions ago, references it confidently in the handoff, and the file has changed since.

### 2. Paste-isolate test

Strip chat-side prose from the handoff. The handoff alone — the file an implementer will read in a fresh session with no shared context — must suffice for them to execute correctly.

If the handoff requires the implementer to remember "what we talked about earlier in this conversation," it's not a handoff. It's a reminder for someone who shares your context. A fresh implementer will read only what's in the handoff file.

### 3. Self-contradiction scan

No instruction in the handoff contradicts any dependency artifact. If COUNCIL.md says "single voice for execution work" and the handoff instructs an executor to convene the full council before each commit, that's a contradiction — fix one before sending.

This is Thoth's silent-reversion check applied at the handoff boundary, not just at the council deliberation boundary.

### 4. First-occurrence registration check

If the handoff introduces new vocabulary, new amendments, new banned terms, or new register-discipline rules — content that future Chairs (including future-you) will be expected to honor — register it. A registry entry in the same commit, in a known location, that future Chairs read at session start.

Without this, locked-decision content creates "remember this" obligations that have no enforcement mechanism. They get forgotten. The decision becomes a silent ghost.

## When the Chair authors a handoff to themselves

Special case: when you (the Chair) author a kickoff in session N and you (the same Chair) execute it in session N+1, the standard chair → fresh-implementer asymmetry collapses.

Discipline:

- **Read with implementer-side rigor, not chair-side rigor.** Read every dependency afresh. Cross-check locked-content claims via string comparison, not memory.
- **Repeat Step 3 (self-contradiction scan) at each chair-amendable boundary** during execution — pre-commit; pre-amendment; pre-convening. Not just at session entry.
- **High-stakes self-handoffs** (architectural amendments, schema changes, anything that establishes or modifies locked content) deserve the discipline of a fresh-session implementer review. Open a fresh session, paste the handoff, see if it executes cleanly.

## Citation-only discipline for locked content

When a handoff (or a council deliberation) needs to reference locked content — committed architectural decisions, registered amendments, pinned schemas — **cite the registry, never restate the content**.

Reasons:

- Restated content drifts from the registry. The registry says X; the restated version says X' (close but different); future readers can't tell which is canonical.
- Restated content silently amends. A handoff that "summarizes" the locked content has implicitly proposed an amendment without going through the amendment process.
- Citation is auditable. Restatement is not.

Pattern:

```
✓ "Per registry entry LCR-019 (locked-content registry), the workflow uses..."
✗ "The workflow uses [restated content]. (As you'll recall, this was decided last week.)"
```

## In-flight modification rule

Any chair-side correction or extension to a handoff updates the file before the response sends. Chat-side prose alone is not a valid modification.

If the chair sends a handoff and then realizes "oh wait, also do X" in chat after the file is sent, X must be added to the file (and re-sent or the file path re-cited). Otherwise the implementer reads the original file — without X — and X is lost.

## Reference rot

References age. A handoff that cites `path/to/file.md` is making a claim that the file exists and contains the claimed content. Both can become false silently.

Discipline:

- The reference-rot check at convening close (see [`templates/convening-log.md`](./templates/convening-log.md)) is mandatory.
- If a Chair-authored handoff references files that have moved or changed, the handoff itself is corrupt. Fix before sending.
- Periodic reference audits across the council corpus (every N convenings) catch the rot the per-convening check misses.

## Amendments to this file

This file describes principles. The principles are stable; the operational details (registry naming, audit cadence, amendment format) emerge from your usage.

If you find that one of the four pre-handoff steps doesn't fit your workflow, change it deliberately — don't drift away from it silently. The version section below tracks the changes.

## Version

- v1.0 — May 2026 — initial public release. Distilled from longer-form internal chair discipline that emerged in multi-month operation. The longer form contains additional registry management, falsification-clock, and amendment-protocol details that are workflow-specific; develop those as your usage matures.
