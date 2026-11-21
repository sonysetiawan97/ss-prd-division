# 01 — Import the five skills under published names

- **Date:** 2026-11-21
- **Source:** `docs/spec/publish-division-bundle.md`
- **Status:** done
- **Blocked by:** None — can start immediately

## Status notes

- [ddd:ubiquitous-language] `skills/ss-grilling/SKILL.md:36,38` — sibling links point at `../ss-domain-modeling/` (the Published name of the local `ss-domain-modeling-001`). The Bundle deliberately excludes `ss-domain-modeling` (spec "Out of Scope", decision: grilling ships copied, no companion skills). The links resolve only when an installer also has the main ss workflow installed; in a standalone Bundle install they are dangling. Direction: vendor the two Format files into the Bundle or drop the file links to plain prose, in a later ticket.
- [clean:duplication] The `ss-grilling` copy is renamed only; its two `ss-domain-modeling` links are the sole cross-Bundle references. Direction: settle with the finding above.

- **Selesai:** 2026-11-21 · ss-prd-division@uncommitted

## What to build

The repo installs as one Bundle of five Skills under their Published names. Each local `ss-*-001` Skill is copied with its reference files, its folder and frontmatter are renamed, and every cross-reference points at the Published name. The local `-001` copies stay untouched.

## Acceptance criteria

- [ ] `skills/` holds exactly five folders: `ss-division-workflow`, `ss-grilling`, `ss-dev-prd`, `ss-qc-prd`, `ss-ui-ux-prd`.
- [ ] Each Skill's frontmatter `name:` equals its folder name.
- [ ] No `-001` remains in a folder name, a frontmatter name, or a cross-reference.
- [ ] Each of the three PRD Skills keeps its `PRD-FORMAT.md`.
- [ ] `grep -rE 'ss-[a-z-]+-[0-9]{3}' skills/` returns nothing.
- [ ] `~/.agents/skills/ss-*-001` is unchanged.
