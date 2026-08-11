---
title: Source-of-truth map
type: reference
status: active
---

<!-- ENGINE-MAINTAINED DOC living in a seed directory: updates may replace this
     file's structure, but the rulings below are edited in place as the install
     grows (add a dated ruling whenever two files start covering the same
     ground). Never carries company names or figures - pointers only. -->

# /context - the source-of-truth map

This directory is the business's knowledge base. Agents and sessions read from here before
acting. When two files look like they cover the same thing, this map says which one is
canonical. `context/index.md` stays the lean session entry point; this file is the full
read-map behind it.

## Directories

| Directory | Holds | Source of truth for |
|---|---|---|
| `context/org/` | Company-wide facts (company, offers, departments, roster, glossary) | "What does this business do, who works here, what do we sell?" - the 60-second top sheet |
| `context/business/` | The deep business layer: story, ICP, pricing, competitive landscape | Any question that needs more than the top sheet - "why do we exist, who exactly buys, what do deals look like?" |
| `context/clients/` | One file per active client - the relationship record | "Who is this client, where does the relationship stand, what's the next step?" |
| `context/prospects/` | One file per prospect - the pipeline's deep records | "Who is this prospect, what do they need, why haven't they signed?" |
| `context/seat.md` | This install's seat truth (never synced) | "Whose seat is this, what may it approve?" |
| `context/team/` | Server-owned shared team knowledge (read-only) | What teammates have promoted to the company layer |

## Which file wins

Near-duplicates are deliberate - each answers a different question. Do not merge them; route by question:

- **Offers** - `context/org/offers.md` is canonical for what we sell and how offers map to clients. `context/business/pricing.md` is canonical for what deals actually close at (live deal data, anchoring). Offer shape → org; money shape → pricing.
- **ICP** - `context/org/company.md` holds the one-paragraph ICP (canonical definition). `context/business/icp.md` holds the deep layer: headspace, verbatim language, objections. Quoting the customer's own words → business/icp.md; stating who we sell to → org/company.md.
- **Voice** - `content-pipeline/voice-profile/` is canonical for how the owner sounds. Nothing in context/ duplicates it.
- **Clients** - `context/clients/<slug>.md` is the relationship record (status, log, next step). `clients/<name>/STATUS.md` + folder is the delivery workspace (artifacts, contracts, deliverables). Relationship question → context record; engagement/delivery question → clients/ folder. Update both when a deal moves.
- **Prospects** - `context/prospects/<slug>.md` is the deep record; the pipeline board installed by the sales-crm pack (`packs/sales-crm/memory/pipeline.md`) is the board view. **Never let a prospect exist only as a board row with no file here** - the row is what renders, the file is what's true.
- **Transcripts** - `memory/transcripts/` holds daily voice-note capture (one file per day). `data/transcripts/` holds source material (calls/, youtube/, competitor/). Your own words → memory; recorded source material → data.
- **Work products** - client-facing deliverables → `clients/<name>/deliverables/`; content → `content-pipeline/`; everything else the agent produces (debriefs, internal reports, briefs) → `outputs/`. Agent work lands in the repo, not in chat.
- **Money** - `memory/finances.md` and the provenance rule win over any figure quoted in a context file. A number without a source is not a number.

When a new conflict appears, add a dated ruling here (`decided YYYY-MM-DD`) naming which file wins for which question - and move the loser's stale sections to `_archive/`.

## The query playbook

For recurring question types, read in a fixed order and answer in a fixed shape. Extend this list as the owner's real questions emerge; keep each entry to three lines.

### "Who is this client / prospect?"

Read in order: `context/clients/<slug>.md` (or `context/prospects/<slug>.md`) → `clients/<name>/STATUS.md` if they're in delivery → `memory/people/dossiers/` for the person.
**Answer shape:** status line + last dated log entry + next step, then depth only if asked.

### "What should we say to this buyer / what are the objections?"

Read in order: `context/business/icp.md` (verbatim language + objections) → `context/org/offers.md` → `content-pipeline/voice-profile/` before drafting anything.
**Answer shape:** the objection or angle in the buyer's own recorded words, labeled verified or unverified; never invented quotes.

### "What do we charge / what did deals close at?"

Read in order: `context/business/pricing.md` (live deal data) → `memory/finances.md` for actuals.
**Answer shape:** figure + provenance (which deal, which file), or "unverified - the real figure lives in <place>".

### "What's on the dashboard / why does it show X?"

Read in order: the seat's dashboard map (dashboards.md in this directory, app-written on every start) → the dashboard-query skill.
**Answer shape:** the number, its source cited (file, table, or endpoint).

## Freshness

When a section is appended rather than rewritten, suffix it `(added YYYY-MM-DD)`. When a directive comes straight from the owner, tag it `[OWNER EXPLICITLY SAID]` so later sessions know it is a quote, not a synthesis. For domains with fast-moving sources, keep a small state table here:

| Component | State | Note |
|---|---|---|
| (example) `context/business/icp.md` | ✅ fresh / ⚠️ frozen / ❌ blocked | when it last moved, what unblocks it |

## Archive, never delete

Superseded documents move to an `_archive/` folder beside their siblings (created on first use, e.g. an `_archive/` inside `context/business/`) - kept for reference, **not to be read as current**. Archived files are excluded from every index and generator. Full rule: engine-core hard rules.

## Verified vs unverified

Facts extracted from real source material (transcripts, signed documents, live queries) are **verified**; everything else is labeled. When a domain accumulates both, keep one verified register per domain and quarantine the unverified pile in a `pre-verification/` subfolder - never quote it as fact. Inline, tag doubtful claims `[UNVERIFIED]`.
