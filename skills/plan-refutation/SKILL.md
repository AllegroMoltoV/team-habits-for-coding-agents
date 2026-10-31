---
name: plan-refutation
description: Have a fresh reviewer with no shared context try to break a plan exactly once, then adopt only findings that change the outcome. Use after writing a plan for multi-step work and before showing it to the user for approval or executing it.
---

# Plan refutation

An agent reviewing its own plan tends to confirm it. A reviewer that inherits the same conversation inherits the same assumptions and agrees too. A useful review needs a reviewer that starts cold and is asked to find failure, not to give an opinion.

## Steps

1. Save the plan where it can be read without this conversation (the plan of record: a parent task, or a plan file). The plan should stand on its own: goal, files, URLs, commands, steps and completion criteria.
2. Check whether a refutation is already recorded for this plan. If it is, do not run another one. Revising the plan or starting a new session is not a reason to repeat it.
3. Start a reviewer with fresh context: a new subagent that does not inherit this conversation, a new session, or another agent tool. Do not use a model weaker than the one running now.
4. Give the reviewer only: where the plan is, where the repository is, and the instructions below. Do not pass the conversation, your reasoning, or options you rejected.
5. When the findings come back, adopt only those that affect whether the goal is reached, whether the plan can be carried out, safety, or the completion criteria, plus findings that remove means the goal does not need. Drop style and wording comments, and do not forward dropped findings to the user as concerns.
6. Rewrite the plan with the adopted findings. Do not append them as a list of corrections.
7. Record in the plan of record that the refutation was done, when, by what kind of reviewer, and which findings were adopted.
8. Check that each adopted finding is reflected in the plan, then present the plan to the user. If the refutation did not complete, say so and report your own review as an unresolved concern; do not count it as done.

## Instructions to give the reviewer

```text
List the ways this plan can fail. Start with three questions:
1. Is each means the plan adds necessary for the goal?
2. Which premises are unverified?
3. Is there a simpler way?

Question the means the plan adds, not the goal itself or decisions the
requester has already confirmed.

Only these findings will be used: ones that affect reaching the goal,
feasibility, safety or the completion criteria, and ones that remove
means the goal does not need. Skip style, wording and details that do
not change the result.

For each finding, give the evidence: the file and line you checked, or
the command you ran and its result. Put concerns you cannot back with
evidence in a separate "unverified" section.
```
