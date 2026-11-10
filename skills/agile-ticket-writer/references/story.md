# Story

## Purpose

A new or changed capability that a user can see or use.

## Summary style

Follow the team's convention: either the full user story sentence, or a short outcome title ("Export invoices as CSV") with the user story as the first section of the description.

## Sections

Add these after Context in the shared frame:

- **User story**: "As a <role>, I want <capability> so that <benefit>."
- **Design**: links to mockups, or a short description of the expected UI.

Then the shared sections: acceptance criteria, out of scope, dependencies, optional technical notes, open questions. Run the INVEST check from Step 5 before handing the story over.

If the work has no user-facing behavior, do not force an "As a developer, I want ..." story. Use a Task instead (`task.md`).

## Example 1: weak vs good

**Weak:**

```
Summary: Order notification
Description: Build push notification on delivery. Use Firebase, add a
notification_logs table.
Points: 5
```

Why it is weak: no user, no reason, no way to verify it is done, and the description is an implementation choice rather than an outcome. The 5 points are a guess about an unclear scope.

**Good:**

```
Summary: Notify customers when their order is out for delivery
Issue type: Story   Priority: Medium   Epic: ORD-12

## Context
Customer support receives about 150 calls a week asking whether an order has
shipped. Source: October support report [link].

## User story
As a customer who has placed an order, I want to be notified as soon as my
order is out for delivery so that I know when to be available to receive it.

## Acceptance criteria
- [ ] Given an order moves to "Out for delivery", when the status is updated,
      then the customer receives an in-app notification within 1 minute with
      the order number and a tracking link.
- [ ] Given the customer has turned off in-app notifications, when the order
      moves to "Out for delivery", then the customer receives an email instead.
- [ ] Given an order is set to "Out for delivery" a second time (redelivery),
      when the status is updated, then the customer receives a new
      notification that says it is a redelivery.
- [ ] Given sending the notification fails, when 3 retries also fail, then the
      failure is logged so support can look it up by order number.

## Out of scope
- SMS notifications.
- Notifications for other statuses (confirmed, delivered).

## Design
- Notification copy: [Figma link]

## Open questions / Assumptions
- [Assumption] The app already has push permission for signed-in customers.
```

## Example 2: a story that drifted into an implementation plan

**Drifted:**

```
Summary: Implement CSV export
Description: Create ExportController with GET /api/invoices/export, use
csv-writer, stream results from InvoiceRepository.findByTenant(), add an index
on invoices(tenant_id, created_at).
```

**Fixed:** keep the outcome in the main sections and move the useful hints to Technical notes.

```
Summary: Export invoices as CSV for month-end reconciliation

## User story
As a billing admin, I want to export invoices as CSV so that I can reconcile
them in our accounting system without copying data by hand.

## Acceptance criteria
- [ ] Given invoices exist, when the admin clicks "Export CSV" on the Invoices
      page, then a CSV downloads with: invoice ID, date, amount, currency, status.
- [ ] Given no invoices match, when exporting, then a CSV with headers only
      downloads and no error appears.
- [ ] Given a non-admin user, when they open the Invoices page, then the export
      button is not shown.
- [ ] Given 10,000+ invoices, when exporting, then the export either completes
      or shows a visible error; it never silently truncates.

## Technical notes (optional)
- Large tenants may need streaming; an index on tenant and date may help.
  The team decides the approach.
```
