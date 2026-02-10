# review-plan

Critically review a strategy or action plan and log feedback.

## What it does

Reads a plan (strategy or action plan), evaluates it against a checklist, and appends a structured review entry to the plan's review log. Never edits the plan directly — only logs feedback.

## Key ideas

- Two review modes: strategy review (is the approach sound? are we solving the right problem?) and action plan review (are tasks complete? sequencing correct? gaps?)
- Strategy checklist: clear goal, accurate context, realistic constraints, simplest viable approach, pre-mortem (what could go wrong)
- Action plan checklist: covers strategy, logical sequencing, tasks specific enough to execute, realistic scope, critical path identified
- Append review entry to review-log.md with: summary, strengths, issues, suggestions, verdict
- Verdicts: NEEDS WORK / READY FOR NEXT PHASE / APPROVED
- If approved, update phase marker in the reviewed file and in todo.md
- Be genuinely critical — the point is to find problems before execution, not rubber-stamp

## Open questions

- Should this support reviewing documents beyond strategy/action-plan (e.g., design docs, RFCs)?
- Should it track review iterations (e.g., "3rd review, 2 issues remain")?

## Post-build

- Delete global `~/.claude/skills/review-plan/` (replaced by this project version, distributed via install flow)
