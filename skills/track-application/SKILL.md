---
name: track-application
description: "Log a new application or check pipeline status. Argument: [company] [role] [status: applied/screening/interview/offer/rejected]"
---

You are managing the user's job application pipeline.

## STEP 1: Read current memory

Read `${CLAUDE_PLUGIN_ROOT}/references/CUSTOMIZATION_MEMORY.md` to understand current patterns and what has been learned. This is the user's real (git-ignored) file. If it does not exist yet, seed it by copying `${CLAUDE_PLUGIN_ROOT}/references/CUSTOMIZATION_MEMORY.example.md` to that path, then proceed.

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

`${CLAUDE_PLUGIN_ROOT}/references/applications.md` is the user's REAL tracker. It is **git-ignored**
(so private job-search data never reaches a public repo). Read it; if it does not exist, create it —
seed it from `${CLAUDE_PLUGIN_ROOT}/references/applications.example.md` if that exists, and put the
privacy header at the top (see the example file). It has exactly one table with this schema — keep the
columns in this order:

```markdown
# Application Tracker

| Num | Company | Role | Type | Status | Applied | Responded | Interview | Source | Score | Outcome reason | Contact | Follow-ups | Last follow-up |
|-----|---------|------|------|--------|---------|-----------|-----------|--------|-------|----------------|---------|-----------|----------------|
| 1   | Northstar AI | Director of Product | AI | applied | 2026-06-30 | — | — | referral | 4.2 | — | jane.recruiter@northstar.example | 0 | — |
```

Field rules:
- **Num** — sequential, never reused.
- **Type** — AI / Consumer / Enterprise / Fintech / Telco / Other.
- **Status** — one of: `evaluated`, `applied`, `screening`, `responded`, `interview`, `offer`, `rejected`, `discarded`, `skip`. Use these exact tokens (the `patterns`/`followup` skills classify on them). `discarded` = went dead with no formal rejection; `skip` = self-filtered before applying.
- **Applied** — `YYYY-MM-DD` you submitted the application.
- **Responded** — `YYYY-MM-DD` the company/recruiter first responded with a real reply (not an auto-ack); `—` until it happens. Set this the moment a reply lands (even if you also move Status to `screening`/`responded`). `followup` keys its urgency off it, and `patterns` reads it as proof the row reached the screening stage.
- **Interview** — `YYYY-MM-DD` of the first interview (scheduled or held); `—` until it happens. `followup` keys momentum off it, and `patterns` reads it as proof the row reached the interview stage.
- **Source** — `referral` / `direct` / `recruiter`.
- **Score** — the evaluation score (X.X/5) if the role was evaluated; else `—`.
- **Outcome reason** — on `rejected`/`discarded`/`skip`, the stated or inferred reason (e.g. "geo-restricted", "stack mismatch", "seniority gap"). This is what `patterns` mines — never leave it blank on a negative outcome.
- **Follow-ups** — integer count of follow-ups actually SENT (not drafted); starts at `0`. `followup` bumps it on a confirmed send and treats `2+` as COLD.
- **Last follow-up** — `YYYY-MM-DD` of the most recent follow-up sent, else `—`.

On a new application: append a row (Responded, Interview `—`; Follow-ups `0`). On an update: rewrite the existing row in place (build the new row as a fresh line, don't mutate columns piecemeal) — and when a reply or interview happens, fill the **Responded** / **Interview** date, don't just change Status. Write the file back. If the file still contains the shipped fictional example rows, delete them when appending the first real row.

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

**Zero-denominator guard (mandatory — same rule as the `patterns` skill):** each conversion rate above is `numerator ÷ denominator`. If a denominator is 0 (e.g. no screens yet, so "screens to interviews" has nothing to divide), print "insufficient data for this rate" for that line — never divide by zero, and never print `0%` when what you mean is "no data yet". A `0%` reported on a zero denominator reads as a real failure signal when it is really just absence of data.

If there are fewer than 5 applications, note: "Pipeline is thin — consider expanding outreach or applying to more roles."

When the tracker has 5+ outcomes, suggest: "Run the `patterns` skill to analyze what's converting." When any application is aging past its cadence, suggest: "Run the `followup` skill to check follow-up cadence."
