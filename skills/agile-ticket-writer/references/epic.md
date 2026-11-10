# Epic

## Purpose

A business initiative made up of several stories and tasks, usually spanning more than one sprint.

## Summary style

A noun phrase naming the initiative, for example "Self-service invoice export for the finance team".

## Sections

Add these after Context in the shared frame:

- **Goals**: two to four outcomes the business wants.
- **Success metrics**: a table of Metric | Baseline | Target | How it is measured. If the numbers are unknown, propose candidate metrics and mark them as assumptions.
- **Users / stakeholders affected**
- **Scope**: In scope and Out of scope, at feature level.
- **Exit criteria**: what must be true to close the epic, tied to the goals and metrics. These replace screen-level acceptance criteria.
- **Milestones / target dates**, if known.
- **Child items**: one-line candidate stories and tasks, each prefixed with its type.
- **Risks & dependencies**

## Example

```
Summary: Custom domains for public profile pages
Issue type: Epic

## Context
Many business customers want their profile page to appear under their own
domain instead of a path on ours. It was the most frequent reason for not
upgrading in the Q3 customer survey [link].

## Goals
- Customers connect their own domain without contacting support.
- More customers upgrade to the paid plan.

## Success metrics
| Metric | Baseline | Target | How it is measured |
|---|---|---|---|
| Domains verified within 24h of being added | n/a | ≥ 90% | Domain status logs |
| Domain-related support tickets per month | n/a | ≤ 10 | Support desk |

## Users / stakeholders affected
Paying customers, support team, infrastructure team.

## Scope
In scope: subdomains, DNS setup instructions, automatic SSL, removing a domain.
Out of scope: apex (root) domains, buying domains inside the app.

## Exit criteria
- [ ] Customers can connect a subdomain from any common domain registrar.
- [ ] Both success metrics meet their targets one month after launch.

## Child items
- Story: Add a custom domain and see DNS setup instructions
- Story: Show domain verification and SSL status
- Story: Serve the profile page on the customer's domain
- Story: Remove a domain when the customer cancels or deletes the account

## Risks & dependencies
- The infrastructure provider charges per custom domain; cost must be confirmed.
```
