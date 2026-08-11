# data/transcripts/ - source transcripts

Recorded source material, typed by origin. Distinct from `memory/transcripts/` (your own daily
voice-note capture, one file per day) - your words go there; recorded sources land here
(ruling: `context/README.md`).

| Folder | Holds |
|---|---|
| `calls/` | Sales and client call transcripts |
| `youtube/` | Own-channel video transcripts (produced by `automations/youtube/`) |
| `competitor/` | Competitor and market content transcripts |

Rules:

- Naming: `YYYY-MM-DD-topic-or-person.md` (date-first, per `memory/CONVENTIONS.md`).
- Transcript CONTENT is gitignored (only these READMEs are tracked): transcripts routinely
  carry client names and figures, and everything tracked here ships in the workspace template.
  Keep raw text intact after extraction - it is the audit trail and the only legitimate source
  for verbatim ICP language (`context/business/icp.md` layer 3).
- Facts extracted from a transcript into context/ or memory/ cite the transcript file path.
