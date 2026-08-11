# context/prospects/ - the pipeline's deep records

One file per prospect, kebab-case slug (`jordan-lee-northwind.md`). This is the CRM's deep
layer: who they are, what they need, every dated touch. The board view lives in
`memory/pipeline.md` (sales-crm pack) - **never let a prospect exist only as a board row with
no file here.** The row is what renders; the file is what's true (ruling: `context/README.md`).

Same record shape as `context/clients/README.md`: bold key-value header (**Status** +
**Next step** mandatory), reverse-chronological dated log, stable profile sections below.
Useful prospect-side sections: `## Pains (their words)` - verbatim from real conversations,
sourced - `## What we'd build`, `## Deal shape`, `## ICP classification`, `## Gaps to fill`.

Lifecycle:

- **They sign** → create the client record in `context/clients/<slug>.md` (and the delivery
  folder from `clients/_TEMPLATE/`). The prospect file STAYS here as the deep history; the
  client record links back to it.
- **They go cold** → set status COLD with the reason and leave the file. Reasons are the
  cheapest sales research that exists.

A fully generic worked example: `_EXAMPLE-jordan-lee-northwind.md` (fictional; delete once
real records exist).
