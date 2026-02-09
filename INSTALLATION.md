# Installation instructions

These instructions are for Claude to follow. A user has asked you to install skills from the luca-skills collection.

## Step 1: Discover available skills

Scan this repo's `skills/` directory. For each subfolder, read the `SKILL.md` frontmatter to get the `name` and `description`.

Skip any skill where the SKILL.md cannot be read or has no valid frontmatter.

## Step 2: Present skills to the user

If the `AskUserQuestion` tool is available, use it to let the user pick which skills to install. Set `multiSelect: true` so they can choose more than one. Each option should be the skill name, and the question text should briefly describe what each skill does.

If the tool is not available, show a plain-language list instead and ask conversationally:

> Here are the skills available from luca-skills:
>
> - **download-earnings** — Download the last 4 quarterly earnings reports for a company from SEC EDGAR.
> - **skills-review** — Review a skill for quality and framework compliance.
> - **skills-update** — Check for improvements to your skills and apply them.
>
> Which would you like to install? You can say "all of them", pick specific ones, or ask me to tell you more about any of them.

Use the actual skill names and descriptions from the frontmatter.

## Step 3: Install selected skills

For each skill the user selects:

1. Create the directory `~/.claude/skills/{skill-name}/` if it doesn't exist.
2. Copy all files from the repo's `skills/{skill-name}/` into `~/.claude/skills/{skill-name}/`.
3. Create a `.skillstate.json` file in the installed skill folder:

```json
{
  "installed_version": "{version from SKILL.md frontmatter}",
  "installed_from": "https://github.com/lucadellanna/luca-skills",
  "last_checked": "{current ISO timestamp}",
  "last_updated": "{current ISO timestamp}",
  "backup_path": null
}
```

If `~/.claude/skills/` does not exist, create it first.

## Step 4: Confirm

Tell the user what was installed and give example usage:

> Installed 3 skills. You can now use them by asking me to:
> - "Download Apple's earnings reports" (download-earnings)
> - "Update my skills" (skills-update)
>
> Your skills are stored locally and you can customize them anytime — just tell me what you'd like to change.

## Notes

- Do not install skills the user didn't select.
- If a skill lists `depends` in its frontmatter, check whether the dependency is already installed or being installed. If not, tell the user: "[skill] works best with [dependency]. Would you like to install that too?"
- Never show file paths, JSON, or technical details to the user unless they ask.
- This installation works the same way in Claude Desktop, Claude Cowork, and Claude Code CLI.
