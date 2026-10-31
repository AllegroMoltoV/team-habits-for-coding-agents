---
name: current-state-docs
description: Keep documents that describe the current state readable by rewriting them instead of appending corrections, moving history elsewhere, and tracking doc-vs-code gaps in docs/known-gaps.md. Use when a spec, design, plan, README, code comment, config or task note needs to change, or when a document and the code disagree.
---

# Current-state documents

When every change is appended ("Update: this no longer applies..."), a document turns into a meeting log. The reader, human or agent, has to work out which line is still true. Agents make this worse because they append by default.

## Steps

1. Decide what the document is for.
   - Current state (spec, design, plan, README, code, comments, config, task notes): it must say what is true now.
   - History (reports, changelogs, commit messages, decision logs): it records what happened and is append-only.
2. For a current-state document, edit the existing text in place: replace, delete or merge. Do not add a correction after the old statement, and do not add a branch, fallback or wrapper in code just to keep an old path working.
3. Before you overwrite something worth keeping (a failed approach, the reasoning behind a decision), copy it into a report under `docs/reports/` and link to it if needed.
4. Keep what is still a requirement today, even if it is old: compatibility, migration, safety measures, deliberate history.
5. If a whole document is obsolete, do not delete it. Put a notice at the very top that it is no longer current and link to the document that replaced it.
6. If a document and the implementation disagree and you will not fix it now, add one line to `docs/known-gaps.md`. Delete the line when the gap is closed.
7. Change only the documents your task touches. Do not use this skill as a reason to clean up unrelated files.

## known-gaps.md format

```markdown
# Known gaps

One line per gap between documents and implementation. Delete the line when it is fixed.

- docs/api.md says `limit` defaults to 50; src/api.ts uses 20. (found 2026-11-02)
```

## Comments

A comment that no longer matches the code is a defect. Update or delete it. Comments explain reasons and constraints the code cannot show; they are not a change log.
