---
name: skills-review
description: Review a skill for quality and framework compliance. Use when "review this skill", "check skill quality", "validate skill".
version: 2026-02-09
---

Review one or more skills against the luca-skills framework (`framework/FRAMEWORK.md`).

### 1. Identify target

Determine which skill(s) to review.

- If the user specifies a skill by name, review that one.
- If no skill is specified, scan `skills/` and review all.
- Skip `skills-review` itself (don't self-review).

### 2. Check structure

For each skill folder, verify:

- `SKILL.md` exists (required — everything else is optional)
- YAML frontmatter is present and parseable
- Required frontmatter fields: `name`, `description`, `version`
- No files that don't belong (expected: `SKILL.md`, `template.md`, `criteria.md`, `pending-updates.md`, `.skillstate.json`)

### 3. Check frontmatter

- `name` matches the directory name
- `description` is plain language and explains what the skill does
- `version` is a date in YYYY-MM-DD format
- If `inspirations` is present, each entry is a recognizable path (e.g. `owner/repo/path` or URL)
- If `depends` is present, each listed skill exists in `skills/`

### 4. Check procedure quality

Read the SKILL.md body and assess:

- Uses numbered steps with descriptive headers
- Imperative tone ("Do X", not "You should X")
- User-facing language is plain and non-technical (per `framework/REQUIREMENTS.md` § Interaction)
- References external files by path rather than embedding large blocks inline
- Covers the full workflow, not just the happy path

### 5. Check separation of concerns

This is a suggestion, not a hard rule. Flag if:

- Evaluation criteria are embedded in SKILL.md instead of living in `criteria.md`
- Output formatting is embedded in SKILL.md instead of living in `template.md`
- The skill is simple enough that separation would be over-engineering (note this and don't flag)

Reference: `framework/FRAMEWORK.md` § "Skill Folder Structure"

### 6. Report

Present findings grouped by severity:

**Errors** (must fix before the skill is usable):
- Missing SKILL.md
- Missing or unparseable frontmatter
- Missing required frontmatter fields (`name`, `description`, `version`)
- Broken dependencies (listed in `depends` but not found)

**Warnings** (should fix):
- `name` doesn't match directory name
- `version` isn't a valid date
- Technical jargon in user-facing language
- Procedure lacks numbered steps or uses passive tone

**Suggestions** (consider):
- Separation of concerns could be improved
- Optional files (template.md, criteria.md) might benefit the skill
- Description could include more trigger phrases

If no issues are found, say so: "Skill passes all checks."
