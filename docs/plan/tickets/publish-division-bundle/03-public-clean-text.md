# 03 — Make the bundle public-clean

- **Date:** 2026-11-21
- **Source:** `docs/spec/publish-division-bundle.md`
- **Status:** done
  - 2026-11-21 — Review (ss-code-review-001): clean against the ticket, with one Suggestion — `ss-division-workflow/SKILL.md` still read "Peta Folder", an Indonesian string; fixed in the same tree to "the folder map". All acceptance greps now return nothing; `~/.agents/skills` paths and Sagara names absent; the workflow stops and names missing `docs/prd.md` / `architecture/overview.md` (Prerequisites section).
- **Blocked by:** 02 — Trim the Division workflow to grilling and the Division PRD

- **Selesai:** 2026-11-21 · ss-prd-division@uncommitted

## What to build

Every Skill reads as a public English Skill: no Indonesian strings, no Sagara names, no local `~/.agents/skills/` paths, and a missing prerequisite is named instead of guessed.

## Acceptance criteria

- [ ] All user-facing and marker strings are English; the four Indonesian headings are translated.
- [ ] `grep -ri 'sagara' skills/` returns nothing.
- [ ] `grep -r '~/.agents/skills' skills/` returns nothing.
- [ ] Cross-skill references use the Published name or a sibling path.
- [ ] With `docs/prd.md` missing, the workflow stops and names it.
- [ ] With `architecture/overview.md` missing, the workflow stops and names it.
- [ ] `grep -rE 'PRD Divisi|Ketergantungan Arsitektur|Strategi Pengujian|Alur & Antarmuka|Lanjut|tiket|seluruh' skills/` returns nothing.
