---
name: ordering-by-dependency
description: Decide what to work on next from dependencies and impact-based priorities, not from what looks easy or has the lowest ID. The agent proposes the order; a person approves it before work starts. Use when choosing the next task, planning multi-step work, setting priorities or dependencies, or when the user asks what to do next.
---

# Ordering by dependency

A team without agreed priorities starts on whatever is closest at hand. Agents do the same: the quickest task, the first item in the list, the lowest ID. Then the work that blocks everything else waits.

## Steps

1. List the tasks. If Beads (`bd`) is available, use it. Otherwise keep the list in `docs/tasks.md`.
2. Record dependencies: which task cannot start until another is done (`bd dep add <later> <earlier>` in Beads).
3. Give each task a priority by its impact on whoever receives the result: a customer, the team, or the developer themself. Do not use deadlines or effort as the priority.

   | Priority | Meaning |
   |---|---|
   | P0 | The recipient cannot use the product in production, or data is lost |
   | P1 | Blocks the next delivery |
   | P2 | Does not block delivery, but causes manual work with no workaround |
   | P3 | Affects neither delivery nor operations |
   | P4 | Someday |

   Write these definitions where the labels live (label descriptions, the top of `docs/tasks.md`), so the meaning travels with the label.
4. Order the work: higher priority first. Within the same priority, start with the task that blocks the most other tasks, or that sits on the longest dependency chain to delivery (the critical path). Never choose a task because it is quick or because its ID is small.
5. Show the user the proposed order with the reason for the first few tasks, and wait for approval before starting.
6. When a blocker appears or is resolved, update the dependency and note it on the task right away.

## Output

```markdown
| Order | Task | Priority | Blocked by | Why now |
|---|---|---|---|---|
| 1 | Define CSV columns | P1 | - | Blocks export and tests |
| 2 | Implement export command | P1 | 1 | On the critical path |
| 3 | Add README section | P3 | 2 | No other task depends on it |
```
