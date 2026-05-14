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

## STEP 4: Output pipeline summary

Always end with a pipeline summary table:

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
