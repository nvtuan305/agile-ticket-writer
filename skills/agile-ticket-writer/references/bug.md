# Bug

## Purpose

Existing behavior differs from what it should be.

## Summary style

"<Where>: <what goes wrong> (<when / condition>)", for example "Invoices page: CSV export is empty when filtering by date range". Describe the symptom, not the suspected cause.

## Sections

Use these sections, in this order. They replace Context in the shared frame.

1. **Problem summary**: one or two sentences.
2. **Environment**
   - Environment: Production / Staging / UAT / Dev
   - App version, build or release (commit hash if known)
   - Platform: browser and version, OS, device; or API client, mobile app version
   - Account, role or tenant used to reproduce (never passwords)
   - Relevant data or configuration: feature flags, language, timezone, plan
   - First seen: date and time with timezone, and since which version if known
3. **Preconditions**: the state needed before step 1, for example "logged in as a billing admin with at least one invoice".
4. **Steps to reproduce**: numbered, one action per step, with exact inputs, test data and URLs.
5. **Expected result**
6. **Actual result**: the exact error message or code, plus request or trace IDs when available. Quote messages in their original language and add an English translation in parentheses if needed.
7. **Reproducibility**: Always / Intermittent (for example, 3 out of 10 attempts) / Happened once, not reproduced.
8. **Impact**: who and how many are affected, business impact, and whether a workaround exists.
9. **Severity and Priority**: suggest both (see `field-guidelines.md`).
10. **Evidence**: screenshots, recordings, logs trimmed to the relevant lines, with secrets and personal data redacted.
11. **Regression?**: did this work before, and in which version?
12. **Acceptance criteria**: the reproduction steps now produce the expected result; relevant variants also work; a regression test covers the case.

Then add the shared Dependencies & links and Open questions / Assumptions sections when they have content.

## When information is missing

Reproduction steps and the actual result matter most, because a bug that cannot be reproduced cannot be verified as fixed. If the user cannot provide them, reconstruct the steps from the description, label them as an assumption, set Reproducibility to "Unknown, needs reproduction", and list the gaps under Open questions.

## Example

```
Summary: Invoices page: CSV export is empty when filtering by date range
Issue type: Bug   Priority: High   Severity: Major

## Problem summary
Exporting invoices to CSV returns a file with only the header row whenever a
date-range filter is applied, even though the page shows matching invoices.

## Environment
- Environment: Production
- Version: web app 4.18.2
- Platform: Chrome 131 on macOS 15; also reproduced on Edge 131 / Windows 11
- Account: billing admin role, tenant "acme-demo"
- Timezone: Asia/Ho_Chi_Minh (UTC+7)
- First seen: 2026-11-03 09:20 UTC+7, after release 4.18.0

## Preconditions
Logged in as a billing admin in a tenant with invoices dated in October 2026.

## Steps to reproduce
1. Open Billing > Invoices.
2. Set the date filter to 01/10/2026 – 31/10/2026 and click Apply.
3. Confirm the table lists invoices (42 rows in acme-demo).
4. Click "Export CSV".

## Expected result
The CSV contains the same 42 invoices shown in the table.

## Actual result
The CSV contains only the header row. No error is shown.
Request ID of the export call: 7f3c-91ab (from the browser network tab).

## Reproducibility
Always (5/5). Exporting without a date filter works correctly.

## Impact
Finance cannot export monthly invoices for reconciliation (month-end close on
2026-11-05). Workaround: export without a filter and filter in a spreadsheet,
which is slow for large tenants.

## Evidence
- Screen recording: [link]
- Exported file: [attached]

## Regression?
Yes. Worked in 4.17.x.

## Acceptance criteria
- [ ] Given the steps above, when the user exports, then the CSV contains
      exactly the invoices shown in the filtered table.
- [ ] Given a date range with no invoices, when the user exports, then the CSV
      contains only the header row and the page shows "No invoices to export".
- [ ] Given a range crossing a timezone boundary (an invoice at 23:30 UTC+7 on
      the last day), when exported, then that invoice is included.
- [ ] A regression test covers export with a date filter.

## Open questions / Assumptions
- [Assumption] Other filters (status, customer) are unaffected; not yet verified.
```
