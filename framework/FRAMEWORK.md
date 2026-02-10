# luca-skills — Framework

How the requirements are implemented. See `REQUIREMENTS.md` for goals and constraints.

---

## Distribution Model

**Public GitHub repo.** The luca-skills repo is publicly readable. Anyone can browse, copy, or fork skills. The Patreon value proposition is curation, ongoing refinement, and support — not access control.

**Dogfooding.** The author (Luca) uses the same install and update flow as every other user. The luca-skills repo is both the development workspace and the distribution source. Meta-skills (create-skill, improve-skill, skills-update, etc.) are distributed alongside domain skills through the same channel.

---

## Repo Structure

```
luca-skills/
├── README.md              ← Human-readable: explains what this is, how to get started
├── INSTALLATION.md        ← Claude-readable: instructions Claude follows to install skills
├── CLAUDE.md              ← Skill routing table (for development and testing)
├── framework/
│   ├── REQUIREMENTS.md    ← Goals and constraints
│   └── FRAMEWORK.md       ← This file
├── skills/
│   ├── skills-review/     ← Meta-skill: review skills for quality
│   │   └── SKILL.md
│   ├── skills-update/     ← The updater (is itself a skill)
│   │   └── SKILL.md
│   ├── skills-integrity-check/ ← Meta-skill: audit installed skills
│   │   └── SKILL.md
│   ├── download-earnings/ ← Domain skill: download SEC filings
│   │   ├── SKILL.md
│   │   ├── template.md
│   │   └── criteria.md
│   └── .../
```

The author tests skills directly from within this repo. Claude discovers `skills/` in the working directory and can invoke them.

---

## Skill Folder Structure

Each skill lives in its own folder. The only required file is `SKILL.md`. All others are optional. A skill folder with just `SKILL.md` is fully functional — the update infrastructure, backlog, and state tracking are conveniences, not prerequisites. Every skill works in a stable form even if no updates are ever applied.

```
skill-name/
├── SKILL.md              ← Procedure + metadata (required)
├── template.md           ← Output format and structure (optional)
├── criteria.md           ← Evaluation focus and signals (optional)
├── pending-updates.md    ← Proposed improvements, written by updater (optional, auto-generated)
└── .skillstate.json      ← Machine-managed state (auto-generated, not for manual editing)
```

### SKILL.md

Contains the procedural description of the skill. Includes YAML front matter for metadata.

```yaml
---
name: earnings-analysis
display-name: Earnings analysis
description: Analyze quarterly earnings reports
last-updated: 2026-02-09T14:56:55Z
inspirations:
  - lucadellanna/luca-skills/skills/earnings-analysis
  - johndoe/earnings-analysis
depends:
  - financial-data-loader
update-behavior: ask before changing procedure, auto-apply presentation changes
---
```

**Metadata fields:**

| Field | Purpose |
|-------|---------|
| `name` | Skill id (kebab-case). Must match the skill folder name. Used for invocation and installation. |
| `display-name` | Optional. Human-readable label used in UI/lists. If omitted, use `name`. |
| `description` | What the skill does (used during installation to help users choose) |
| `last-updated` | Timestamp of last update (ISO-8601 UTC, e.g. `2026-02-09T14:56:55Z`) |
| `inspirations` | List of skills this one learns from. Can be from luca-skills, third parties, or any public source. All treated equally — no privileged "upstream" |
| `depends` | List of other skills this one requires to function |
| `update-behavior` | Optional. Preferred update behavior — e.g. "auto-apply presentation changes, ask for procedural changes" |

**The body** of SKILL.md is the procedure — natural language instructions that Claude follows when executing the skill.

### template.md

Defines how outputs are structured and phrased. Safe for any user to customize. Changes here affect presentation without risking procedural logic.

### criteria.md

Defines what the skill pays attention to: questions, signals, distinctions, evaluation criteria. Primary surface for user judgment and domain preferences. Safe for any user to customize.

### pending-updates.md

Human-readable list of proposed improvements, written by the updater. Users can read this to understand what improvements are available. Not intended for manual editing — the updater manages it.

### .skillstate.json

Machine-managed state file. Tracks installation metadata and skill-specific persistent state.

**Standard fields:**

```json
{
  "enabled": true,
  "skill_timestamp": "2026-02-09T14:56:55Z",
  "installed_from": "https://github.com/lucadellanna/luca-skills",
  "last_checked": "2026-02-09T10:00:00Z",
  "last_updated": "2026-02-01T10:00:00Z",
  "backup_path": ".backups/2026-02-01T10.00.00Z/"
}
```

**Custom fields (skill-specific):**

Skills may store user-provided configuration that should persist across invocations. This avoids re-asking the user on every run.

Example (from `download-earnings`):

