# 03 — Make the bundle public-clean

- **Date:** 2026-11-21
- **Source:** `docs/spec/publish-division-bundle.md`
- **Status:** ready
- **Blocked by:** 02 — Trim the Division workflow to grilling and the Division PRD

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
