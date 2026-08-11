---
name: dashboard-query
description: Use when the user asks about a dashboard on their Dashboard tab — a data point, a metric, "why does the dashboard show X", or a request to change/add/fix something on a dashboard. Resolves which GitHub repo backs that dashboard and whether this seat may read or write it.
---

# Dashboard Query

The Dashboard tab in the desktop app shows dashboards assigned to this seat by the Imperium
admin. Each one is a hosted web app backed by a GitHub repository. This seat's map of
dashboard → repo → access lives in `context/dashboards.md` (admin-managed, refreshed on every
app start — never edit it).

## Answering questions about a dashboard ("what's X", "why does it show Y")

1. Open `context/dashboards.md` and find the dashboard the user means (match by name; ask only
   if genuinely ambiguous).
2. If it has a repo, clone or pull it into `.cache/repos/<repo-name>` (shallow is fine) and
   read the relevant code/data: where the number comes from, which table or API feeds it, how
   it is computed.
3. If the answer is about live data rather than logic, the repo shows you which backend the
   dashboard reads (Supabase tables, API routes). Query that backend only with credentials
   this workspace already has (`connection.json`, `.env`) — never invent or request new ones.
4. Answer with the source of truth cited (file, table, or endpoint).

## Changing a dashboard ("change X", "add a field", "fix the chart")

Check the `access` column first:

- **read** — do not attempt the change. Say plainly: "You have read access to this dashboard,
  so I can explain it but can't change it. Ask your Imperium admin for write access." Then
  offer the read-side help you CAN give (what the change would involve, where it would land).
- **write** — make the change, with care:
  1. The deployment is **shared**: everyone assigned this dashboard sees the same URL, so a
     change affects them all. Say so before pushing anything non-trivial.
  2. Work on a branch and open a pull request; never push to the default branch of a shared
     dashboard repo. (Your own seat repo is the only repo you push to directly.)
  3. Keep the change minimal and in the repo's existing style; deployment happens per that
     repo's own pipeline once merged.
- GitHub is the hard enforcement: if a push is rejected, your access changed — report it, do
  not work around it.

## The `cockpit_data` table (company dashboards on the company Supabase)

Company-built dashboards usually render from the company workspace's `cockpit_data` table -
one row per dashboard page:

- `page` (text, primary key) - e.g. `overview`, `finance`, `sales`, `marketing`, `ops`
- `department` (text) - which department's seats may edit that page; `null` = admin backend only
- `payload` (jsonb) - the full page content the dashboard renders
- `updated_at`, `updated_by` - `updated_by` is the employee_id of the last seat edit; `null` = server job

Reading a page's data = one row by `page`. Editing is **department-gated**: only write a row
whose `department` matches this seat's department (from `imperium-user.json`); RLS enforces it
server-side, so a rejected write means the gate is real - report it, don't work around it.
Edits replace the `payload` - read it first, change only the fields asked for, write it back
whole. A dashboard whose numbers come from `cockpit_data` changes WITHOUT a repo push; the repo
route above is for changing the dashboard's code, not its data.

## Rules

- Never edit `context/dashboards.md` or claim access it doesn't grant.
- A dashboard not listed there is not this seat's to query — say so.
- Dashboard sign-in screens inside the app are that dashboard's own auth; you cannot bypass
  them and should not try.
