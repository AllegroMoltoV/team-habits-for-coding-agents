---
name: requirements-vs-means
description: Keep proposed means from silently becoming requirements. Labels every decision Confirmed, Provisional or Open, with who decides and when. Use when a technical limit, tool, threshold or approach is about to shape a design or requirement, when the agent proposes a solution, or when an old decision no longer fits new facts.
---

# Requirements vs. means

In meetings, a suggestion often turns into "what we decided" without anyone deciding it. Agents do the same. A limit the agent ran into, or an approach it proposed, shows up in the next plan as if it were a requirement. Later sessions then defend it.

## Steps

1. Separate the statement into two parts: what the user needs (the requirement), and how it could be done (the means). Write both down in one sentence each.
2. For every technical constraint you are about to rely on (a limit, a size, a library, a rate, an API shape), ask whether it is a real requirement or your assumption. Check it against the source: the user's words, documentation, or a measurement. Do not ask the user to change a requirement because of a constraint until you have looked for a way to relax the constraint.
3. Record each decision with a state:

   | State | Meaning | Must also record |
   |---|---|---|
   | Confirmed | The person who approves work in this project has agreed | Who confirmed it, the date, and the reason |
   | Provisional | A working assumption, usually proposed by the agent | The condition that will confirm or drop it, when it will be checked, and who decides |
   | Open | Not decided yet | Who decides, by when, and what information is missing |

4. Anything you proposed starts as Provisional. Only the person who approves work can move it to Confirmed. Never record your own proposal as Confirmed.
5. When the user hedges ("maybe", "I think", "it might be"), treat the statement as Open, not as an instruction. Check the facts or offer options, and give the decision back to them.
6. Store the decisions where the next session will read them. Load `record-placement` if you are not sure where that is.

## Revisiting decisions

A Confirmed decision holds only while its premises hold. If a new fact breaks a premise, say which premise broke and what the evidence is, and propose a review. Do not silently keep following the old decision, and do not reopen a settled decision without a new fact.

## Output

A short decision list, for example:

```markdown
| Decision | State | By / date | Reason or condition |
|---|---|---|---|
| Export uses CSV, not XLSX | Confirmed | Alex, 2026-11-02 | Users import into many tools |
| Files over 10 MB are streamed | Provisional | Decide after the size test on 2026-11-05 (Alex) | Assumed from current data size |
| Include archived tasks | Open | Alex, before planning | Need to know who uses archives |
```
