# Division PRD Format — UI/UX

One file per Division at `docs/ui-ux/prd.md`. Use the template exactly: the same headings in the same order, nothing added or renamed. A section with nothing decided holds only the project's word for "none decided".

```md
# Division PRD: UI/UX — <project name>

## 1. Overview
1–2 paragraphs: what the UI/UX division designs and why it matters to the project.

## 2. Goals
3–5 measurable objectives owned by this division.

## 3. Target Users

### 3.1 Persona A
Role, context, and primary need.

### 3.2 Persona B
Role, context, and primary need.

## 4. Functional Requirements

### 4.1 Core Features
The user-facing capabilities this division designs.

### 4.2 Supporting Features
Capabilities that enhance the core experience.

### 4.3 Integrations
External services, APIs, or platforms this division connects to.

## 5. User Stories
Numbered: "As a <actor>, I want <goal>, so that <benefit>." Top 5–7 only.

## 6. Non-Goals
What this division explicitly does not design.

## 7. Technical Considerations
Design tooling, component library, accessibility, and constraints that shape the work.

## 8. Milestones
| Phase | Milestone | Description | Timeline |
| :---- | :-------- | :---------- | :------- |
|  |  |  |  |

## 9. Success Metrics
2–4 metrics with targets.

## 10. Risks & Mitigations
| Risk | Impact | Mitigation |
| :--- | :----- | :--------- |
|  |  |  |

## 11. Flows & Interface
Screen or flow sequence, the state of each surface (empty, loading, error, success), accessibility rules, and responsive breakpoints.

## 12. Acceptance Criteria
Numbered and testable without reading code.

## 13. Changelog
<!-- newest first -->

- **YYYY-MM-DD** — <what changed and why>.
```
