---
name: verify-in-operation
description: Check that a mechanism meant to run repeatedly works in real operation, on every target it should cover and in non-normal situations, before reporting it as done. Use when you have set up or changed CI, a hook, a scheduled job, linter or formatter config, or agent rules, and are about to report it as done or working.
---

# Verify in operation

A team rolls out a new check, sees it pass once on one machine, and calls it done. Weeks later they find it never ran on half the projects, or that nobody's agent was reading the new rules. Agents repeat this: they write an instruction file and report that "both agents read it", or edit a CI workflow and report that "CI runs it", without anything having run there.

That the mechanism works once, where you built it, is not evidence that it works everywhere it is supposed to. Check the places, not the count of checks.

## Steps

1. **List the targets.** Before checking anything, write down every place the mechanism has to take effect. Think beyond the copy in front of you:
   - every package, directory or project it should cover, including ones added later if the request says so;
   - every agent or tool that must pick it up: each coding agent the project uses, and the subagents they start;
   - every environment it runs in: CI, other operating systems or shells, other people's existing clones, a fresh clone;
   - the way it gets switched on: a hook that is not enabled, or a file that is not committed, does nothing for anyone else.
2. **Check each target where it runs.** Make the target itself show the mechanism working:
   - For agent rules and instruction files, start each agent fresh in the repository (for example `claude -p` or `codex exec`) and ask it a question it can only answer from the new rules. Reading the file yourself proves nothing about whether another agent loads it.
   - For hooks, trigger them through the tool that runs them (a real `git commit`, not running the script by hand), in a clone set up the way the target is.
   - For things that span packages or directories, run it so that each one is exercised, and add a dummy one if the request covers future additions.
3. **Try at least one situation that is not the happy path** and that matters for this mechanism: a case it must block, a fresh clone with nothing set up, the other shell or OS, the mechanism being skipped or bypassed, a missing tool, or the mechanism's own failure (does it fail loudly, or silently pass?).
4. **Mark what you could not check.** Some targets cannot be reached from here: a CI service without network access, someone else's machine, an agent that is not installed. Say so for each one, with what the user has to do to confirm it. Never describe an unchecked target as working.
5. **Report per target, not per check.** End with a table like the one below. Do not summarize as "all checks pass" or count tests as the measure of done.

## When something later turns out not to work

If a target you reported as checked fails in real use, ask why your check did not catch it: a target missing from the list, a check that could not fail, or a situation you did not try. Fix the way you check, and record it with the project's decisions so the next rollout lists that target or situation from the start. Do not only fix the one failure.

## Output

```markdown
| Target | How it was checked | Result |
|---|---|---|
| Agent A (main agent) | Started fresh in a new clone and asked "Which command runs the tests here?" | Answered with the command from the new rules |
| Agent B (main agent) | Same question | Answered from its own instruction file |
| Subagents | Not checked | Ask an agent to start a subagent and repeat the question |
| A teammate's existing clone | Not checked: cannot reach that machine | They enable the hook, then make a test commit that should be blocked |
| CI | Not checked: no network here | Push and confirm a green run |
```

## Rules

- A check that cannot fail is not a check. Before trusting one, make it fail once on purpose.
- Do not count checks or passing tests as evidence that the rollout is complete. The target list is the measure.
- Leave other people's clones and machines unchanged unless the user asked you to change them. Simulate them in a scratch clone instead.
- Keep scratch clones and test files out of the commit, and remove them when you are done.
