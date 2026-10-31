---
name: start-here
description: Set up the Team Habits pack in a project. Writes a short table into CLAUDE.md and AGENTS.md so the agent loads the right skill from this pack in each situation, without the user naming it. Use once per project, when the user asks to install, set up or start using this pack, or asks which skills it has.
---

# Start here

Skills from this pack are not announced to the agent at session start. The agent only uses them if something tells it to. This skill writes that "something": a table in the instruction files the agent reads at the start of every session.

## Steps

1. Find the slug you used to load this pack. Call the pack listing (`get_skill` with this slug and no path) if you need the exact path of each skill.
2. Check which instruction files exist at the repository root: `CLAUDE.md` (Claude Code) and `AGENTS.md` (Codex, Cursor and most other agents). If neither exists, create `AGENTS.md`. If only one exists, ask the user whether to create the other.
3. Add the block below to each file. If a block between the same markers already exists, replace it instead of adding a second one. Fill in the slug and the paths from the listing.
4. Show the user the block you wrote and the files you changed.
5. Ask the user who requests and approves work in this project and how they want to be named in records (for example, their name or handle). Load `glossary-and-actors` and record the answer there. If the user prefers to skip this, continue.

## Block to write

```markdown
<!-- team-habits:start -->
## Team Habits skills

Before acting in the situations below, load the matching skill with the agensi MCP tool `get_skill` and follow it.

| Situation | Call |
|---|---|
| A technical limit, tool or approach is about to become part of a design or requirement | `get_skill {"slug": "<slug>", "path": "<path of requirements-vs-means>"}` |
| A document that describes the current state (spec, design, plan, README, comment, config) needs to change | `get_skill {"slug": "<slug>", "path": "<path of current-state-docs>"}` |
| A new term, role or person appears, or two names seem to mean the same thing | `get_skill {"slug": "<slug>", "path": "<path of glossary-and-actors>"}` |
| Deciding what to work on next, or setting priorities and dependencies | `get_skill {"slug": "<slug>", "path": "<path of ordering-by-dependency>"}` |
| A plan for multi-step work has been written and is about to be shown to the user or executed | `get_skill {"slug": "<slug>", "path": "<path of plan-refutation>"}` |
| A decision, finding or temporary constraint needs to be recorded | `get_skill {"slug": "<slug>", "path": "<path of record-placement>"}` |
<!-- team-habits:end -->
```

## Rules

- This skill is for the Agensi edition. If the skills were copied into the repository instead (for example `.claude/skills/` or `.agents/skills/`), the agent already sees them. Tell the user this skill is not needed and stop.
- Write only the block. Do not copy any other part of this pack into the repository.
- Keep the block short. Agents read these files every session, and longer instruction files cost tokens without making instructions more reliable.
- If the user declines changes to the instruction files, tell them they can still ask for each skill by name.
