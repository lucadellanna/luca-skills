# skills-plan

Initialize a structured planning cycle for a project or initiative.

## What it does

Creates a planning directory with separate files for strategy (what/why), action plan (how/when), review log (append-only feedback), and decisions (rationale trail). Updates a top-level todo.md as the entry point.

## Key ideas

- Separation of concerns: strategy and action plan are different files because they change at different rates
- Phase markers track progress: DRAFT → REVIEWING → APPROVED → EXECUTING
- Review log is append-only — never edit previous entries
- todo.md is a pointer file only (under 30 lines), no duplicated content
- Decisions file captures rationale so future-you knows why choices were made
- After scaffolding, prompt the user toward the natural next step (fill in strategy, then review)

## Open questions

- Should this skill pair tightly with skills-review-plan, or stay independent?
- Should it support different planning templates (quarterly, project, sprint)?

## Post-build

- Remove global `~/.claude/skills/plan/` and replace with symlink to this project's `skills/plan/`
