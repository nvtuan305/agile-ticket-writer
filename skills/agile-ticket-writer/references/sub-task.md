# Sub-task

## Purpose

A slice of a parent Story or Task that one person can finish on their own, usually within one or two days.

## Summary style

Action verb plus object, for example "Add CSV download button to Invoices page" or "Write QA test cases for invoice export".

## Sections

Keep sub-tasks short; they do not need the full shared frame.

- **Parent**: the parent ticket key.
- **What this delivers**: one or two sentences on how it contributes to the parent's acceptance criteria.
- **Done when**: two to four verifiable checklist items.
- **Notes**, optional.

Sub-tasks can be more technical than stories because developers are the main readers, but they must still state a result, not just an activity. Steps that take half an hour belong as checklist items in the parent, not as sub-tasks.

## Example

Parent story PROF-21: "Let users change their profile picture".

```
Summary: Save new profile pictures and reject invalid images
Issue type: Sub-task   Parent: PROF-21

## What this delivers
Valid images are saved and linked to the profile; images in the wrong format
or over 5 MB are rejected with a clear error message.

## Done when
- [ ] Uploading a valid image saves it and shows it on the profile.
- [ ] Uploading a wrong format or an oversized file returns an error and keeps
      the previous picture.
- [ ] Only the profile owner can change the picture.
```

```
Summary: Write and run QA test cases for changing the profile picture
Issue type: Sub-task   Parent: PROF-21

## What this delivers
Confirms that every acceptance criterion of PROF-21 is met.

## Done when
- [ ] There is a test case for each acceptance criterion of PROF-21.
- [ ] All test cases pass on staging.
```
