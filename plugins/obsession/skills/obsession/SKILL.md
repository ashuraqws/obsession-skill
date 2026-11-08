---
name: obsession
description: Obsessive mode. Use when the user says "use obsession", invokes /obsession, or wants a task pushed until it is genuinely excellent rather than merely done. Works the task, then a separate watcher agent attacks the result; the loop continues until the watcher finds nothing material left to fix.
---

# Obsession

Goal: the task is done well, not just finished. The quality bar is set by evidence, not by feeling.

## Why two agents

The worker is biased toward "it works, ship it". A separate watcher with fresh context and a hostile brief catches what the worker stopped looking at. Keep them apart: the worker never grades its own work.

## Loop

1. **Frame the bar.** Restate the task as 3-7 concrete, checkable criteria (behavior, edge cases, visuals, tests, performance, copy). Write them down before working.
2. **Work.** Do the task. Run the checks the task needs: tests, build, syntax checks, screenshots. Keep raw output out of the main reply.
3. **Watch.** Spawn a fresh watcher subagent (general-purpose, or code-reviewer for code). Its brief: "You are hostile to this work. Find every way it is wrong, weak, unfinished, or untested against these criteria. Cite file:line or evidence. Return a numbered list of material defects, each with severity and the fix. If there are none, say NONE and list what you verified." Do not tell the watcher what the worker believes is fine.
4. **Fix.** Address each material defect. Re-run the checks that cover it.
5. **Repeat** from step 3 with a new watcher. Each watcher is new, not reused, so it has no memory of excusing earlier problems.
6. **Stop** only when a watcher returns NONE with evidence, or after 8 rounds. If round 8 still has defects, stop and report them to the user. Never loop forever.

## Rules

- Material defects only in the loop: broken behavior, missing criteria, untested paths, visual regressions, security issues. Style nits go in a final note, not another round.
- A round that finds nothing new and fixes nothing means the work is done. Do not invent defects to keep going.
- Do not loosen the criteria to get a NONE. If a criterion turns out wrong, say so to the user and change it openly.
- Respect the project's own rules (CLAUDE.md, memory, backups, reply format). Obsession does not override them.
- Destructive or outward-facing actions (delete, push, overwrite user work, send anything) still need the user's confirmation, even in obsession mode.

## Report

End with:
- One-line result.
- `IMPORTANT` for anything the user must decide.
- `WARNING` for defects left open, unverified paths, and rounds used.
- `TIP` for the next step.
