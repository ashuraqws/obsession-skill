# obsession-skill

A Claude Code skill that makes Claude obsessive about a task. A worker does the job, then a fresh watcher agent attacks the result. The loop repeats until the watcher finds nothing material left to fix (max 8 rounds).

## Install

In Claude Code:

```
/plugin marketplace add ashuraqws/obsession-skill
/plugin install obsession@obsession-skill
```

## Use

Say "use obsession" or run `/obsession` before your task.

## Safety

Destructive or outward-facing actions (delete, push, send) still need your confirmation.

## License

MIT
