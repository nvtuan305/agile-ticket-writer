# Field guidelines

## Summary

- 80 characters or fewer, specific and outcome-focused.
- Good: "Add email notification when an order ships". Weak: "Email feature".
- Do not prefix the summary with the type ("[Bug]") when Jira already shows the type.

## Priority (how urgent)

Use the team's own priority names if known.

| Priority | When to use |
|---|---|
| Highest / Blocker | System down, data loss, security issue, no workaround |
| High / Critical | Major function broken, or a deadline at risk |
| Medium | Moderate impact, a workaround exists |
| Low | Minor, cosmetic, nice to have |

## Severity (bugs only, how bad the impact is)

| Severity | Meaning |
|---|---|
| Critical | Crash, data loss, security or money impact |
| Major | Core feature unusable, no workaround |
| Minor | Partly broken, a workaround exists |
| Trivial | Cosmetic or text issue |

Severity and priority can differ: a typo on the login page is trivial in severity but may be high priority before a launch.

## Story points (relative effort, complexity and uncertainty)

| Points | Meaning |
|---|---|
| 1 | Trivial, well understood, under half a day |
| 2–3 | Small and clear, no unknowns |
| 5 | Medium, some complexity or coordination |
| 8 | Large or uncertain, consider splitting |
| 13+ | Too big, split before committing |

## Labels and components

Reuse the team's existing labels and components. Do not create new labels unless asked.
