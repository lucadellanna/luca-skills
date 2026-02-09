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

## Development

- Skills live in `skills/<name>/`
- Claude discovers them by scanning the `skills/` directory
- Test by running a skill from within this repo
- See FRAMEWORK.md § "Skill Folder Structure" for file conventions
- See FRAMEWORK.md § "Development Workflow" for the full author loop

## Key Rules

- Keep this file and `framework/*.md` concise. Prefer bullets over prose. Edit to tighten, never to expand.
