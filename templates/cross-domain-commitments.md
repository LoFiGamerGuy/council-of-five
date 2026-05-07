# Cross-Domain Commitments — Saraswati's Reference (Public Structure)

**Owner:** Saraswati (council Weaver)
**Purpose:** Single source of truth for active commitments across the user's domains. Used by Saraswati to detect cross-domain collisions before any council decision lands.
**Status:** Public template structure. Personal data — if any — lives in `cross-domain-commitments.local.md` (gitignored).

---

## How this file works

This file is the **tracked, public** version of cross-domain commitments. It carries the structure but no environment-specific data. It's safe to push to any remote.

Saraswati's loading priority:

1. If `cross-domain-commitments.local.md` exists → use it as the primary reference (real data)
2. Otherwise → use this file (structure only; operate in degraded mode)

For Ryan's environments: `cross-domain-commitments.local.md` carries the real data and overrides this file.

For any fresh clone: copy this file to `cross-domain-commitments.local.md` (or directly populate this file in environments where privacy isn't a concern) and fill in the domains.

> **Discipline:** Whichever file Saraswati ends up reading, the rule is: do NOT duplicate canonical content. Carry one-line summaries plus authoritative citations. When in doubt, follow the citation.

---

## Setup (for fresh environments)

1. Identify your domains. The default council assumes 3-5. Examples:
   - Engineering / platform / product domains
   - Personal / family / health
   - Business / legal / financial
   - Creative / publishing / IP
2. For each domain, fill in: canonical source path, hard commitments (locked decisions, deadlines, firewalls), active deliverables, anything else that would surprise a future-you who forgot.
3. Section §6 (collision map) is the load-bearing section. It's what Saraswati actually exists to maintain.

---

## 1. Domain A — <NAME>

**Canonical:** `<path-to-canonical-source>`
**State:** <one-line current state>

### Hard commitments (load-bearing)
| Commitment | Source | What it commits to |
|---|---|---|
| <e.g., specific architectural lock> | <ADR-XXX or doc> | <what it locks in> |

### Active deliverables / deadlines
- <Deliverable 1 with date>
- <Deliverable 2 with date>

---

## 2. Domain B — <NAME>

**Canonical:** `<path>`
**State:** <one-line>

### Hard firewalls (project-fatal if violated)
- <Firewall rule 1>
- <Firewall rule 2>

### Active state
- <Item 1>
- <Item 2>

---

## 3. Domain C — <NAME>

<Same structure>

---

## 4. Domain D — <NAME>

<Same structure>

---

## 5. Domain E — <NAME>

<Same structure>

---

## 6. Cross-domain interactions (collision map)

This is what Saraswati actually exists to maintain. List every place where two of your domains touch — those are the collisions to watch.

| Cross-domain commitment | Where it touches | Collision risk |
|---|---|---|
| <Domain A → Domain B coupling> | <specific files / decisions> | <what breaks if A changes without B knowing> |
| <Domain B → Domain D timing> | <deadline / dependency> | <consequence of slip> |
| <Domain C firewall vs Domain A public surface> | <where the boundary is> | <what crosses it> |

---

## Update protocol

- New commitment → add to relevant domain section + collision-map entry if it touches another domain.
- Removed commitment → mark as `STRUCK YYYY-MM-DD` rather than deleting (audit trail).
- Conflict between this file and a canonical source → trust the canonical source, update this file.
- Used by Thoth as a secondary check for silent reversion: if a council decision contradicts a row here, that's a flag.

## Version
- v0.1 — public structure template — populate as needed per environment