```json
{
  "enabled": true,
  "skill_timestamp": "2026-02-09T14:56:55Z",
  "installed_from": "https://github.com/lucadellanna/luca-skills",
  "last_checked": "2026-02-09T10:00:00Z",
  "last_updated": "2026-02-01T10:00:00Z",
  "backup_path": null,
  "sec_contact": "Jane Smith (jane@example.com)"
}
```

The `sec_contact` field is skill-specific — it stores the user's name and email for SEC API requests so they don't have to provide it every time the skill runs.

**Conventions:**
- Standard fields (enabled, skill_timestamp, etc.) are managed by the framework
- Custom fields are skill-specific and documented in the skill's SKILL.md
- Use custom fields for: user preferences, contact info, cached identifiers, and references to secrets stored elsewhere (e.g. a system keychain identifier)
- Do not store: secrets (API keys, tokens, passwords), large data (use separate files), temporary state (use runtime variables)

Not intended for manual editing, but Power Analysts may edit custom fields directly if documented by the skill.

---

## Installation Flow

The repo contains two entry points:

**`README.md`** — Written for the non-technical user. Explains what luca-skills is and gives simple instructions:
1. Install Claude Desktop (or Claude Code CLI).
2. Copy-paste a prompt that points Claude to `INSTALLATION.md`.

**`INSTALLATION.md`** — Written for Claude to read. Contains the instructions Claude follows to install skills on the user's machine.

### What happens when the user pastes the prompt

1. Claude fetches `INSTALLATION.md` from the luca-skills repo.
2. Claude follows its instructions: scans the repo's `skills/` directory, reads each SKILL.md frontmatter.
3. Claude presents available skills to the user in plain language: "Here are the skills available. Which would you like?"
4. User selects (conversationally — "all of them", "just the financial ones", etc.).
5. Claude copies selected skill folders to `~/.claude/skills/`.
6. Claude creates `.skillstate.json` in each installed skill, recording source and timestamp.
7. Claude confirms with example usage: "You can now use these by asking me to [example]."

**No git knowledge required.** Claude handles fetching and copying. The user never sees a terminal, a repo, or a file path (unless they want to).

**No manifest required.** Installed skills are discovered by scanning `~/.claude/skills/`. Available skills in a source repo are discovered by scanning its `skills/` directory and reading SKILL.md frontmatter. No central registry or profile file is needed.

**Enable/disable.** Users can disable an installed skill without removing it. A disabled skill remains on disk but is not invoked or offered. This is managed via `.skillstate.json` (an `enabled` flag) and can be toggled conversationally ("disable the earnings analysis skill") or by the Power Analyst editing the state file.

---

## Usage

Once installed, skills are invoked naturally — no special syntax required for Practitioners.

**Conversational invocation:** The user asks Claude to do something ("analyze these earnings", "review this deal memo"). Claude matches the request to an installed skill based on its `name` and `description` from the SKILL.md frontmatter, loads the skill's procedure, criteria, and template, and executes.

**Explicit invocation:** The user or a Power Analyst can invoke a skill directly by name (e.g. `/earnings-analysis`). This is optional — natural language works the same way.

