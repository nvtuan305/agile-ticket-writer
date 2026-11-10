# Custom issue types

Teams often use issue types beyond Epic, Story, Task, Sub-task and Bug. Map the team's type to the closest of these, keep the team's type name in the output, read the reference file of the mapped type, and apply the adjustments below.

| Team type | Maps to | Adjustments |
|---|---|---|
| Improvement / Enhancement | Story | Describe current versus desired behavior in Context |
| Spike / Research | Task | Add a timebox; the questions to answer become the acceptance criteria; the output is a decision or a short document |
| Tech Debt / Refactor | Task | Explain the risk or cost of not doing it; criteria: behavior unchanged plus a measurable improvement |
| Change Request | Story | Requester, reason for the change, current versus requested behavior, approval needed |
| Incident / Problem | Bug | Timeline, impact window, mitigation taken, follow-up ticket for the root cause |
| Test / QA task | Task or Sub-task | Scope of testing, environments, pass criteria |
| Support / Service request | Task, or Bug if something is broken | Requester, SLA, steps already taken |
| Initiative / Feature (above Epic) | Epic | Longer horizon; epics as child items |

If a type fits none of these, use the shared frame alone and ask the user which sections their team expects.

## Example: Spike

```
Summary: Research how to integrate MoMo payments for the Premium plan
Issue type: Spike   Timebox: 2 days [Assumption]
Epic: Online payments for the Premium plan

## Context
The team needs to understand MoMo's onboarding process, payment methods and
integration risks before it can estimate the payment stories in the epic.

## Objective
Answer the questions below and recommend an integration approach, detailed
enough for the team to estimate the related stories.

## Acceptance criteria (questions to answer)
- [ ] What documents and contracts are needed for a merchant account, and how
      long does approval take?
- [ ] Is there a sandbox environment, and how do we get access?
- [ ] Which payment methods are available, and which fits the Premium plan?
- [ ] How does our system receive payment results, and how should delayed or
      duplicate results be handled?
- [ ] What are the transaction fees, settlement time and refund process?

## Expected outcome / deliverables
- A 1–2 page document answering the questions, with a recommended approach and
  risks.
- A list of proposed stories with rough estimates.

## Out of scope
- Writing the production integration.
- Researching VNPay (separate Spike).

## Open questions / Assumptions
- [Assumption] Timebox of 2 days.
- Does the company already have the legal documents needed to register as a
  merchant?
```
