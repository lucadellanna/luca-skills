# skills-hook

Help users configure Claude Code hooks through conversation.

## What it does

Guides the user through setting up automation hooks: what event triggers it, what tool/action it matches, and what command to run. Writes the result into settings.

## Key ideas

- Reference table of hook events (PreToolUse, PostToolUse, Stop, SessionStart, etc.) and hook types (command, prompt, agent)
- Walk through: trigger event → matcher pattern → command/action → write to settings file
- Matcher is a regex string, not an object — easy to get wrong
- Hooks activate next session, not the current one — tell the user
- Hook commands run from project root
- Settings go in `.claude/settings.local.json` (gitignored, local only)

## Open questions

- Should this skill also support editing/removing existing hooks?
- Should it offer common hook templates (e.g., lint on save, test on commit)?

## Post-build

- Remove global `~/.claude/skills/add-hook/` and replace with symlink to this project's `skills/hook/`
