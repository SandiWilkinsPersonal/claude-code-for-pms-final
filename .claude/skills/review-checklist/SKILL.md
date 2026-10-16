---
name: review-checklist
description: Reviews a product brief against the PM's six-point checklist before it goes any further. Use when the user says "review this brief", "run the review checklist", "check this brief", or points at a brief file or wiki page and asks whether it is ready. Checks owner, success measure, scope consistency, problem-before-fix, technical effort, and open questions.
---

# Sandi Product School skill

Review checklist (invoke as `review-checklist`). Run the same six checks, in the same order, on any brief. The user should not have to explain the checks again.

## Input

The brief is whatever the user points at: a file path, a wiki page, or text pasted into the chat. Read all of it, including any "Scope", "Open questions" and "Next step" sections at the end. If you can't tell which brief they mean, ask once.

This is a read-only review. Do not edit the brief unless the user asks you to after seeing the result.

## The six checks

1. **It names who owns it.**
   Look for a named person or a specific role accountable for the work, not just a team. "Owner: Dispatch PM" or "Owner: the product designer" pass. "Product, Dispatch" alone, "TBD", "nobody's picked it up" or no owner at all do not.

2. **It says how we'll know it worked.**
   Look for a success measure someone could actually check: a number, a baseline, and ideally a target or a date. "Fewer tickets" with no baseline is partial. No measure, or only a description of what will be built, fails.

3. **The scope at the end matches the scope at the start.**
   Compare what the opening (problem and proposal) says will be done against the closing parts (scope, "does not do", open questions, next steps). Flag anything promised at the start that the end drops, anything new that appears at the end, and any contradiction between the two. Quote both sides.

4. **It explains the problem before it proposes a fix.**
   The problem, with evidence, must come before the proposal in the document's order. Fail it if the fix is described first, or if the problem is only implied by the solution. Partial if the problem is stated but has no evidence.

5. **It says how much technical effort this is for the dev team.**
   Look for an effort estimate from engineering or a named engineer: a size (small, medium, large), a duration, or a count of people or sprints, plus what it touches (services, shared contracts such as the Responder Availability Record, other teams). "Small enough to ship this afternoon" with no name behind it is Partly. No mention fails. Do not make up an estimate yourself; if there isn't one, say who should give it.

6. **It lists its open questions.**
   Look for an explicit list of what is not yet known or decided, each with an owner or who can answer it. A list with owners passes. Open questions scattered through the text, or a list with no owners, is Partly. If the brief reads as if nothing is open, fail it and say so.

## How to report

Give each check a verdict of **Pass**, **Partly** or **Fail**, then one or two lines of evidence, quoting the brief's own words with the section they came from. Never give a verdict without evidence from the text. If the brief says nothing about a check, say "not stated".

Use this layout:

```
Brief reviewed: <title or path>

1. Owner: <Pass / Partly / Fail>
   <evidence and what's missing>
2. How we'll know it worked: <verdict>
   <evidence>
3. Scope matches start to end: <verdict>
   Start: "<quote>"   End: "<quote>"
4. Problem before fix: <verdict>
   <evidence>
5. Technical effort: <verdict>
   <the estimate and who gave it, or who should>
6. Open questions: <verdict>
   <evidence>

Open questions
- <each question the brief lists, with its owner>
- <any further question this review raised, marked "(raised in review)">

Ready to go further? <Yes / Not yet>
Fix first: <the one to three changes that matter most, in order>
```

The "Open questions" list is always included, even when check 6 fails. If the brief has none, list only the ones the review raised.

"Ready" means no check is Fail. Say "Not yet" if any check fails, and name the fixes. Partly checks are listed under "Fix first" only if they would stop someone acting on the brief.

## Rules

- Judge only what is written. Do not fill gaps with what you know from elsewhere, and do not assume an owner or a target.
- Keep it short. A reviewer should read the result in under a minute.
- Do not add checks of your own. If you notice something else worth mentioning, put it on one line after the result under "Also noticed", and only if it matters.
