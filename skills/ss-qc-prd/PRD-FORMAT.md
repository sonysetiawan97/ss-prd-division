# Division PRD Format — QC

One file per Division at `docs/qc/prd.md`. Use the template exactly: the same headings in the same order, nothing added or renamed. A section with nothing decided holds only the project's word for "none decided".

```md
# Division PRD: QC — <project name>

## 1. Overview
1–2 paragraphs: what the QC division verifies and why it matters to the project.

## 2. Goals
3–5 measurable objectives owned by this division.

## 3. Target Users

### 3.1 Persona A
Role, context, and primary need.

### 3.2 Persona B
Role, context, and primary need.

## 4. Functional Requirements

### 4.1 Core Features
The verification work this division must do.

### 4.2 Supporting Features
Capabilities that enhance the core verification.

### 4.3 Integrations
Tools, environments, or platforms this division connects to.

## 5. User Stories
Numbered: "As a <actor>, I want <goal>, so that <benefit>." Top 5–7 only.

## 6. Non-Goals
What this division explicitly does not verify.

## 7. Technical Considerations
Test tooling, environments, data, and constraints that shape the work.

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

## 11. Testing Strategy
Test levels (unit, integration, end-to-end), environments and test data, pass criteria per level, and what is deliberately not tested.

## 12. Acceptance Criteria
Numbered and testable without reading code.

## 13. Changelog
<!-- newest first -->

- **YYYY-MM-DD** — <what changed and why>.
```
