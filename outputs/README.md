# outputs/ - committed work products

Agent work lands in the repo, not in chat. Anything substantial the system produces that isn't
a client deliverable (those → `clients/<name>/deliverables/`) or content
(→ `content-pipeline/`) is written here, committed, and linked in the reply.

## Typed subfolders

| Folder | Holds |
|---|---|
| `briefs/` | Forward-looking: plans, specs, and briefs for work about to happen |
| `reports/` | Analysis and research findings: audits, investigations, syntheses |
| `debriefs/` | Backward-looking: what happened and what it taught (post-call, post-launch, post-mortem) |

Add a new typed folder (with a one-line README) only when a recurring output type doesn't fit
these three - resist per-project folders; the date does that job.

## Naming

- Single file: `YYYY-MM-DD-topic-slug.md` (kebab-case, date-first ISO - the repo standard,
  `memory/CONVENTIONS.md`).
- Multi-file deliverable: a dated folder `reports/YYYY-MM-DD-topic/` with the canonical
  artifacts at its root. Superseded first passes move to a `pre-verification/` subfolder inside
  it - kept, quarantined, never quoted as current (verified-data rule).

## Rules

- Superseded outputs move to `outputs/_archive/`, never get deleted.
- `_archive/` and `pre-verification/` are excluded from every index and register.
- A report that states figures cites sources inline, per the financial-accuracy rule.
