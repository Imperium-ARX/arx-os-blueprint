---
name: artifact-create
description: Use ONLY when the user explicitly asks to create a personal artifact, dashboard, goal board, vision board, tracker, or similar personal visualization for their Dashboard tab. Not for company dashboards (admin-managed) and never proactively.
---

# Artifact Create

Personal artifacts are self-contained local HTML files in `artifacts/` at the workspace root.
The desktop app's Dashboard tab lists every `artifacts/*.html` automatically and previews it
in a sandboxed frame — no deploy, no accounts, works offline. The file syncs with the rest of
the workspace to this seat's private repo.

## Hard rules

- **Explicit ask only.** The user must have asked for an artifact/board/tracker in so many
  words. Never create one as a side effect of another task.
- **Soft cap: 2 artifacts.** If two already exist, refuse and offer to replace or extend one
  instead. Only exceed the cap if the user insists after hearing that.
- **One file per artifact.** Everything inline — CSS and JS in the file, no external CDNs,
  fonts, or build steps. The preview frame is sandboxed without network guarantees.
- Filename is the title: `vision-board-2026.html` renders as "Vision Board 2026" in the rail.

## Building one

1. Ask what it should show only if the request doesn't say (goals? metrics? habits?). One
   question, then build.
2. Write a single polished HTML file to `artifacts/<kebab-name>.html`: inline styles, dark
   theme by default (the app is dark), readable typography, no lorem ipsum — use the user's
   real content from the conversation or workspace.
3. Interactivity is welcome (checkboxes, progress bars, tabs) but there is no server, and the
   preview sandbox runs on an opaque origin where `localStorage` THROWS — always wrap storage
   access in try/catch with a graceful in-memory fallback.
4. If it needs live data, the sandboxed frame can `fetch` HTTP APIs that allow cross-origin
   reads (e.g. the company backend's RLS-safe endpoints with the workspace's existing
   credentials, or a personal Supabase/Railway service the user sets up — tell them what to
   create, don't create accounts for them).
5. Tell the user it's live: they'll find it at the bottom of the Dashboard tab immediately.

## Editing and removing

- Edits are just edits to the file; the preview refreshes on next open.
- To remove an artifact, delete the file (confirm first — it may hold their goal history).
