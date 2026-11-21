---
name: ss-division-workflow
description: Run one Division end to end — grilling scoped to the division, then its Division PRD — stopping for confirmation after each stage. Use when the user says "run the dev division", "start QC", or wants the full division flow. User-invoked; writes no files itself.
disable-model-invocation: true
---

Run one Division through its whole workflow: **grilling → Division PRD**. The skill orchestrates; it never writes an Artifact itself.

## Argument

One Division slug: `dev`, `qc`, `ui-ux`, or a Division configured for this Project. If the user did not name one, ask which Division to run.

| Division | PRD skill | PRD path |
|---|---|---|
| `dev` | `ss-dev-prd` | `docs/dev/prd.md` |
| `qc` | `ss-qc-prd` | `docs/qc/prd.md` |
| `ui-ux` | `ss-ui-ux-prd` | `docs/ui-ux/prd.md` |

A custom Division uses the closest PRD skill and its own folder: `docs/<division-slug>/`.

## Preconditions

Stop and name the missing step when either file is absent:

- `docs/prd.md` — the main PRD.
- `architecture/overview.md` — the architecture, including the folder map.

## Inputs

1. `docs/prd.md` — the main PRD; the division PRD may not contradict it.
2. `architecture/overview.md` and `architecture/database-schema.md`.
3. `GLOSSARY.md` and `architecture/decisions/`.
4. `contract/` — only the documents that mention this Division or its features; not the whole folder.
5. The Division's existing PRD, when updating.

## Process

### 1. Grilling

Run `ss-grilling` scoped to the Division. The frontier is the decisions the Division must make that the main PRD and architecture leave open. Do not re-litigate decisions the main PRD or architecture already settled — read them and ask only what is still open. Write glossary terms and ADRs as decisions settle.

Stop when the user confirms the shared understanding.

### 2. Division PRD

Run the Division's PRD skill from the table above. It writes `docs/<division-slug>/prd.md` from the main PRD, the architecture, and the grilling decisions. Stop for confirmation.

## Rules

- **Never skip a confirmation.** Grilling and the Division PRD each end with a question, not an automatic next step.
- **Never write an Artifact.** One Artifact, one writer: the step skill writes it. This keeps the "headings match the template" gate trustworthy.
- **Main PRD wins.** A Division decision that contradicts `docs/prd.md` is a main-PRD change: stop and ask the user to update the main PRD first.
- **Pass the path explicitly.** The Division PRD skill writes to the Division's PRD path from the table; never let it fall back to another folder.

## Done when

The Division has a confirmed Division PRD under `docs/<division-slug>/`.
