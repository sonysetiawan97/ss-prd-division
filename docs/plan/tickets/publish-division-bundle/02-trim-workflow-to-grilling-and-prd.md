# 02 — Trim the Division workflow to grilling and the Division PRD

- **Date:** 2026-11-21
- **Source:** `docs/spec/publish-division-bundle.md`
- **Status:** done
- **Blocked by:** 01 — Import the five skills under published names

## Status notes

- **Selesai:** 2026-11-21 · ss-prd-division@uncommitted

## What to build

Running `ss-division-workflow` for one Division grills that Division, writes its Division PRD, then stops for confirmation. The spec and ticket stages are gone, and the PRD Skills also stop after the PRD.

## Acceptance criteria

- [ ] `ss-division-workflow` has exactly two stages: grilling, then the Division PRD.
- [ ] The Division table has no Spec path or Ticket path column.
- [ ] No Skill references `ss-spec` or `ss-ticket`.
- [ ] No PRD Skill tells the user to continue to a spec.
- [ ] On `dev`, the workflow writes `docs/dev/prd.md` and stops.
- [ ] `grep -rE 'ss-spec|ss-ticket' skills/` returns nothing.
