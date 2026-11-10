# Task

## Purpose

Work with no direct user-facing behavior: migrations, upgrades, configuration, data fixes, documentation, or research with a defined output.

## Summary style

Start with an action verb, for example "Upgrade payment SDK to v5" or "Migrate customer avatars to new storage".

## Sections

Add these after Context in the shared frame:

- **Objective**: one sentence on what is true when the task is done.
- **Background**: why it is needed now, including the risk or cost of not doing it. This can replace Context when it covers the same ground.
- **Expected outcome / deliverables**
- **Definition of Done**: a checklist of verifiable items. It serves as the acceptance criteria.

Technical notes may describe the high-level approach, but not a file-by-file plan. If the task will take more than one or two days, propose sub-tasks (see `sub-task.md`).

## Example

```
Summary: Upgrade Node.js from 18 to 22 for the backend service
Issue type: Task   Priority: Medium

## Background
Node.js 18 reached end of life on 30 April 2025 and no longer receives security
patches. Staying on it increases security risk and blocks library upgrades.

## Objective
The backend service runs reliably on Node.js 22 in every environment, with no
change in behavior for users.

## Expected outcome / deliverables
- The service builds and runs on Node.js 22 in dev, staging and production.
- CI/CD and runtime environments use Node.js 22.
- A short note listing the libraries that had to be upgraded and why.

## Definition of Done
- [ ] All automated tests pass on Node.js 22.
- [ ] Staging runs on Node.js 22 for at least 3 days [Assumption] with no new
      errors in the logs.
- [ ] API response times on staging are no more than 10% slower [Assumption].
- [ ] Production runs on Node.js 22, and a tested rollback to Node.js 18 exists.
- [ ] Setup docs for new developers state the new Node.js version.

## Out of scope
- Frontend and other services.
- Adopting new Node.js 22 features (separate tickets if needed).

## Technical notes (optional)
- Review native dependencies and engine constraints in the project config.

## Proposed sub-tasks
- Update dev and CI environments to Node.js 22
- Upgrade incompatible libraries
- Deploy to staging and monitor
- Deploy to production with a rollback plan

## Open questions / Assumptions
- Does the service run in Docker or directly on servers?
- Is there a maintenance window for the production rollout?
```
