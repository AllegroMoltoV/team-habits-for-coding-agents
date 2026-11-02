# Team Habits for Coding Agents

AI coding agents fail in the same ways human teams always have. A suggestion quietly becomes a decision. Notes pile up until nobody knows which line is still true. One word means two different things. Work starts on whatever looks easiest.

Software teams found fixes for these long ago: decision records, current-state documents, a shared glossary, dependency-based ordering, independent review. This pack teaches your agent those habits, one skill per failure, and tells it where to write things down so the next session can pick up where this one stopped.

## Who it is for

Developers and small teams who work with Claude Code, Codex or a similar agent in the same repository over many sessions. You decide and approve; the agent implements and keeps records in the repository.

The skills pay off when a later session, or another person, reads what an earlier session left behind. For one-off scripts or tasks that finish in a single session, you will not get much from this pack.

## When each skill helps

- `requirements-vs-means`: you work out the spec of a feature with the agent over several sessions, and you do not want a passing "maybe" or a limit the agent ran into to turn into a requirement.
- `current-state-docs`: you keep specs, design docs, plans and a README in the repository and have the agent update them as the code changes.
- `glossary-and-actors`: the agent writes issues, commit messages, reports or messages for people, and your product has users of its own, so "the user" is ambiguous.
- `ordering-by-dependency`: you have a backlog and ask the agent what to do next.
- `plan-refutation`: you plan a migration or a large refactor and approve the plan before the agent carries it out.
- `record-placement`: the work spans sessions, and decisions or instructions such as "don't push yet" must survive a context compaction or a new session.

## Skills

| Skill | Failure it prevents | What it leaves in your repo |
|---|---|---|
| `start-here` | The agent never loads the other skills (Agensi edition only) | A short table in `CLAUDE.md` / `AGENTS.md` that maps situations to skills |
| `requirements-vs-means` | A proposed means is treated as a requirement | Decisions labelled Confirmed, Provisional or Open |
| `current-state-docs` | Appended corrections bury what is true now | Rewritten documents, history moved to reports, `docs/known-gaps.md` |
| `glossary-and-actors` | One name for two things, or two names for one | `docs/glossary.md`, including the people involved |
| `ordering-by-dependency` | Work starts on the easiest or lowest-numbered task | A dependency-ordered task list with impact-based priorities |
| `plan-refutation` | The agent approves its own plan | One recorded refutation pass by a fresh reviewer |
| `record-placement` | Decisions are written where the next session never looks | Each record in the place that will be read when it is needed |

Each skill is a single `SKILL.md` under `skills/`. There are no scripts and no hooks; the skills only ask the agent to read and write Markdown files in your repository.

## Usage

### From Agensi

The pack is listed for free on [Agensi](https://www.agensi.io). Connect your agent to the Agensi MCP server, then ask it to run `start-here` from this pack once per project. It writes a small table into `CLAUDE.md` and `AGENTS.md`. Agents read those files at the start of every session, so from then on the agent loads the right skill when the situation comes up, without you naming it.

Free Agensi skills are not announced to your agent automatically. Without the table, you have to ask for a skill by name each time.

### From this repository

Copy the skills you want into your project. `start-here` is not needed in this case.

```sh
# Claude Code
mkdir -p .claude/skills
cp -r skills/requirements-vs-means skills/current-state-docs skills/glossary-and-actors \
      skills/ordering-by-dependency skills/plan-refutation skills/record-placement .claude/skills/

# Codex and other agents that read .agents/skills
mkdir -p .agents/skills
cp -r skills/requirements-vs-means skills/current-state-docs skills/glossary-and-actors \
      skills/ordering-by-dependency skills/plan-refutation skills/record-placement .agents/skills/
```

The agent picks a skill from its description when the situation matches. You can also name it: "Use the plan-refutation skill on docs/plan.md."

## Requirements

- An agent that can read and write files in your repository.
- Git is recommended.
- [Beads](https://github.com/gastownhall/beads) (`bd`) is optional. If it is installed, the skills use it for tasks and decisions. If not, they use plain Markdown files under `docs/`.

## Feedback

Questions, bug reports and suggestions are welcome in [Issues](https://github.com/AllegroMoltoV/team-habits-for-coding-agents/issues).

## Origin

These skills are adapted from the author's open rule set for Claude Code, [my-claude-code-rules](https://github.com/AllegroMoltoV/my-claude-code-rules) (Japanese), rewritten as on-demand, agent-neutral skills in English.

## License

MIT License. See [LICENSE](https://github.com/AllegroMoltoV/team-habits-for-coding-agents/blob/main/LICENSE).

## Changelog

| Version | Date | Changes |
|---|---|---|
| 1.2.1 | 2026-11-02 | `start-here`: copy the table word for word in English. An agent told to work in another language translated and shortened it, and the reworded table had not been tested. |
| 1.2 | 2026-11-02 | `start-here`: the table now describes each situation by what the request and the repository show at the start of the work. Agents load skills while they orient themselves, before the first edit, so situations that only arise mid-task were often missed. README: added who the pack is for and when each skill helps. |
| 1.1 | 2026-10-31 | `requirements-vs-means`: requirements derived from a hedged statement stay Open. `requirements-vs-means` and `record-placement`: name people as the project glossary does, not from git config. |
| 1.0 | 2026-10-31 | First release: `start-here` and six skills. |
