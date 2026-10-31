---
name: glossary-and-actors
description: Maintain one project glossary, docs/glossary.md, that defines terms and also the people and roles involved, so records say who decided what. Use when a new term, role or person appears, when two names seem to mean the same thing, when the agent is about to write "the user" in an issue, commit or report, or when start-here asks who approves work.
---

# Glossary and actors

Without shared definitions, one word ends up meaning two things. The most damaging case is "the user". An agent calls the person it works for "the user", but the product also has users. An issue that says "the user approved this" no longer tells a reader whether the developer approved a change or a customer asked for it.

## Steps

1. Keep a single glossary at `docs/glossary.md`. If the project already has one elsewhere, use that file instead and do not create a second.
2. Define each term once, in the glossary. Other documents link to the glossary instead of repeating the definition.
3. Include the actors, not only domain terms:
   - The person who requests and approves the agent's work. Record them by name or handle. In issues, commits, reports and decision logs, write that name, never "the user".
   - The people who use the product. Reserve the product's own word for them (for example "user", "customer", "player").
   - Other roles that appear in decisions (reviewer, client, team).
4. When you find two names for one thing, pick one, record the other as an alias, and use the chosen name from now on.
5. When you find one name used for two things, split it into two entries and fix the documents your task touches.
6. When a definition changes, rewrite the entry. Do not append a correction (see `current-state-docs`).
7. If the glossary and the code disagree, trust neither blindly. Check the code, then fix the glossary or record the gap in `docs/known-gaps.md`.

## Format

```markdown
# Glossary

## People and roles

| Name | Who | Notes |
|---|---|---|
| Alex | Developer of this project. Requests and approves the agent's work. | Write "Alex" in records, not "the user". |
| User | A person who uses the todo app. | Product users only. |

## Terms

| Term | Definition | Aliases |
|---|---|---|
| Task | One item in the todo list, stored in tasks.json. | todo, item |
```
