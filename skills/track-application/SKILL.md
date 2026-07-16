---
name: track-application
description: "Log a new application or check pipeline status. Argument: [company] [role] [status: applied/screening/interview/offer/rejected]"
---

You are managing the user's job application pipeline.

## STEP 1: Read current memory

Read `${CLAUDE_PLUGIN_ROOT}/references/CUSTOMIZATION_MEMORY.md` to understand current patterns and what has been learned.

## STEP 2: Determine the action

Based on the user's input:

**If logging a new application:**

- Extract: company name, role title, date applied, source (referral / direct / recruiter)
- Determine company type (AI / Consumer / Enterprise / Fintech / Telco)
- Confirm: was the resume and cover letter generated using this plugin?
- Ask: any customizations made that worked well?

**If updating an existing application:**

- Extract: company, new status, outcome notes
- If rejected: what was the stated reason? What can we learn?
- If progressing: what round, who is interviewing?

**If checking pipeline:**

- Summarize all open applications by status
- Flag any applications needing follow-up (no response after 7 days)
- Show conversion rates by company type

## STEP 3: Update CUSTOMIZATION_MEMORY.md

Read the current `CUSTOMIZATION_MEMORY.md`, then propose specific additions to the "Successful Patterns" or "Unsuccessful Patterns" sections based on the outcome.

Write the updated file back to: `${CLAUDE_PLUGIN_ROOT}/references/CUSTOMIZATION_MEMORY.md`

Format additions as:

```
#### [Company Type] - [Company Name] - [Outcome]
Date: [date]
Resume strategy: [what was emphasized]
Cover letter hook: [what opener was used]
Result: [screen / reject / offer / pending]
Learning: [what this tells us for future applications]
```

## STEP 4: Persist the structured tracker (machine-readable — required)

`CUSTOMIZATION_MEMORY.md` holds the *prose* learnings. It is NOT queryable, so it cannot drive the `patterns` (rejection analysis) or `followup` (cadence) skills. Those skills read a structured tracker instead. Maintain it here.

Read (create if missing) `${CLAUDE_PLUGIN_ROOT}/references/applications.md`. It has exactly one table with this schema — keep the columns in this order:

```markdown
# Application Tracker

| Num | Company | Role | Type | Status | Applied | Source | Score | Outcome reason | Contact | Last follow-up |
|-----|---------|------|------|--------|---------|--------|-------|----------------|---------|----------------|
| 1   | Northstar AI | Director of Product | AI | applied | 2026-06-30 | referral | 4.2 | — | jane.recruiter@northstar.example | — |
```

Field rules:
- **Num** — sequential, never reused.
- **Type** — AI / Consumer / Enterprise / Fintech / Telco / Other.
- **Status** — one of: `evaluated`, `applied`, `screening`, `responded`, `interview`, `offer`, `rejected`, `discarded`, `skip`. Use these exact tokens (the `patterns`/`followup` skills classify on them). `discarded` = went dead with no formal rejection; `skip` = self-filtered before applying.
- **Applied / Last follow-up** — `YYYY-MM-DD`.
- **Score** — the evaluation score (X.X/5) if the role was evaluated; else `—`.
- **Outcome reason** — on `rejected`/`discarded`/`skip`, the stated or inferred reason (e.g. "geo-restricted", "stack mismatch", "seniority gap"). This is what `patterns` mines — never leave it blank on a negative outcome.

On a new application: append a row. On an update: rewrite the existing row in place (build the new row as a fresh line, don't mutate columns piecemeal). Write the file back. If the file still contains the shipped fictional example rows, delete them when appending the first real row.

## STEP 5: Output pipeline summary

Always end with a pipeline summary table (derived from `applications.md`):

```
APPLICATION PIPELINE

| Company | Role | Status | Date | Follow-up Needed? |
|---------|------|--------|------|-------------------|
| [name]  | [role] | [status] | [date] | [yes/no] |

Conversion Rates:
- Applications to screens: X%
- Screens to interviews: X%
- Interviews to offers: X%

Patterns Working: [what's getting responses]
Patterns to Change: [what's not working]
```

If there are fewer than 5 applications, note: "Pipeline is thin — consider expanding outreach or applying to more roles."

When the tracker has 5+ outcomes, suggest: "Run the `patterns` skill to analyze what's converting." When any application is aging past its cadence, suggest: "Run the `followup` skill to check follow-up cadence."
