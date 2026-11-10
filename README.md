# Agile Ticket Writer

An agent skill that helps Claude write and review **ready-to-build Jira tickets** of any issue type, written from the user and business point of view instead of as implementation notes.

Give it rough notes, a meeting summary, a spec or an error report, and it produces a paste-ready ticket that a PO can understand, a developer can start on without a meeting, and QA can verify without asking anyone.

## Features

- **One shared structure for every issue type**: Context, Acceptance criteria, Out of scope, Dependencies & links, optional Technical notes, Open questions / Assumptions. Each type then adds its own sections.
- **Outcome over implementation**: technical details are kept out of the main sections and moved to an optional *Technical notes* section at the end.
- **Testable acceptance criteria**: Given/When/Then, covering the happy path plus edge cases (empty states, errors, permissions), with a healthy range of 3–7 criteria.
- **Detailed bug reports**: environment, preconditions, steps to reproduce, expected vs actual result, reproducibility, impact, severity and priority, evidence, regression check.
- **Quality checks**: INVEST for stories and a Definition of Ready before a ticket enters a sprint.
- **Breakdown and estimation**: candidate child items for epics, sub-task rules for stories and tasks, and story-point guidance with split recommendations.
- **Custom issue types**: Spike, Improvement, Change Request, Incident, Tech Debt and more are mapped to the closest standard type while keeping your team's type name.
- **No invented facts**: unknowns are written as labelled assumptions and open questions.
- **English tickets from any input**: tickets are always written in English, even when your notes or requests are in another language. Exact UI labels and error messages are kept as they appear, with an English translation when needed.
- **Markdown by default**: pastes cleanly into the Jira Cloud editor and works with the Atlassian MCP; Jira wiki markup on request.

## Supported ticket types

| Type | Type-specific sections |
|---|---|
| Epic | Goals, success metrics, stakeholders, scope, exit criteria, milestones, child items, risks |
| Story | User story statement, design links |
| Task | Objective, background, expected outcome, Definition of Done |
| Sub-task | Parent, what it delivers, done-when checklist |
| Bug | Environment, preconditions, steps to reproduce, expected vs actual, reproducibility, impact, severity, evidence, regression |
| Custom types | Mapped to the closest type above (see `references/custom-types.md`) |

Each type has its own reference file with its sections and a worked example.

## Installation

### Claude.ai and Claude Desktop

1. Download or zip the `skills/agile-ticket-writer` folder (or use a packaged `.skill` file).
2. Upload it in the Skills section of Claude's settings.

### Claude Code

Using the `skills` CLI:

```bash
npx skills add nvtuan305/agile-ticket-writer --skill agile-ticket-writer
```

Or manually, for all your projects:

```bash
git clone https://github.com/nvtuan305/agile-ticket-writer.git
mkdir -p ~/.claude/skills
cp -r agile-ticket-writer/skills/agile-ticket-writer ~/.claude/skills/
```

Start a new Claude Code session so the skill is loaded.

## Usage

Just ask naturally; the skill triggers on ticket-related requests.

```
Write a bug: the revenue report exported to Excel is off by one day compared with the screen.
Create an epic and stories for online payments for the Premium plan.
Turn these meeting notes into Jira tickets: <paste notes>
Are these acceptance criteria testable? <paste criteria>
Write a Spike ticket: research how to integrate a payment gateway.
```

You can also ask in another language, for example Vietnamese. The ticket is still written in English:

```
Viết bug: xuất báo cáo doanh thu ra Excel bị lệch 1 ngày so với màn hình.
Tạo epic cho tính năng thanh toán online gói Premium.
Chia story PROF-21 thành các sub-task.
```

See the files in `skills/agile-ticket-writer/references/` for a full example of each ticket type.

## Repository structure

```
agile-ticket-writer/
├── README.md
├── LICENSE
└── skills/
    └── agile-ticket-writer/
        ├── SKILL.md                  # Workflow, shared ticket frame, rules
        └── references/
            ├── epic.md               # Epic sections + example
            ├── story.md              # Story sections + weak vs good examples
            ├── task.md               # Task sections + example
            ├── sub-task.md           # Sub-task sections + example
            ├── bug.md                # Bug sections, missing-info rules + example
            ├── custom-types.md       # Mapping for Spike, Improvement, Incident... + Spike example
            └── field-guidelines.md   # Summary, priority, severity, story points, labels
```

## Customizing for your team

Team conventions live in the reference files, so you can change one ticket type without touching the others:

- Edit a type's sections or example in its own file (for example `references/bug.md`).
- Rename priority and severity levels, or change the story-point scale, in `references/field-guidelines.md`.
- Add your own issue types to the table in `references/custom-types.md`, or add a new reference file for a type and list it in Step 3 of `SKILL.md`.
- To write tickets in another language by default, change principle 4 in `SKILL.md`.

## References and acknowledgements

This skill was built by combining and extending ideas from the following open-source skills. Thanks to their authors.

- **jira-ticket-writer** by [SkillMedev](https://github.com/SkillMedev) — [source](https://github.com/SkillMedev/skills/blob/main/skills/jira-ticket-writer/SKILL.md).
  Inspired the step-by-step workflow, the outcome-focused user story approach, the acceptance criteria rules (edge cases, measurable wording, 3–7 criteria), the INVEST check, the Definition of Ready, sub-task rules and story-point guidance.
- **jira-ticket-create** from the AlphaAgent Team plugin marketplace (`aai-pm-jira` plugin) — [the-answerai/alphaagent-team](https://github.com/the-answerai/alphaagent-team), also published as `bradtaylorsf/alphaagent-team`.
  Inspired the Epic, Bug and Task templates, the success-metrics table for epics, and the field guidelines for summaries, priority, labels and components.

Additions in this skill include the shared frame for all issue types, one reference file per ticket type with worked examples, the Sub-task type, custom issue type mapping, the extended bug environment and reproducibility sections, severity guidance, English-only output from any input language, and the Markdown-first output rules.

The skill also builds on well-known agile practices: the INVEST criteria (Bill Wake) and the Given/When/Then format from Behavior-Driven Development.

## License

Released under the [MIT License](LICENSE).
