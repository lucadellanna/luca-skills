# luca-skills — Requirements

A curated, locally-owned collection of AI skills that non-technical users can install, customize, and keep improving over time through plain conversation — learning from the author's ongoing refinements and from any other public skill, without ever needing to understand the underlying system.

---

## Strategic Context

The value is curation, judgment, and ongoing involvement — not technical exclusivity. Skills are easy to copy by design. The differentiation is active maintenance by someone embedded in the professional community served. Distribution is trust-based (e.g. Patreon): users support continued development because they value the refinement and translation work. The code is not the product — the evolving practice behind it is.

## Core Paradigm

Skills are natural language instructions, not code. Skill updates are therefore natural language changes interpreted by an LLM at runtime — not patches or diffs applied by scripts. This is what makes it possible to learn from skills with different structures, incorporate ideas without merging code, and let non-technical users participate through conversation.

## Users

**Practitioners (~70%)** — interact entirely through conversation (Claude Desktop/Cowork or CLI). Never see files. No CS background needed.

**Power Analysts (~30%)** — comfortable editing markdown files directly. Not expected to know git, diffs, or programming.

Everything must work for both. The framework must never require understanding its internals.

---

## Requirements

Use as a checklist: every framework decision should satisfy these.

### Interaction
- [ ] All user-facing language is plain and non-technical. No diffs, merges, versions, commits, patches, or schemas leak through.
- [ ] Users can install, use, update, customize, and undo without understanding how the system works.
- [ ] Works in both Claude Code CLI (with non-interactive/preview-only paths) and Claude Desktop/Cowork.

### Ownership
- [ ] Skills live locally on the user's machine. Users fully own their files.
- [ ] Customization spans the full range: presentation, judgment, and procedural logic.
- [ ] The framework works for users who never touch files, users who edit safe surfaces, and power users who rewrite skills entirely.

### Separation of concerns
- [ ] The framework encourages (but does not enforce) separating procedure, judgment, and presentation.
- [ ] Users who collapse or blur these boundaries are fully supported.

### Learning from others
- [ ] A skill can declare any number of inspiration sources — from luca-skills, third parties, or any public skill. All are treated equally.
- [ ] The learning mechanism works even if the user has heavily modified the skill.
- [ ] The learning mechanism works even if the inspiration source has a completely different structure.
- [ ] Updates are based on reasoning and intent, not structural comparison. Ideas are extracted and re-expressed in the user's own skill — never merged as code.
- [ ] When a change can't be applied confidently, the system asks rather than guesses.

### Safety
- [ ] No modification silently overwrites user work.
- [ ] Before changing any skill file (SKILL.md, template.md, criteria.md, etc.), the framework backs up the affected files automatically. Before modifying any user-owned external file (e.g. a spreadsheet), the skill creates a labeled backup copy next to the original.
- [ ] Users can undo the last update with a single action.
- [ ] A preview is shown before any modification is applied.
- [ ] Every skill remains usable in stable form even if no updates are ever applied.
- [ ] Skills read from anywhere (with user approval) but write only within the current working context by default — either the skill's own folder in `~/.claude/skills/` for skill-owned artifacts, or the active Claude Code CLI / Cowork workspace for skill outputs and working files.

### Architecture constraints
- [ ] The framework adapts to user behavior through meta-features (meta-skills, commands, safety mechanisms), not by requiring users to follow conventions.
- [ ] Skills are discovered by scanning the filesystem. No manifest, registry, or profile file is required.
- [ ] Skills may depend on other skills. An audit mechanism checks for broken dependencies.
- [ ] The execution environment (e.g. Claude Code) is an implementation detail, not a core dependency.

### Longevity
- [ ] Learning from any skill — including competing ones — is a first-class capability.
- [ ] Updates prioritize explaining *why* an improvement matters, not *how* it's implemented.
- [ ] Local author voice, priorities, and philosophy are preserved when incorporating ideas from others.
- [ ] Users may selectively adopt, delay, or permanently decline improvements.
- [ ] The framework is optimized for slow, compounding value — not rapid feature accumulation.
