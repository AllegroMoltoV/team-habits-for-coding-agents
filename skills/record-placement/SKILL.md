---
name: record-placement
description: Put each decision, finding and temporary constraint where the next session will actually read it, chosen by when it will be needed next. Records facts as they become true instead of at the end of the session, and keeps one source of truth. Uses Beads (bd) if installed, plain Markdown otherwise. Use when a decision is made, a check passes or fails, a blocker appears or clears, the user gives an instruction that should outlive the conversation, or the user says "remember this".
---

# Record placement

A decision the user already made, written somewhere the next session never reads, will be asked again. That spends the user's time on a question they already answered. Conversation history, compaction summaries and handoff notes do not survive reliably.

## When to record

Record a fact when it becomes true, not at the end of the session. Sessions end without warning: context compaction, a closed terminal, the user walking away. Writing as you go means a break loses minutes, not the session.

| Event | Record it |
|---|---|
| A direction was chosen | On the task. Also as a lasting project rule if it will keep applying |
| A check passed or failed | On the task, with how it was checked |
| A blocker appeared or cleared | On the task, plus the dependency |
| Follow-up work was found | As a new task, not as a note on the current one |
| The user set a temporary constraint ("don't push yet") | As a lasting project note with a key that includes the session, removed when lifted |

## Where to put it

Choose by the next situation in which the record will be needed.

| Content | Needed when | Place |
|---|---|---|
| History and verification of one task | Someone opens that task | Task notes; the closing reason when done |
| Knowledge or decisions for this repository | Any later session in this repository | Project memory (`bd remember --key <key>`) or `docs/decisions.md` |
| Conventions for all projects, the user's preferences | Any project | The user's global instruction files |
| Facts about one machine | Work on that machine | A machine-local instruction file |

Know what the next session sees without being asked:

| Place | Read automatically next session? |
|---|---|
| Instruction files (`CLAUDE.md`, `AGENTS.md`, rule files) | Yes |
| Beads project memory (`bd remember`) | Yes, if Beads session hooks are installed |
| Open task titles | Usually only titles; bodies need `bd show` or opening the file |
| Closing reasons and notes on closed tasks | No |

So never put a decision that must keep applying only in a closing reason or a note on a closed task.

## Rules

- One fact, one place. Do not copy the same decision into several files; one copy will go stale.
- Task notes and project memory describe the current state. Rewrite outdated entries; update project memory by its key so the old entry does not survive beside the new one.
- Before overwriting history worth keeping (approaches that failed, how a decision was reached), move it to `docs/reports/`.
- Write how each fact was verified. Mark anything unverified as unverified.
- When closing a task, write what was done and how it was verified, or that it was not verified.

## Without Beads

Use plain files instead: `docs/tasks.md` for tasks and their notes, `docs/decisions.md` for lasting decisions (with the states from `requirements-vs-means`), and a short pointer in `AGENTS.md` or `CLAUDE.md` so the next session opens them.
