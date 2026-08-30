# Phase 4 - Connections

**Goal:** plug the system into the tools they already use — through the **Connections tab**, together, one app at a time.

Work-app connections (mail, calendar, accounting, CRM, ads and the rest) are **panel-driven**: the person connects each app themselves from the Connections tab in the sidebar, by signing in with their own account in their own browser. You never handle a credential. The live state of every connection is written automatically to `context/connections.md` — that file, not the onboarding state table, is the source of truth for what is connected.

**The three standing rules of this phase:**

1. **NEVER ask for keys, tokens, logins, passwords or codes in chat.** Not to "speed things up", not if they offer. Connecting always happens in the Connections tab and their own browser. If someone pastes a credential unprompted, tell them to treat it as exposed and rotate it, and point them at the tab.
2. **Connector state lives in `context/connections.md`.** Read it whenever you need to know what is connected; never copy connection status into the onboarding state table — it drifts.
3. **What the tab doesn't show doesn't get set up solo.** Apps marked "Being set up" are waiting on the install team; "Coming soon" is not available yet. Name them, record interest in the state file under "Pending items", move on.

## 1. Open the phase

**Recall their Phase 2 answer** about where they go each week. Then ask one question before starting: **"Who else works in these tools day to day - an assistant, a partner, a team member?"** → `team_users` in the state file.

If someone shares the inbox or pipeline, give the honest answer: each of those people can get their own seat - a separate install of this same system that shares [company]'s context through the built-in company workspace. Setting up extra seats is an install-team job. Note anyone who should get a seat in the state file.

**Backup is already handled - say so, don't set it up.** Open with the good news, in these words or closer ("repository", "versioned", "API", "token" are banned in intro sentences): "Your work backs itself up automatically - everything you and I build here is saved privately to your company workspace, so if your laptop dies tomorrow, nothing is lost."

## 2. Walk the Connections tab

Open the Connections tab together (the plug icon in the sidebar). Then, card by card:

- a. Read `context/connections.md` first so you know the live state before you speak.
- b. For each app under **Yours**, give one sentence on what connecting it does for THEM, tied to their business ("Gmail means 'what came in from the Hendersons this week' is one question, not twenty minutes of scrolling").
- c. Ask: **"Want to connect this now, later, or skip it?"** Respect the answer. Later → move on, no guilt; the tab is always there.
- d. If now: tell them to click **Connect** on the card. Their browser opens; they sign in and approve **there**. You wait. The card ticks by itself when it lands — no keys, nothing to paste, nothing for you to do.
- e. **Verify by using it, not by asking.** When the card shows Connected, run one real, tiny read ("your newest email's subject is…", "your next meeting is…") so they SEE it working. That moment is the phase's whole point.
- f. Apps under **Connected by your company** are already live for everyone - one sentence on what that means, no action.
- g. Apps under **Being set up** or **Coming soon**: one sentence each, log interest in the state file, never attempt a solo workaround.

Use the natural dead time: while they're in the browser approving an app, prepare the verification question for step e so the win lands the second the tick appears.

## 3. Install-team and legacy connectors

A few capabilities are configured WITH the install team, not walked through here: the company brain, always-on workers, extra seats, and any legacy key-based connector guide still in `docs/connectors/` (see the scope note in `docs/connectors/INDEX.md`). If the plan or the user's answers touch these, name them in one sentence each and record the interest under "Pending items" in the state file - never attempt the setup solo mid-onboarding, and never collect their keys in chat.

## 4. End-of-phase token sweep

Run a project-wide grep for `{{` and resolve every remaining token using this default table - "leave" is only allowed for tokens on the deferred-ok allowlist in `docs/ONBOARDING-FLOW.md` (dormant features that never load into always-on instructions).

| Token family | If not collected by now | Why |
|---|---|---|
| `{{DEPLOY_TARGET}}` | replace with `none configured (local only)` | it sits in always-loaded instructions; a literal token must never survive onboarding |
| `{{CCY}}` | replace with the Phase 2 currency, or `USD` + a note | finance skills read it |
| `{{BRAND_PRIMARY}}/{{BRAND_NEUTRALS}}/{{BRAND_FONTS}}` | replace with `not set - ask the owner before any branded deliverable` | stops literal tokens reaching presentations |
| `{{MEDIA_STORE}}` | replace with `local: content-pipeline/media/ (no cloud media store configured yet)` | no orphan tokens |
| `{{FOLDER_*}}` / `{{MEDIA_HUB_DRIVE_ID}}` | leave (dormant skill) or `not-configured` | filled by the install team if that capability lands |
| `{{OWNER_SOUL_ID}}` + likeness fields | leave (dormant rule, deferred-ok) | filled by the install team with that connector |
| `{{NOTIFY_CHANNEL}}` | leave - deferred-ok | the notify rule carries a "not configured - skip silently" runtime fallback |

Log the decision per token in the state file. The grep result after this step should contain NO token outside the deferred-ok allowlist paths (and the files that document the tokens, per the pass exclusions in SKILL.md).

## 5. Failure policy

If a connection fails or a card shows "Needs reconnecting": stay calm, never blame them. Reconnecting is the same one click on the card. If it still fails after two attempts, note it under "Notes for next session" in the state file and move on - momentum beats completeness; any card can be finished any day by opening the Connections tab.

## 6. Close the phase

This phase can span multiple sessions. `context/connections.md` updates itself; update the onboarding state file only for `team_users`, pending items, and the token sweep. When the person has connected or consciously passed on every card under **Yours**: update status page (Phase 4 done, Phase 5 current, overall 63%).

**Exit criteria:** every card under **Yours** is connected or passed on by the user's explicit choice; each connected app got its one visible verification moment; the token sweep is logged.
