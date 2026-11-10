---
name: agile-ticket-writer
license: MIT
description: Write and review ready-to-build Jira tickets of any issue type (Epic, Story, Task, Sub-task, Bug, and team-specific types such as Spike, Improvement, Change Request or Incident) using one shared structure plus type-specific sections, written in English from the user and business point of view instead of as implementation notes. Covers outcome-focused summaries, user stories, Given/When/Then acceptance criteria, scope, bug reproduction steps and environment details, sub-task breakdown, INVEST and Definition of Ready checks, and story-point guidance. Use this skill whenever someone asks to write, draft, rewrite, improve, split, or estimate a Jira ticket, issue, epic, story, task, sub-task or bug report; to turn meeting notes, a spec, a chat thread or an error report into tickets; or to check whether acceptance criteria are testable. Trigger even for casual or non-English requests such as "tạo ticket", "viết task", "log bug giúp", "viết user story", or when the user pastes rough notes and asks for a ticket.
---

# Agile Ticket Writer

A good ticket can be understood by someone who was not in the conversation: a PO sees why it matters, a developer can start without a meeting, and QA can verify it without asking anyone.

There are two common ways tickets fail. The first is the vague ticket ("Fix the export") that reads fine on the day it is written, but a week later nobody can build, estimate or verify it. The second is the ticket that is really an implementation plan, full of file paths and class names, so non-technical readers cannot tell what the user actually gets. This skill avoids both.

## Core principles

1. **Describe the outcome, not the implementation.** State what the user or the business gets and how everyone will know it is done. Leave the "how" to the team. When technical details are genuinely useful, put them in an optional **Technical notes** section at the end, so non-technical readers can stop before it.
2. **One shared frame for every ticket type.** Every ticket uses the same backbone (Step 3), then adds the sections for its type. Teams have their own issue types, and a shared frame keeps all of them consistent.
3. **Never invent facts.** When something is unknown, write the best guess, label it as an assumption, and list it under open questions. A visible guess gets corrected; a hidden guess ships.
4. **Write tickets in English.** Write the ticket in English even when the request, notes or source material are in another language, translating the content faithfully. Keep product names, field names and code identifiers unchanged. Quote UI labels and error messages exactly as they appear, adding an English translation in parentheses when they are not in English, because QA needs to match the exact text on screen. Switch the ticket language only if the user explicitly asks for another language. Short notes to the user around the ticket can stay in the user's own language.

## Workflow

### Step 1: Identify the ticket type

Use the type the user names. If none is named, infer it:

- New user-facing capability → **Story**
- Existing behavior that is wrong → **Bug**
- Large initiative spanning several stories, usually more than one sprint → **Epic**
- Work with no direct user-facing behavior (migration, upgrade, configuration, data fix, research with a defined output) → **Task**
- A slice of a parent ticket that one person can finish → **Sub-task**

For a team-specific type (Spike, Improvement, Change Request, Incident, Tech Debt, Test, and so on), map it to the closest of the five types above using `references/custom-types.md`. Keep the team's own type name in the output.

### Step 2: Gather inputs

Take what you can from the conversation, notes, files or linked tickets. Inputs every ticket needs:

- Who is affected: a real role ("billing admin", "warehouse staff"), not just "user"
- The problem and why it matters now, with a link to the source if there is one
- The desired outcome in one sentence
- Known edge cases: empty states, errors, permissions
- Links to designs, specs or related tickets
- Anything explicitly out of scope

Bugs need more (environment and reproduction details); see `references/bug.md`.

If something blocking is missing, for example a bug report with no actual result, ask at most two or three short questions. Otherwise draft right away with labelled assumptions, because a draft the user can react to is faster than a questionnaire.

### Step 3: Draft with the shared frame

Read the reference file for the ticket type before drafting. Each file lists the type-specific sections and shows a worked example:

| Type | Reference file |
|---|---|
| Epic | `references/epic.md` |
| Story | `references/story.md` |
| Task | `references/task.md` |
| Sub-task | `references/sub-task.md` |
| Bug | `references/bug.md` |
| Any other type | `references/custom-types.md`, then the file of the mapped type |

Then fill in this frame:

