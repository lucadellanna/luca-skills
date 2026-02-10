# Improvement and optimization criteria

## Minimal framework and requirements (use by default)

Use this checklist when improving any skill, especially if `framework/REQUIREMENTS.md` and `framework/FRAMEWORK.md` are not available in the current context.

- **Plain language:** Keep user-facing language non-technical. Avoid exposing diffs, git, patches, or internal implementation details unless the user asks.
- **Context portability:** Support both:
  - Project context (a `./skills/` folder in the current workspace)
  - Installed context (skills under `~/.claude/skills/`)
  Avoid hard-coded repo-relative paths (e.g. `skills/<name>/...`) unless guarded by an existence check.
- **Safety model:** Preview → confirm → backup → apply → verify → rollback on failure.
- **Backups:** Use filesystem-safe timestamps for backup folders (replace `:` with `.`).
- **Write boundaries:** By default, write only within the skill folder you are improving (for skill-owned artifacts) or the active workspace (for outputs). Ask before writing elsewhere.
- **Minimum structure:** `SKILL.md` exists; YAML frontmatter is parseable; required fields are present; `last-updated` is ISO-8601 UTC.
- **Separation of concerns:** If the skill is complex enough, keep procedure in `SKILL.md`, evaluation/judgment in `criteria.md`, and output formatting in `template.md`. If the skill is simple, don't over-engineer.

If `framework/REQUIREMENTS.md` and `framework/FRAMEWORK.md` are available, treat them as the source of truth and prefer them over this minimal checklist.

## Improvement dimensions

Assess each dimension below. Skip dimensions where the skill is already strong. Generate suggestions only for genuine gaps — specific and actionable, not generic.

### Completeness
- Missing edge cases or error paths
- Steps that assume a happy path without fallback
- Missing user confirmation before destructive actions
- Undeclared dependencies on other skills or tools

### Robustness
- Steps that could fail silently
- Missing verification after critical actions
- Brittle assumptions about input format, file existence, or responses
- Missing retry or timeout handling for external calls

### Clarity
- Ambiguous steps that could be interpreted multiple ways
- Technical jargon leaking into user-facing language (per REQUIREMENTS.md § Interaction)
- Long steps that should be decomposed
- Missing context on *why* a step matters

### Separation of concerns
- Evaluation criteria embedded in SKILL.md that belong in `criteria.md`
- Output formatting embedded in SKILL.md that belongs in `template.md`
- Only flag if the skill is complex enough to benefit

### Framework compliance
- Frontmatter completeness and correctness
- Missing references to framework docs where appropriate
- Inconsistent use of imperative tone or numbered steps
- Safety model gaps (missing backups, previews, or confirmations)

### Domain accuracy
- Incorrect instructions for the domain (wrong APIs, invalid assumptions)
- Newer or better approaches the skill should adopt

---

## Optimization checklist

Reduce token count without losing meaning or coverage.

**Tighten:**
- Redundant phrasing ("You should then proceed to" → state the action)
- Hedging words that add no meaning ("basically", "essentially", "in order to")
- Repeated instructions across steps — extract once at the top
- Verbose examples — shorten to minimum that conveys the pattern
- Unnecessary meta-commentary about why the skill is structured a certain way
- "Don't do X" instructions where the positive instruction is sufficient
- Passive voice → imperative ("The file should be saved" → "Save the file")

**Preserve:**
- Error handling and edge cases
- User-facing explanations and plain language
- Safety measures (backups, previews, confirmations)
- Domain-specific detail that ensures correctness
