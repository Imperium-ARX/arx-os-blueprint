# context/clients/ - the client relationship records

One file per active client, kebab-case slug (`acme-industries.md`). This is the **relationship
record**: where the relationship stands, what happened when, what's next. The **delivery
workspace** (contracts, research, deliverables) is the client's folder in `clients/<name>/` -
keep both, they answer different questions (ruling: `context/README.md`).

## The record shape

No YAML frontmatter. A bold key-value header directly under the H1, then a reverse-chronological
dated log, then stable profile sections. The invariant keys are **Status** (CAPS state + date)
and **Next step** (one concrete action with an owner):

```
# <Client> (CLIENT - SIGNED, YYYY-MM-DD)

**Status:** ACTIVE - one-line narrative with dates
**Deal:** commercials, with provenance
**Primary contact:** name, role
**Source:** how they found us
**Next step:** one concrete action, named owner

---

## YYYY-MM-DD - HEADLINE OF WHAT HAPPENED (supersedes <older entry> if it does)
## Who they are
## The business
## Deal shape
## Open questions
```

Rules:

- Newest log entry on top. When an entry supersedes an older one, say so in its heading.
- Live risks go in a `> ⚠` blockquote at the very top, removed when resolved.
- Money figures cite their source (signed doc, invoice), per the financial-accuracy rule.
- When the engagement ends, the record stays here with status ARCHIVED; the delivery folder
  moves per `clients/README.md`.

A fully generic worked example: `_EXAMPLE-acme-industries.md` (fictional; delete once real
records exist).
