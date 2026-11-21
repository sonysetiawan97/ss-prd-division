# PRD: Publish the ss Division Workflow Bundle

- **Date:** 2026-11-21
- **Source:** the grilling session of 2026-11-21, `GLOSSARY.md`

## Problem

The Division layer of the ss workflow exists only on one machine, as local `ss-*-001` folders under `~/.agents/skills/`: `ss-division-workflow-001`, `ss-grilling-001`, `ss-dev-prd-001`, `ss-qc-prd-001`, and `ss-ui-ux-prd-001`. They are not in git, cannot be installed online, and carry local-only details: `-001` suffixes, references to suffixed skill names, Indonesian strings, and spec and ticket stages the Division flow no longer runs. Nobody else, and no other machine, can install the Division workflow.

## Goals / Non-Goals

**Goals**

- Publish all five Skills as one Bundle from `sonysetiawan97/ss-prd-division`, installable with `npx skills add sonysetiawan97/ss-prd-division`, globally (`-g`) or per project.
- Ship Skills under their Published names (no Dev suffix).
- Make the Division workflow exactly two stages: grilling, then the Division PRD. No spec and no tickets.
- Every user-facing string in English.
- Release it as version 1.0.0.

**Non-Goals**

- No `ss-spec` or `ss-ticket` in this Bundle. The Division flow stops at the Division PRD.
- No main PRD, architecture or AGENTS.md skill in this Bundle.
- No npm package, Claude Code plugin, or Agent files.
- No Sagara version.
- No dev-install script; the local `-001` copies stay as they are and are not regenerated.

## Users / Actors

- **Maintainer**: the repo owner, who edits the Skills in this repo from now on.
- **Installer**: anyone who installs the Bundle on a Host with `npx skills add`.
- **Division runner**: a person who runs one Division (Dev, QC, UI/UX, or custom) through grilling and its Division PRD.

## Requirements

1. The repo `sonysetiawan97/ss-prd-division` is public on GitHub.
2. The repo contains exactly five Skills under `skills/<published-name>/`: `ss-division-workflow`, `ss-grilling`, `ss-dev-prd`, `ss-qc-prd`, `ss-ui-ux-prd`, copied once from `~/.agents/skills/ss-*-001/` with their reference files.
3. Every Skill drops the Dev suffix in its folder name, its `SKILL.md` frontmatter `name:`, and every reference to any Skill in the Bundle.
4. `ss-division-workflow` runs exactly two stages: grilling scoped to the Division, then the Division PRD. It has no spec stage and no ticket stage.
5. `ss-division-workflow` maps `dev` → `ss-dev-prd` → `docs/dev/prd.md`, `qc` → `ss-qc-prd` → `docs/qc/prd.md`, `ui-ux` → `ss-ui-ux-prd` → `docs/ui-ux/prd.md`. A custom Division uses the closest PRD skill and its own `docs/<division-slug>/prd.md`.
6. No Skill writes a spec or a ticket, and no Skill references `ss-spec` or `ss-ticket`.
7. Each Division PRD skill writes only `docs/<division-slug>/prd.md`; it never writes a spec, a ticket, or another Division's PRD.
8. No Skill hardcodes `~/.agents/skills/`. A Skill that points to another Skill's `SKILL.md` uses a sibling path (`../ss-<name>/SKILL.md`), resolved to an absolute path from its own base directory before it goes into a subagent prompt.
9. No Skill names a Sagara skill.
10. Every user-facing and marker string is in English. The Indonesian headings become `Division PRD`, `Architecture Dependencies`, `Testing Strategy`, and `Flows & Interface`.
11. `README.md` holds only: the install command (with the `-g` variant), the flow diagram, a one-line list of the five Skills, and the MIT license.
12. `LICENSE` is MIT.
13. `CHANGELOG.md` has a `1.0.0` entry for the initial release, and the release commit is tagged `v1.0.0`.
14. The local `~/.agents/skills/ss-*-001` copies are left untouched.
15. A Division PRD may not contradict the main `docs/prd.md`; a contradiction is a main-PRD change, so the Skill stops and asks the user to update the main PRD first.
16. A Division PRD skill stops when `docs/prd.md` or `architecture/overview.md` is absent, and names the missing file.
17. The workflow skill never writes an Artifact; the stage skill writes it. The grilling and the Division PRD each end with a confirmation Gate, not an automatic next step.
18. Each PRD skill uses its `PRD-FORMAT.md` exactly: same headings, same order, nothing added or renamed.

## Acceptance Criteria

1. `npx skills add sonysetiawan97/ss-prd-division -g` lists five Skills, all with Published names.
2. A project install (`npx skills add sonysetiawan97/ss-prd-division` in a repo) installs the same five Skills.
3. `grep -rE 'ss-[a-z-]+-[0-9]{3}' skills/` returns nothing.
4. `grep -r '~/.agents/skills' skills/` returns nothing.
5. `grep -ri 'sagara' skills/` returns nothing.
6. `grep -rE 'ss-spec|ss-ticket' skills/` returns nothing.
7. `grep -rE 'PRD Divisi|Ketergantungan Arsitektur|Strategi Pengujian|Alur & Antarmuka|Lanjut|tiket|seluruh' skills/` returns nothing.
8. Each Skill's frontmatter `name:` equals its folder name.
9. On `dev`, `ss-division-workflow` runs grilling, then writes `docs/dev/prd.md`, then stops for confirmation; it writes no spec and no ticket.
10. `README.md`, `LICENSE` (MIT) and `CHANGELOG.md` (with `1.0.0`) exist, and tag `v1.0.0` exists on GitHub.
11. `~/.agents/skills/ss-*-001` are unchanged.
12. Each Division PRD matches its Skill's `PRD-FORMAT.md` heading for heading.
13. With `docs/prd.md` missing, `ss-division-workflow` stops and names `docs/prd.md` as the missing step.

## Constraints / Assumptions

- skills.sh has no publish step; it lists Skills from `npx skills` install telemetry.
- `npx skills add` does not install from npm; it reads `skills/<name>/SKILL.md` from a git repo.
- Hosts install to different directories (Claude Code `~/.claude/skills/`, pi `~/.agents/skills/`, opencode `~/.config/opencode/skills/`, or `.agents/skills/` per project), with every Skill of the Bundle side by side.
- The Bundle is self-contained for grilling and the Division PRD. It deliberately stops before spec and tickets.
- **Unverified**: requirement 8 assumes the Host tells a Skill its own base directory. Claude Code does ("Base directory for this skill"); pi and opencode are not checked.
- The repo is personal (`ss`) and kept separate from office work.
- The three Division PRD Skills are near-identical; they are copied as they are, not merged into one.

## Companion Docs

None: this repo is a skills Bundle with no tables, endpoints or page routes.

## Changelog

<!-- newest first -->

- **2026-11-21**: Initial PRD for publishing the Division workflow Bundle via `npx skills add`. Settled in the grilling session: five Skills, grilling plus Division PRD only (no spec or tickets), Published names without the Dev suffix, English strings, MIT, v1.0.0.
