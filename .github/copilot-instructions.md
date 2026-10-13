# Copilot Instructions

## Execution Order

1. Read [docs/status.md](../docs/status.md) first for branch work.
2. Read [docs/project.md](../docs/project.md) for main/master roadmap or project definition updates.
3. Use [docs/prd/00-index.md](../docs/prd/00-index.md) as the PRD entrypoint.

## Response Style

- Be concise.
- Focus only on the current task.
- Do not repeat previous explanations.
- Assume requirements are already understood.
- Explain only new or changed information.
- Prefer code over prose.
- Limit explanations to essential details.
- When modifying existing code, show only the modified section.
- Avoid requirement recap unless explicitly requested.

## Documentation Sources

- PRD source files are under `docs/prd/`.
- Start PRD context from `docs/prd/00-index.md`.
- Keep high-level PRD summary in `docs/prd/01-master-prd.md`.

## Coding Style Source

- Use the two-layer style system in `docs/style/`.
- Layer 1 baseline: `docs/style/coding-style-baseline.md`.
- Layer 2 appendices: `docs/style/language-appendices.md`.
- If a conflict occurs, follow the language appendix for language-specific rules.
