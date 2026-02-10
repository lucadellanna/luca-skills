---
name: skills-improve
description: Analyze a skill for improvement opportunities, implement selected ones, optimize for conciseness, and review. Use when "improve this skill", "make this skill better", "optimize skill".
last-updated: 2026-02-10T12:00:00Z
---

Improve a skill through analysis, targeted changes, and optimization. Works on skills in the `skills/` directory.

Read `framework/REQUIREMENTS.md` and `framework/FRAMEWORK.md` before starting.

---

## Phase 1 — Brainstorm

### 1. Identify target

Determine which skill to improve.

- If the user names one, use it.
- Otherwise, scan `skills/` and ask which one.
- Do not target `skills-improve` itself.

### 2. Read and analyze

Read the skill's full folder: `SKILL.md`, and any `criteria.md`, `template.md`, or other files present.

Assess against the improvement dimensions in this skill's `criteria.md` (`skills/skills-improve/criteria.md`). For each dimension, generate specific, actionable suggestions tied to what you actually read — not generic advice. Reference specific steps or sections.

### 3. Present suggestions

Use `AskUserQuestion` with `multiSelect: true` to present improvement suggestions.

- Number each suggestion.
- For each: what to change, why it matters, which file(s) it touches.
- Group by dimension.

The user may select improvements, ask follow-up questions, or add their own ideas.

---

## Phase 2 — Implement

### 4. Backup

Before modifying files, create a timestamped backup:
- Create `{skill_folder}/.backups/{ISO-timestamp}/`
- Copy all files that will change into it.

### 5. Apply selected improvements

Implement the user's selections. Work file-by-file within the skill folder.

- Preserve existing structure and voice.
- If an improvement requires a new file (e.g. extracting criteria into `criteria.md`), create it.
- Update `last-updated` in SKILL.md frontmatter.

---

## Phase 3 — Optimize

### 6. Optimize for conciseness

Re-read the skill with improvements applied. Assess against the optimization checklist in this skill's `criteria.md`.

Look for opportunities to reduce token count without losing meaning or coverage.

### 7. Present optimization proposals

Show the user what you would tighten, with before/after for significant changes.

Ask for confirmation. If declined, skip to Phase 4.

### 8. Apply optimizations

Apply confirmed optimizations. Update `last-updated`.

---

## Phase 4 — Review

### 9. Run skills-review

Invoke `/skills-review` on the improved skill.

### 10. Summary

Report:
- What was improved and why.
- Approximate token count change (if optimization was applied).
- Any review findings that need attention.
