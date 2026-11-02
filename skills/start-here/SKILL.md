---
name: start-here
description: Set up the Team Habits pack in a project. Writes a short table into CLAUDE.md and AGENTS.md so the agent loads the right skill from this pack in each situation, without the user naming it. Use once per project, when the user asks to install, set up or start using this pack, or asks which skills it has.
---

# Start here

Skills from this pack are not announced to the agent at session start. The agent only uses them if something tells it to. This skill writes that "something": a table in the instruction files the agent reads at the start of every session.

## Steps

1. Find the slug you used to load this pack. Call the pack listing (`get_skill` with this slug and no path) if you need the exact path of each skill.
2. Check which instruction files exist at the repository root: `CLAUDE.md` (Claude Code) and `AGENTS.md` (Codex, Cursor and most other agents). If neither exists, create `AGENTS.md`. If only one exists, ask the user whether to create the other.
3. Add the block below to each file. If a block between the same markers already exists, replace it instead of adding a second one. Fill in the slug and the paths from the listing. Copy everything else exactly as written, in English, even if the project or the user works in another language. Do not translate, shorten or rephrase the heading, the sentence or the Situation column: the wording was tested so that agents recognize each situation at the start of their work, and a reworded table has not been.
4. Show the user the block you wrote and the files you changed.
5. Ask the user who requests and approves work in this project and how they want to be named in records (for example, their name or handle). Load `glossary-and-actors` and record the answer there. If the user prefers to skip this, continue.

## Block to write

```markdown
<!-- team-habits:start -->
## Team Habits skills

Before acting in the situations below, load the matching skill with the agensi MCP tool `get_skill` and follow it.

| Situation | Call |
|---|---|
| The request settles what a feature must do, the user hedges about what is needed ("maybe", "I think", "might"), or the work will write limits, tools or approaches into a spec, design, plan or decision record | `get_skill {"slug": "<slug>", "path": "<path of requirements-vs-means>"}` |
| The work changes behavior that a spec, design, plan, README or comment describes, or updates any of those documents | `get_skill {"slug": "<slug>", "path": "<path of current-state-docs>"}` |
| The work includes writing an issue, commit message, report, changelog or a message for people, or the user uses a new name for something or mentions a new person or role | `get_skill {"slug": "<slug>", "path": "<path of glossary-and-actors>"}` |
| The user asks what to do next, points to a backlog or list of tasks, or the work has several tasks to order | `get_skill {"slug": "<slug>", "path": "<path of ordering-by-dependency>"}` |
| The work includes writing a plan for multi-step work, or carrying out a plan (even an approved one) | `get_skill {"slug": "<slug>", "path": "<path of plan-refutation>"}` |
| The user makes a decision or gives an instruction meant to last ("from now on", "don't ... until", "remember"), the work may span several sessions, or it produces decisions or check results to write down | `get_skill {"slug": "<slug>", "path": "<path of record-placement>"}` |
<!-- team-habits:end -->
```

## Rules

- This skill is for the Agensi edition. If the skills were copied into the repository instead (for example `.claude/skills/` or `.agents/skills/`), the agent already sees them. Tell the user this skill is not needed and stop.
- Write only the block. Do not copy any other part of this pack into the repository.
- Write the block word for word in English. Only the slug and the paths change. If the user prefers another language, explain the block to them in that language, but keep the block itself in English.
- Keep the block short. Agents read these files every session, and longer instruction files cost tokens without making instructions more reliable.
- If the user declines changes to the instruction files, tell them they can still ask for each skill by name.