```
Summary: <80 characters or fewer, specific, outcome-focused>
Issue type: <type>   Priority: <if known or suggested>   Parent / Epic: <if any>
Labels / Components: <if known>

## Context
Why this matters now, who is affected, link to the source.

## <Type-specific sections from the reference file>

## Acceptance criteria
- [ ] Given ..., when ..., then ...

## Out of scope
- ...

## Dependencies & links
- ...

## Technical notes (optional)
Only when the user provided them or they are essential. Keep implementation choices open.

## Open questions / Assumptions
- [Assumption] ...
```

Leave out a section only when it would be empty and is truly irrelevant (for example, Out of scope on a small sub-task). Do not pad sections with filler.

### Step 4: Write acceptance criteria that QA can execute

- Use Given/When/Then, or a checklist when that reads more naturally (common for tasks and sub-tasks). Every line must be verifiable without a conversation.
- Cover the happy path and the important edge cases: empty state, error handling, permissions. A ticket with only the happy path is only half specified.
- Replace vague words with measurable ones: not "loads fast" but "the dashboard loads in under 2 seconds at p95".
- Aim for 3 to 7 criteria. A single criterion usually means missing edge cases; more than about 8 usually means the ticket should be split.
- For bugs, start from the reproduction scenario ("Given the steps above, when ..., then <expected result>") and add a regression check.
- For epics, write exit criteria tied to the success metrics, not screen-level behavior.

### Step 5: Run the quality checks

For stories and story-like custom types, check INVEST and fix what fails instead of only reporting it:

- **Independent**: can be built without waiting on another open story; if not, name the dependency.
- **Negotiable**: states the outcome, not the implementation.
- **Valuable**: the "so that" part names a benefit someone would notice. If you cannot write one, say so rather than faking it.
- **Estimable**: the team could put points on it. Unknowns that block estimation belong in a Spike.
- **Small**: fits in one sprint for one or two people.
- **Testable**: every criterion passes Step 4.

Definition of Ready, for any ticket entering a sprint: clear summary; context with a source; testable criteria including edge cases; dependencies and out of scope noted; designs or specs linked where needed; estimated and small enough to finish. Mention briefly any item that is still missing.

### Step 6: Break the work down when needed

- **Epic**: list candidate child stories and tasks as one-line summaries, each able to become its own ticket.
- **Story or Task**: add sub-tasks when the work exceeds roughly one to two days or involves several people or disciplines (backend, frontend, QA, design). Each sub-task must be completable on its own and start with an action verb. Steps that take half an hour are checklist items in the parent, not sub-tasks.
- **Too big to split into sub-tasks**: propose splitting the story itself, by workflow step, user role, business rule, or happy path versus edge cases.

### Step 7: Estimate, only when asked or when the team uses points

Estimate relative effort, complexity and uncertainty, not hours, using the scale in `references/field-guidelines.md`. At 8 points suggest splitting; at 13 or more split before committing. If estimates differ widely, the ticket is under-specified, so clarify it instead of averaging the numbers.

## Output format

- Default to Markdown. It pastes cleanly into the current Jira Cloud editor and works when issues are created through the Atlassian MCP.
- Use Jira wiki markup (`h2.`, `*bold*`, `{code}`) only if the user says they use Jira Server / Data Center or the legacy editor, or asks for it.
- For several tickets at once (for example an epic and its stories), give each ticket its own block, put the epic first, and show the parent links.
- If you are creating tickets in Jira through a tool, show the draft first and create the issues only after the user confirms, unless they already told you to go ahead.
- After the ticket, add at most two or three lines: assumptions to confirm or Definition of Ready gaps. No long commentary.

## Do not

- Do not write "fix the thing" tickets without context; the context is cheapest to capture now.
- Do not turn a story into an implementation plan (file paths, class names, SQL) in its main sections.
- Do not write acceptance criteria that only restate the summary.
- Do not copy secrets, tokens, passwords or personal data from logs or screenshots into a ticket; redact them.
- Do not commit tickets of 13 points or more as they are, and do not estimate in hours while calling them points.

## Reference files

- `references/epic.md`, `references/story.md`, `references/task.md`, `references/sub-task.md`, `references/bug.md`: sections and a worked example for each type. Read the one for the ticket type in Step 3.
- `references/custom-types.md`: how to map team-specific types (Spike, Improvement, Change Request, Incident, and more), with a Spike example. Read it in Step 1 for any non-standard type.
- `references/field-guidelines.md`: summary, priority, severity, story points, labels and components. Read it when setting these fields or estimating.
