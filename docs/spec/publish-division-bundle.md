# Spec: Publish the ss Division Workflow Bundle

Source: the settled grilling decisions of 2026-11-21, `docs/prd.md`, and `GLOSSARY.md`.

## Problem Statement

The Division layer of the ss workflow exists only as local `ss-*-001` folders on one machine. It cannot be installed from git, it points at suffixed skill names, it mixes Indonesian and English strings, and its workflow still runs spec and ticket stages the Division flow no longer needs. A person on another machine cannot run a Division through grilling and its PRD.

## Solution

Publish the Division layer as one Bundle from `sonysetiawan97/ss-prd-division`: five Skills under their Published names, installed with `npx skills add sonysetiawan97/ss-prd-division`. The Division workflow runs two stages — grilling scoped to the Division, then the Division PRD — and stops. The Bundle is self-contained: grilling ships with it, and no spec or ticket skill is included.

## User Stories

1. As an Installer, I want to install all five Division Skills with one command, so that I do not copy folders by hand.
2. As an Installer, I want a global install and a per-project install, so that I can choose where the Skills live.
3. As a Division runner, I want to name a Division and have the workflow ask which one when I forget, so that I never guess a slug.
4. As a Division runner, I want grilling scoped to the Division, so that I do not re-litigate decisions the main PRD and architecture already settled.
5. As a Division runner, I want the grilling to end at a confirmation Gate, so that the Division PRD is not written on an unsettled design.
6. As a Division runner, I want the Division PRD written to `docs/<division-slug>/prd.md`, so that each Division has one home.
7. As a Division runner, I want the flow to stop after the Division PRD, so that spec and tickets stay in the main workflow.
8. As a Division runner, I want the Division PRD to select only what the Division owns and depends on, so that it is not a copy of the main PRD.
9. As a Division runner, I want a contradiction with the main PRD to stop the flow, so that the main PRD stays the source of truth.
10. As a Division runner, I want a missing `docs/prd.md` or `architecture/overview.md` named as the missing step, so that I know what to write first.
11. As a Maintainer, I want every Skill under its Published name, so that installs and cross-references work without a Dev suffix.
12. As a Maintainer, I want every user-facing string in English, so that the Bundle is consistent with the published ss workflow.
13. As a Maintainer, I want one Format file per PRD skill, so that the three templates do not drift.
14. As a Maintainer, I want README, LICENSE and CHANGELOG to describe the release, so that the repo is publishable.
15. As a Maintainer, I want the local `-001` copies untouched, so that my test install keeps working.

## Implementation Decisions

- The Bundle ships five Skills: `ss-division-workflow`, `ss-grilling`, `ss-dev-prd`, `ss-qc-prd`, `ss-ui-ux-prd`. Each is copied from its `~/.agents/skills/ss-*-001/` folder with its reference files, then renamed.
- `ss-division-workflow` has exactly two stages: grilling, then the Division PRD. The spec stage, the ticket stage, the Spec path and Ticket path columns, and every reference to `ss-spec` and `ss-ticket` are removed. The "one feature per spec/ticket run" rule is removed with them.
- The Division table has three columns: Division, PRD skill, PRD path. It maps `dev` → `ss-dev-prd` → `docs/dev/prd.md`, `qc` → `ss-qc-prd` → `docs/qc/prd.md`, and `ui-ux` → `ss-ui-ux-prd` → `docs/ui-ux/prd.md`. A custom Division uses the closest PRD skill and its own `docs/<division-slug>/prd.md`.
- `ss-grilling` is copied unchanged except for its Published name. It is the only stage skill the workflow calls before the PRD.
- Each PRD skill keeps its own `PRD-FORMAT.md`; the three are near-identical but section 11 differs: Dev holds Architecture Dependencies, QC holds Testing Strategy, UI/UX holds Flows & Interface. They are not merged into one generic skill.
- All Indonesian headings and body strings are translated to English: `PRD Divisi` → `Division PRD`, `Ketergantungan Arsitektur` → `Architecture Dependencies`, `Strategi Pengujian` → `Testing Strategy`, `Alur & Antarmuka` → `Flows & Interface`.
- No Skill hardcodes `~/.agents/skills/`. Cross-skill references use the Published name; a reference to another Skill's `SKILL.md` uses a sibling path resolved from the Skill's own base directory.
- A Division PRD skill stops when `docs/prd.md` or `architecture/overview.md` is absent, and names the missing file.
- The workflow skill never writes an Artifact. The grilling and the Division PRD each end at a confirmation Gate, not an automatic next step.
- The repo carries `README.md` (install command with `-g`, flow diagram, one-line list of the five Skills, MIT), `LICENSE` (MIT), and `CHANGELOG.md` with a `1.0.0` entry. The release commit is tagged `v1.0.0`.
- No companion docs: the repo has no tables, endpoints or page routes.

## Testing Decisions

- The seam is the installed Skill files plus the repo's grep checks; there is no runtime code to unit-test.
- Acceptance is the PRD's acceptance criteria: install the Bundle, grep for suffixes, hardcoded paths, Indonesian strings, Sagara names, and `ss-spec`/`ss-ticket`; compare each Skill's frontmatter `name:` to its folder name.
- Prior art: the `ss-workflow` repo's publish-bundle checks, which use the same grep-based acceptance style.
- Manual check: in a project with `docs/prd.md` and `architecture/overview.md`, run the workflow for `dev` and confirm it grills, writes `docs/dev/prd.md`, then stops for confirmation without writing a spec or ticket.
- Manual check: remove `docs/prd.md`, run the workflow, and confirm it stops and names the missing file.

## Out of Scope

- `ss-spec` and `ss-ticket` in this Bundle; the Division flow stops at the Division PRD.
- The main PRD, architecture and AGENTS.md skills.
- An npm package, a Claude Code plugin, or Agent files.
- A Sagara version of the Bundle.
- Merging the three PRD skills into one generic `ss-division-prd`.
- Regenerating or editing the local `~/.agents/skills/ss-*-001` copies.

## Further Notes

- The Host base-directory assumption (a Skill knows its own base directory) is verified on Claude Code and unverified on pi and opencode.
- skills.sh has no publish step; it lists Skills from `npx skills` install telemetry.
- The repo is personal (`ss`) and kept separate from office work.
- The five Skills reference each other by Published name, so they must be installed side by side.
