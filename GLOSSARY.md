# ss-prd-division

The Division layer of the ss workflow, packaged as agent skills and published so it can be installed online: one Division runs grilling, then its PRD.

## Language

**Bundle**:
The full set of `ss-*` skills published together from one repository, because the skills reference each other by name.
_Avoid_: pack, collection, suite

**Skill**:
One `ss-*` folder containing a `SKILL.md` and its reference files.
_Avoid_: command, prompt

**Division**:
A team-scoped slice of a project — Dev, QC, UI/UX, or a custom one — that owns part of the main PRD and has its own `docs/<division-slug>/` folder.
_Avoid_: team, department, unit

**Main PRD**:
The project-level `docs/prd.md` that every Division PRD derives from and may not contradict.
_Avoid_: root PRD, master PRD

**Division PRD**:
The PRD a Division writes at `docs/<division-slug>/prd.md`, derived from the main PRD and the architecture; it selects what the Division owns and depends on.
_Avoid_: sub-PRD, team PRD, second PRD

**Division workflow**:
The `ss-division-workflow` skill that runs one Division through grilling and its Division PRD, stopping at each Gate.
_Avoid_: pipeline, orchestration

**Artifact**:
A document a Skill writes, such as a Division PRD. The Division workflow orchestrates and never writes one.
_Avoid_: output, file, deliverable

**Gate**:
A confirmation stop between stages: the user must approve the grilling and the Division PRD before the next stage starts.
_Avoid_: checkpoint, approval step

**Grilling**:
The interview that sharpens an idea into shared understanding before a PRD is written.
_Avoid_: interview, Q&A

**Published name**:
A Skill's name as users install it, with no version suffix, such as `ss-division-workflow`.
_Avoid_: public name, release name

**Dev suffix**:
The local-only `-NNN` suffix, such as `-001`, added to every Skill name so a test copy can sit beside the published one.
_Avoid_: version, revision

**Host**:
The coding-agent program that loads and runs skills, such as Claude Code, pi or opencode.
_Avoid_: agent, runtime, client

**Format file**:
The single reference file that holds a document's template, such as `ss-dev-prd/PRD-FORMAT.md`.
_Avoid_: template file, schema