**Discovery:** Claude knows which skills are available because it scans `~/.claude/skills/` (or the project's `skills/` directory). Disabled skills (per `.skillstate.json`) are skipped.

If a skill has missing dependencies or a broken SKILL.md, Claude should inform the user and suggest running the integrity check (`/skills-integrity-check`) rather than failing silently.

---

## Update Flow (`/skills-update`)

Single entry point. One command for all update activity.

**Trigger:** User says "update my skills" or runs `/skills-update`.

### Phase 1 — Discover and gather

No user-customizable skill files are modified in this phase (e.g. `SKILL.md`, `criteria.md`, `template.md`). This phase may create or update `pending-updates.md` files to save proposed improvements for later review.

1. **Check for new skills:** Fetch latest from the luca-skills repo. Identify any new skills not yet installed. Offer them to the user.
2. **Check each installed skill's inspirations:** For every installed skill (regardless of origin — luca-skills, user-created, or third-party):
   - Read `inspirations` from SKILL.md frontmatter.
   - Fetch latest version of each inspiration source.
   - Claude compares the inspiration source's current state against the version last seen (tracked in `.skillstate.json`). If the source has changed significantly since last check (e.g. multiple revisions), Claude summarizes the net effect rather than proposing each intermediate change — the user sees one consolidated proposal, not five.
   - Extract improvement ideas semantically — based on meaning and intent, not structural comparison.
   - Translate ideas into plain-language proposals, optionally recording provenance (which inspiration source the idea came from).
   - Write or update `pending-updates.md` in the skill folder.
3. **Review backlog:** Claude reviews all pending updates across all skills for staleness, conflicts, and redundancy. Merges proposals that overlap, drops proposals made obsolete by newer ones, and summarizes where the backlog has grown large.

This phase works for any skill — including skills the user created from scratch that have no connection to the luca-skills repo, as long as they declare inspirations.

### Phase 2 — Present and preview (no changes made)

4. Show aggregated proposals across all skills, grouped by skill, in plain language.
5. User selects which to apply: "yes to all", "skip #3", "tell me more about #2", "dismiss all for this skill".
6. For each selected proposal, Claude shows a preview:
   > "This will update [skill name] to also [plain description of what changes].
   > Specifically, I'll modify [which file(s)]."
7. User confirms.

### Phase 3 — Apply

8. Create timestamped backup of all files that will change.
9. Apply changes.
10. Verify: Claude checks that the skill still functions (sanity check / dry run).
11. If verification fails: rollback from backup, inform user.
12. Update `.skillstate.json` with new version and backup path.
13. Mark applied items in `pending-updates.md`. Remove or archive dismissed items.

### Transactionality

If an update touches multiple files within one skill and any change fails verification, all changes to that skill are rolled back. The user sees a clean result: either the update succeeded fully, or nothing changed.

---

## Customization

### Conversational (for Practitioners)

User says: "I want the earnings analysis to focus more on recurring revenue."

Claude identifies the appropriate surface — in this case, `criteria.md` — and makes the change. The procedure/judgment/presentation separation guides Claude toward safe surfaces when the user's intent allows it. No meta-skill required: Claude reads the skill structure and makes the judgment itself.

### Direct editing (for Power Analysts)

User opens `template.md` or `criteria.md` in a text editor and modifies it directly. The framework treats this as a local customization. On the next update, Claude sees the user's version and the proposed change, and proposes a reconciliation rather than overwriting. The user's modifications are always preserved unless the user explicitly chooses otherwise.

### Heavy modification

If a user substantially rewrites `SKILL.md` itself, the skill still functions — it's just natural language instructions. Future upstream learning becomes harder (the gap between the user's version and inspiration sources is wider), but the mechanism still works: Claude reads both, reasons about the intent of the proposed improvement, and proposes how to incorporate it into the user's version. If it can't do this confidently, it asks the user.

---

## Undo

User says: "Undo the last update."

1. Claude reads `.skillstate.json` to find `backup_path`.
2. Restores all files from the backup.
3. Reverts `.skillstate.json` to previous state.

One action, full reversal.

---

## Safety Model

### Skill-owned files

User-customizable files within a skill folder (SKILL.md, template.md, criteria.md, and any other user-authored files) are protected by:
- Automatic timestamped backups before every modification.
- Single-action undo.
- Preview before any change is applied.

Machine-managed files (`pending-updates.md`, `.skillstate.json`, `.backups/`) may be created or updated without backup, since they can be regenerated and are not intended for manual editing.

### User-owned external files

When a skill is instructed to modify a user-owned file outside the skills directory (e.g. a spreadsheet, document, or data file):
- The skill first creates a clearly labeled backup copy next to the original.
- The user is informed of what will change.
- The original is never modified silently.

### Permissions

By default, skills may read from user-approved input locations anywhere on the system, but write only within their workspace. When a skill is explicitly instructed to write to a user-owned external location, the backup-before-modify rule applies.

### Workspace root

All skill-owned artifacts (outputs, caches, logs, backups, and state) live within `~/.claude/skills/`. Each skill's folder is its workspace. This is the single canonical location — portable, predictable, and safe to back up, move, or delete as a unit. This boundary is the framework's primary security boundary.

---

## Integrity Check and Dependencies

The `skills-integrity-check` meta-skill checks:

- **Broken dependencies:** Skills that declare `depends` on skills that are missing or broken.
- **Structural issues:** Missing SKILL.md, malformed frontmatter, or other problems.
- **Stale state:** `.skillstate.json` inconsistencies, orphaned backups.

The audit checks a set of minimal invariants (required frontmatter fields, valid structure, working dependencies). Skills may optionally declare strict compliance (`strict: true` in frontmatter) for tighter validation, or declare explicit exceptions to specific invariants.

This audit covers all installed skills — not just luca-skills originals, but also user-created and third-party skills.

---

## Development Workflow (Author)

The luca-skills repo is both the development environment and the distribution source.

1. Edit skills directly in `luca-skills/skills/<name>/`.
2. Test by running the skill from within the repo (Claude discovers `skills/` in the working directory).
3. Push to GitHub.
4. Run `/skills-update` on own machine — same flow as any user. This dogfoods the entire update experience.

The updater is itself a skill (`skills-update`), so it updates itself through the same mechanism it uses for everything else.
