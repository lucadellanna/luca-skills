# Improvement and optimization criteria

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
