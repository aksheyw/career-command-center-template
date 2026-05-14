---
name: update-memory
description: Log what worked (or didn't) to improve future applications. Argument: [company] [outcome] [what worked / what to change]
---

You are updating the customization memory — the learning log that makes every future application smarter.

## STEP 1: Read the current memory file

Read `${CLAUDE_PLUGIN_ROOT}/references/CUSTOMIZATION_MEMORY.md` fully. Understand the existing patterns before adding anything.

## STEP 2: Gather information

Ask the user (or extract from their input):

- Which company and role?
- What was the outcome? (Resume screen passed / rejected / screened / interviewed / offered)
- What resume strategy was used? (Which company-type template?)
- What was the cover letter hook?
- Was there a referral involved?
- For rejections: any feedback or signal about why?
- For successes: what specific framing or metric seemed to resonate?

## STEP 3: Identify the learning

Based on the outcome, generate a specific, actionable learning:

- NOT "good resume" — say WHAT specifically seemed to work
- NOT "bad fit" — say which framing missed the mark
- Connect to company-type patterns already in the file

## STEP 4: Update the file

Write the updated `CUSTOMIZATION_MEMORY.md` to `${CLAUDE_PLUGIN_ROOT}/references/CUSTOMIZATION_MEMORY.md`.

Add the new entry under the correct company-type section. Update:

- "Successful Customizations" if outcome was positive
- "Unsuccessful Patterns" if outcome was negative or no response
- "Screen Rate" with the updated percentage if calculable

## STEP 5: Surface patterns

After updating, analyze across all logged applications:

- Which company types are yielding screens?
- Which cover letter hooks got the most traction?
- Which resume strategies need improvement?
- Are there any keywords or framings that appear in multiple successful applications?

Output a brief "What We Know So Far" summary with 3-5 actionable insights.
