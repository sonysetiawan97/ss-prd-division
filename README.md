# ss-prd-division

The Division layer of the [ss workflow](https://github.com/sonysetiawan97/ss), published as one Bundle: five Skills that run one Division through grilling, then its Division PRD.

## Install

```bash
npx skills add sonysetiawan97/ss-prd-division
```

Global install (Skills available in every project):

```bash
npx skills add sonysetiawan97/ss-prd-division -g
```

The five Skills reference each other by name, so install the whole Bundle; do not copy a single Skill folder.

## The five Skills

| Skill | What it does |
|---|---|
| `ss-division-workflow` | Runs one Division end to end: grilling, then its Division PRD |
| `ss-grilling` | The interview that sharpens an idea into shared understanding |
| `ss-dev-prd` | Writes the Dev division PRD at `docs/dev/prd.md` |
| `ss-qc-prd` | Writes the QC division PRD at `docs/qc/prd.md` |
| `ss-ui-ux-prd` | Writes the UI/UX division PRD at `docs/ui-ux/prd.md` |

## Flow

```
name a Division (dev | qc | ui-ux | custom)
        │
        ▼
   ss-grilling ──► Gate: confirm shared understanding
        │
        ▼
   Division PRD skill ──► Gate: confirm the PRD
        │
        ▼
   docs/<division-slug>/prd.md  — flow stops here
```

The Bundle stops after the Division PRD. Specs and tickets stay in the main workflow.

## Preconditions

A Division run needs, in the project it runs on:

- `docs/prd.md` — the main PRD, which the Division PRD derives from and never contradicts.
- `architecture/overview.md` — the architecture, including the folder map.

## License

MIT — see [LICENSE](./LICENSE).
