---
name: ss-ui-ux-prd
description: Create or update the UI/UX division PRD at docs/ui-ux/prd.md, derived from docs/prd.md and the architecture. Use after the main PRD and architecture are settled, when the user says "write the UI/UX PRD", or when ss-division-workflow runs the UI/UX division. Synthesizes settled decisions; never interviews.
---

Write or update the PRD for the **UI/UX** division at `docs/ui-ux/prd.md`.

This PRD is derived from the main PRD: it selects the requirements that have a user-facing surface and turns them into flows, states, and interface rules.

## Inputs

1. **`docs/prd.md`** — the main PRD. It must exist; if it does not, stop and say the main PRD comes first.
2. **`architecture/overview.md`** and **`architecture/database-schema.md`** — must exist. The division PRD may rely on them but must not restate them.
3. **`GLOSSARY.md`** and **`architecture/decisions/`** — the project's vocabulary and settled trade-offs.
4. **The division's grilling conversation** — the settled decisions from this division's session.

## Process

1. Read the inputs. Do **not** re-interview; the grilling already happened.
2. Draft from the main PRD: select the requirements, users, and acceptance criteria with a user-facing surface. Every item traces to a main-PRD requirement or a settled decision — say which.
3. Fill `## 11. Alur & Antarmuka`: the screen or flow sequence, the state of each surface (empty, loading, error, success), accessibility rules, and responsive breakpoints.
4. If a requirement contradicts the main PRD, stop and ask the user to update the main PRD first. The main PRD always wins.
5. Write the file using [PRD-FORMAT.md](./PRD-FORMAT.md) exactly: same headings, same order, nothing added or renamed. A section with nothing decided holds only the project's word for "none decided".
6. Append one line to the top of `## 13. Changelog`: date, what changed, why.
7. Show the user the written PRD and the changelog line. Stop for confirmation.

## Rules

- **Never contradict the main PRD.** A contradiction is a main-PRD change, not a division decision.
- **Every surface has states.** A flow that only describes the happy path is unfinished; name the empty, loading, and error states.
- **One decision, one home.** If the architecture already states it, link to it instead of restating it.
- **Update in place.** When the file exists, change the sections that changed and keep the rest.
- Write body text in the project's language; keep headings exactly as [PRD-FORMAT.md](./PRD-FORMAT.md) defines them.
