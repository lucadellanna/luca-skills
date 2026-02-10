# skills-consolidate

Find duplication and single-source-of-truth violations across skills.

## What it does

Scans a set of skills (global, project, or both) and identifies overlapping procedures, duplicated content, conflicting triggers, and opportunities to extract shared patterns into frameworks or templates.

## Key ideas

- Look for: duplicate steps across skills, overlapping trigger phrases, same information in multiple places, embedded templates that should be files
- Categorize findings by severity: must-fix (SSOT violations, conflicts), should-fix (heavy duplication), nice-to-have (minor overlaps)
- For each finding, propose a resolution: extract to framework, merge skills, create reference chain, extract to template, or acknowledge intentional duplication
- Estimate effort/risk/value for each proposal, then prioritize
- Implement approved changes one at a time if the user wants

## Open questions

- Should this also detect unused or orphaned skills?
- How to handle cross-project duplication (same skill installed in multiple projects)?

## Post-build

- Remove global `~/.claude/skills/consolidate-skills/` and replace with symlink to this project's `skills/skills-consolidate/`
