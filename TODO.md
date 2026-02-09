# luca-skills — TODO

## Phase 1: Bootstrap

1. Create repo scaffolding: CLAUDE.md (with skill routing table), skills/ directory
2. Build `skills-review` meta-skill
3. Build `download-earnings` domain skill (given a company, download last 4 earnings reports)
4. Run `skills-review` against `download-earnings` — validate and iterate
5. Test `download-earnings` end-to-end with a real company

## Phase 2: Update loop (proves the core paradigm)

6. Build `skills-update` meta-skill
7. Make an improvement to `download-earnings` in the repo
8. Run `skills-update` from a simulated user install — verify it proposes the change in plain language, previews, applies, and can undo

## Phase 3: Distribution

9. Write README.md (human-readable, for non-technical users)
10. Write INSTALLATION.md (Claude-readable, install instructions)
11. End-to-end test: fresh install from repo, use skill, receive update, undo

## Post-MVP

- `skills-audit` (checks individual skills: dependencies, structure, frontmatter)
- `skills-framework-audit` (checks overall framework against REQUIREMENTS.md)
- `skills-create`
- `skills-improve`
