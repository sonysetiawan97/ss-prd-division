# 05 — Publish v1.0.0

- **Date:** 2026-11-21
- **Source:** `docs/spec/publish-division-bundle.md`
- **Status:** ready-for-human
- **Blocked by:** 04 — Add the release files

## What to build

The repo is public and installable. A person pushes the release commit, tags `v1.0.0`, and checks both install modes.

## Acceptance criteria

- [ ] The repo `sonysetiawan97/ss-prd-division` is public.
- [ ] Tag `v1.0.0` exists on the release commit.
- [ ] `npx skills add sonysetiawan97/ss-prd-division -g` lists the five Skills.
- [ ] A per-project install lists the same five Skills.
- [ ] The local `~/.agents/skills/ss-*-001` copies are untouched.
