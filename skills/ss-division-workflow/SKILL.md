---
name: ss-division-workflow
description: Run one Division end to end — grilling scoped to the division, then its PRD, spec, and tickets — pausing for confirmation at every gate. Use when the user says "run the dev division", "start QC", "jalankan alur divisi", or wants the full division flow. User-invoked; writes no files itself.
disable-model-invocation: true
---

Run one Division through its whole workflow: **grilling → PRD Divisi → spec → tiket**. The skill orchestrates; it never writes an Artefak itself.

## Argument

One Division slug: `dev`, `qc`, `ui-ux`, or a Division configured for this Project. If the user did not name one, ask which Division to run.

| Division | PRD skill | PRD path | Spec path | Ticket path |
|---|---|---|---|---|
| `dev` | `ss-dev-prd` | `docs/dev/prd.md` | `docs/dev/spec/<feature-slug>.md` | `docs/dev/tickets/<feature-slug>/` |
| `qc` | `ss-qc-prd` | `docs/qc/prd.md` | `docs/qc/spec/<feature-slug>.md` | `docs/qc/tickets/<feature-slug>/` |
| `ui-ux` | `ss-ui-ux-prd` | `docs/ui-ux/prd.md` | `docs/ui-ux/spec/<feature-slug>.md` | `docs/ui-ux/tickets/<feature-slug>/` |

A custom Division uses the closest PRD skill and its own folder: `docs/<division-slug>/`.

## Preconditions

Stop and name the missing step when either file is absent:

- `docs/prd.md` — the main PRD.
- `architecture/overview.md` — the architecture, including Peta Folder.

## Inputs

1. `docs/prd.md` — the main PRD; the division PRD may not contradict it.
2. `architecture/overview.md` and `architecture/database-schema.md`.
3. `GLOSSARY.md` and `architecture/decisions/`.
4. `contract/` — only the documents that mention this Division or its features; not the whole folder.
5. The Division's existing PRD, specs, and tickets, when updating.

## Process

### 1. Grilling

Run `ss-grilling` scoped to the Division. The frontier is the decisions the Division must make that the main PRD and architecture leave open. Do not re-litigate decisions the main PRD or architecture already settled — read them and ask only what is still open. Write glossary terms and ADRs as decisions settle.

Stop when the user confirms the shared understanding.

### 2. PRD Divisi

Run the Division's PRD skill from the table above. It writes `docs/<division-slug>/prd.md` from the main PRD, the architecture, and the grilling decisions. Stop for confirmation before continuing.

### 3. Spec

Run `ss-spec` with the Division's spec path: `docs/<division-slug>/spec/<feature-slug>.md`. Stop for confirmation.

### 4. Tickets

Run `ss-ticket` with the Division's ticket path: `docs/<division-slug>/tickets/<feature-slug>/`. Stop for confirmation.

## Rules

- **Never skip a confirmation.** Grilling, PRD, and spec each end with a question, not an automatic next step.
- **Never write an Artefak.** One Artefak, one writer: the step skill writes it. This keeps the "headings match the template" gate trustworthy.
- **Main PRD wins.** A Division decision that contradicts `docs/prd.md` is a main-PRD change: stop and ask the user to update the main PRD first.
- **One feature per spec/ticket run.** A Division may have many features; run steps 3–4 again for the next feature.
- **Pass the path explicitly.** The vendored `ss-spec` and `ss-ticket` take the Division folder as an argument; never let them fall back to `docs/spec/` or `docs/plan/tickets/`.

## Done when

The Division has a confirmed PRD, a confirmed spec for the current feature, and its tickets, all under `docs/<division-slug>/`.
