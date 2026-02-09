---
name: skills-integrity-check
description: Check installed skills for broken dependencies, malformed metadata, and inconsistent state. Use when "check my skills", "integrity check", "find broken skills".
last-updated: 2026-02-09T14:56:55Z
---

Audit installed skills for common problems: broken dependencies, malformed frontmatter, and inconsistent `.skillstate.json`.

Do not modify any files unless the user explicitly asks you to fix issues.

### 1. Locate installed skills

Scan for skill folders:
- In production: `~/.claude/skills/`
- In development: `skills/` in the current working directory

Each subfolder containing a `SKILL.md` is a skill.

### 2. Check each skill's structure

For each skill folder:
- `SKILL.md` exists and contains parseable YAML frontmatter
- Required frontmatter fields exist: `name`, `description`, `last-updated`
- `name` matches the folder name (skill id)
- `last-updated` is an ISO-8601 UTC timestamp (e.g. `2026-02-09T14:56:55Z`)
- If `depends` is present, each listed dependency exists as a skill folder

### 3. Check `.skillstate.json` (if present)

If the skill folder contains `.skillstate.json`, verify:
- JSON is parseable
- `enabled` is present and is a boolean
- `skill_timestamp` exists (string)
- `installed_from` exists (string) if the skill was installed from a repo
- `last_checked` and `last_updated` (if present) are ISO timestamps
- If `backup_path` is non-null, the referenced backup directory exists

### 4. Check backups (if present)

If the skill folder contains `.backups/`:
- If `.skillstate.json.backup_path` exists, confirm it points to a directory inside `.backups/`
- Flag any obviously orphaned backups (directories in `.backups/` that are not referenced by any `backup_path`)

### 5. Report findings

Report issues grouped by severity:

**Errors** (broken or unsafe):
- Missing/unparseable SKILL.md frontmatter
- Missing required frontmatter fields
- Broken dependencies
- Unparseable `.skillstate.json`
- `backup_path` points to a missing directory

**Warnings** (should fix):
- `name` doesn't match folder name
- `last-updated` not a valid ISO-8601 UTC timestamp
- Missing `enabled` in `.skillstate.json`
- Orphaned backup directories

**Suggestions** (nice to have):
- Add `display-name` for better UI presentation
- Add `criteria.md` / `template.md` to separate concerns

If no issues are found, say so: "All skills look healthy."
