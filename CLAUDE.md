# luca-skills

Curated AI skills that non-technical users install, customize, and improve over time through plain conversation.

## Context

- `framework/REQUIREMENTS.md` — goals and constraints
- `framework/FRAMEWORK.md` — architecture and flows

## Available Skills

| Skill | Purpose | Trigger phrases |
|-------|---------|-----------------|
| `/skills-review` | Review a skill for quality and framework compliance | "review this skill", "check skill quality", "validate skill" |
| `/download-earnings` | Download last 4 quarterly earnings filings from SEC EDGAR | "download earnings", "get earnings reports", "fetch 10-Q" |
| `/skills-update` | Check for skill improvements and apply them | "update my skills", "check for updates", "skills update" |
| `/skills-integrity-check` | Check installed skills for broken dependencies and inconsistent state | "check my skills", "integrity check", "find broken skills" |
| `/skills-improve` | Analyze a skill for improvements, implement them, optimize, and review | "improve this skill", "make skill better", "optimize skill" |
| `/reflect` | Structured reflection after complex work — extract insights and propose actions | "reflect on this", "what did we learn", "session recap" |
| `/create-skill` | Create a new skill with proper structure | "create a skill", "new skill for", "add a skill" |

## Development

- Skills live in `skills/<name>/`
- Claude discovers them by scanning the `skills/` directory
- Test by running a skill from within this repo
- See FRAMEWORK.md § "Skill Folder Structure" for file conventions
- See FRAMEWORK.md § "Development Workflow" for the full author loop

## Key Rules

- Keep this file and `framework/*.md` concise. Prefer bullets over prose. Edit to tighten, never to expand.
- Naming: reserve the `skills-*` prefix for skill-maintenance operations (e.g., `skills-review`, `skills-update`, `skills-improve`, `skills-integrity-check`). Use plain names for general-purpose workflows (e.g., `reflect`, `create-skill`).
