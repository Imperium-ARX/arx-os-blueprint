# Changelog

All notable changes to Imperium OS. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning follows [SemVer](https://semver.org/). Versions 0.1.0-0.2.1 are donor lineage (pre-repo, no dates recorded); everything under Unreleased landed in this repository on 2026-07-02.

## [1.2.0] - 2026-08-11

### Added

- **Source-of-truth architecture layer** (patterns ported from a production install, content-free). `context/README.md` - the canonical source-of-truth map: directory table, "which near-duplicate wins" rulings, a query playbook (read-order + answer-shape per question archetype), freshness conventions (`(added YYYY-MM-DD)`, `[OWNER EXPLICITLY SAID]`), and the file-vs-database-row truth split. `context/index.md`'s "Where detail lives" now points at it.
- **Deep business layer.** `context/business/{company-story,icp,pricing,competitive-landscape}.md` - empty templates filled during onboarding discovery. Deliberately NOT added: offers (canonical in `context/org/offers.md`) and voice (canonical in `content-pipeline/voice-profile/`) - the read-map rules on both.
- **Relationship records (file CRM).** `context/clients/` + `context/prospects/` - one file per entity: bold key-value header (Status + Next step mandatory), reverse-chronological dated log with supersession in the headings, static profile sections below. One fully fictional example each. `clients/_prospects/` demoted to artifact storage; `memory/pipeline.md` (sales-crm pack) stays the board view with a new "never a row without a record file" rule.
- **`outputs/` - committed work products.** Typed subfolders (briefs/, reports/, debriefs/); agent work lands in the repo, not chat; multi-file reports get a dated folder with a `pre-verification/` quarantine.
- **`data/transcripts/` - source transcripts** (calls/, youtube/, competitor/), distinct from `memory/transcripts/` (daily voice capture). Content gitignored by design - tracked files ship in the desktop workspace template, transcripts carry names and figures.
- **Hard rules 20 + 21** in engine core: archive-never-delete (demotion to `_archive/`, excluded from every index) and verified-data discipline (source-cited facts vs `[UNVERIFIED]` tags, one verified register per domain).
- **`dashboard-query` extended** with the company Supabase `cockpit_data` contract (one row per page, department-gated edits, whole-payload writes); `dashboard/README.md` gains a scope note separating the self-built cockpit contract from admin-managed Dashboard-tab dashboards. Routing rows added for `dashboard-query` and `artifact-create` (fixes registry drift).

## [1.1.0] - 2026-07-04

### Removed

- **GitHub connectors retired - backup and team sharing are now built into Imperium OS.** The desktop app saves each seat's knowledge folders to the company's own workspace backend (one Supabase project per company, RLS-scoped per seat) and pulls shared team contributions read-only into `context/team/`. Removed: `docs/connectors/github-backup.md`, `docs/connectors/org-sync.md`, `scripts/org-sync.js`, the org-sync SessionStart hook, the github-backup connector row/card/state entries. `context/org/` in org mode is now pre-loaded and kept aligned by the install team (propose-upward flow via `memory/org-proposals/` unchanged); rule 32 extended to cover the server-owned `context/team/`.

## [1.0.0] - 2026-07-02

### Added

- **M8 - Verification battery + fixes.** Four-track verification before this release: an adversarial scrub hunt (derivative/indirect leak detection beyond token matching), a fresh-clone integrity pass (registry, lint, package-check, worker boot, all four pack install/uninstall round-trips byte-identical, always-on token budget measured under 16k), and two full persona install simulations (a solo head-of-marketing seat with a hidden real operator; a second seat joining an existing org). 22 raw findings adversarially judged to 17 confirmed, all fixed: donor-domain example prompts neutralised, an org-truth guard so department-head installs never write the seat holder as company owner, the real-operator score cap extended to weekly health checks, a machine-readable deferred-ok placeholder allowlist reconciling the client-mode gate with Phase 4 deferrals, org-joining inheritance for company-level tokens, and the rules catalog relocated to `.claude/reference/rules-index.md` to keep the always-on surface under budget.
- **Desktop integration spec.** `docs/DESKTOP-INTEGRATION.md`: the engine-pack artifact format (manifest with per-file engine/seed classes), offline-first provisioning flow, quarantine-and-merge update protocol, org wiring, telemetry touchpoints, and the per-release verification matrix for any desktop shell that preinstalls this OS.

- **M2 - Department packs.** Optional packs (content-marketing, finance, ops, sales-crm) with `scripts/install-pack.js` install/uninstall (exact-reverse, rollback on conflict) and a pack-integrity lint check.
- **M4 - Onboarding v2 (role-aware, org-aware) + engine/seed split.** The start-onboarding skill becomes a directory: dispatcher `SKILL.md` + one script per phase (`phases/phase-0..7.md`) + five role cards (`roles/`: owner, marketing, ops, finance, assistant - each carrying the seat interview, connector picks, and pack recommendation). New behaviours: Phase 0 org-detect (solo / org-first-seat / org-joining, with the "click into place" greeting for pre-loaded seats), Phase 1 role taxonomy + the mandatory real-operator question (a named non-user operator caps the Phase 7 Context score at 7/10 until their 20-minute sub-onboarding runs) + the OS-naming question (fills the `OS_NAME` token), Phase 2 org-vs-seat split (full company interview vs read-back-and-confirm; seat interview from the role card into `context/seat.md`), Phase 4 connector menu (`docs/connectors/INDEX.md`: benefit, key y/n, effort bucket, per-role relevance), Phase 5 pack offer wired to `scripts/install-pack.js`, Phase 7 graduation writes the first `memory/system_changelog.md` entry. State file gains `user_role_type`, `department`, `org_mode`, `real_operator`, `approval_boundary`, `os_name`, `packs_installed/declined`; the status page gains seat + org-mode header fields and pack cards. Engine/seed split: stable hard rules, dev rules, and key paths moved from `.claude/CLAUDE.md` into the engine-class `.claude/rules/00-engine-core.md`; CLAUDE.md slims to the seed shell with `ENGINE-BOUNDARY` markers; the two path classes and merge-point exceptions (the update-manifest contract) are documented in `docs/ARCHITECTURE.md`.
- **M3 - Org layer.** `context/org/` (company truth) vs `context/seat.md` (this seat) split, `scripts/org-sync.js` read-only mirror sync with a SessionStart hook, propose-upward flow via `memory/org-proposals/`, and the org-context rule (32).
- **M5 - Persona.** `context/identity.md` persona layer (named via the `OS_NAME` placeholder) plus the `self-improve-nudge` Stop hook (report-only).
- **M6 - Dormant operating layer.** Brain core contract (`brain/`: RLS-forced Postgres schema, append-only audit log, approval queue), fixtures-first worker hub (`automations/worker/`: zero-credential boot, every response stamped `"source": "fixtures"`), and the cockpit contract (`dashboard/README.md`, SEED DATA badge requirement).
- **M7 - Packaging guardrails.** `scripts/package-check.js` pre-release/pre-delivery gate: scrub-blacklist sweep, donor-branding check, external-domain-leak check, seed single-source integrity, SEED DATA badge contract, placeholder inventory (zero-survivor in `--client` mode). Plus `docs/conventions/seed-data.md`, a WARN-level seed-integrity check in `os-lint.js` (shared helper `scripts/lib/seed-utils.js`), and this changelog.

### Changed

- **M1 - Skill directory migration.** All 44 skills moved from flat files to `<name>/SKILL.md` directories with agentskills-compatible frontmatter; registry, lint, and routing references updated.
- **M2 - Base slimmed to 21 engine skills.** Department-specific skills moved out of the base and into their packs.
- **M7 - README install step re-neutralised.** The clone instruction no longer hardcodes a personal GitHub URL (donor-branding leak caught by the new gate).

### Security

- Scrub-blacklist mechanism ships with the repo; the list itself stays maintainer-local and gitignored (`scrub-blacklist.local.json`).

## [0.2.1]

### Added

- Public-release README.

## [0.2.0]

### Changed

- Onboarding hardened via two full overnight install simulations against real personas (an external multi-business CEO and an in-house creative director); every verified install bug fixed.

## [0.1.0]

### Added

- Engine extracted from the founder's master OS: rules, skills, memory system, hooks, registry, and lint.
