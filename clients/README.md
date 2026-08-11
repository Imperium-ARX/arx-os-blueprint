# Clients

Every client engagement gets its own folder: `clients/<client-name>/` (kebab-case). Copy `_TEMPLATE/` to start one; it carries the standard internal structure so any session (or sub-agent) can orient inside a client folder without guessing.

## The per-client pattern

```
clients/<client-name>/
├── STATUS.md        # the single source of truth: stage, commercials, next step
├── README.md        # 1-pager: who they are, what they pay for, who owns the relationship
├── context/         # scope, stakeholders, systems inventory, discovery notes
├── legal/           # NDAs, MSAs, SoWs, contracts (PDFs + markdown drafts)
├── research/        # client-specific research and analysis
└── deliverables/    # what we built for them (apps, dashboards, docs, decks)
```

Rules of the pattern:

- **STATUS.md is always current.** After any client call, decision, invoice, or delivery, update it in that session.
- **Commercials carry provenance.** Any money figure in a STATUS.md cites its source (signed SoW, invoice file, bank row), per the financial-accuracy rule. No remembered numbers.
- **Client work never lives in memory/.** Memory holds your company's knowledge; client artifacts live here.

## Prospects

The prospect RECORD lives in `context/prospects/<slug>.md` (one file per prospect - see its README; board view: `memory/pipeline.md` from the sales-crm pack). A folder in `clients/_prospects/<name>/` is created only once a prospect accumulates artifacts (draft proposals, research). When they sign, create `clients/<name>/` from `_TEMPLATE/` and the client record in `context/clients/<slug>.md`; the prospect record stays as the deep history. When they go cold, set the record's status to COLD with the reason.

## Archiving

When an engagement ends, move the whole folder to `clients/_archive/<name>/` and set STATUS.md to archived with the end date and final state. Never delete; old engagements are reference material for proposals and case studies.
