# 01 — Import the five skills under published names

- **Date:** 2026-11-21
- **Source:** `docs/spec/publish-division-bundle.md`
- **Status:** ready
- **Blocked by:** None — can start immediately

## What to build

The repo installs as one Bundle of five Skills under their Published names. Each local `ss-*-001` Skill is copied with its reference files, its folder and frontmatter are renamed, and every cross-reference points at the Published name. The local `-001` copies stay untouched.

## Acceptance criteria

- [ ] `skills/` holds exactly five folders: `ss-division-workflow`, `ss-grilling`, `ss-dev-prd`, `ss-qc-prd`, `ss-ui-ux-prd`.
- [ ] Each Skill's frontmatter `name:` equals its folder name.
- [ ] No `-001` remains in a folder name, a frontmatter name, or a cross-reference.
- [ ] Each of the three PRD Skills keeps its `PRD-FORMAT.md`.
- [ ] `grep -rE 'ss-[a-z-]+-[0-9]{3}' skills/` returns nothing.
- [ ] `~/.agents/skills/ss-*-001` is unchanged.
