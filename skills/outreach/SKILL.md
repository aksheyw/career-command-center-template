---
name: outreach
description: "Generate the right outreach message for any contact or company. Argument: [person name / company / context — e.g., 'alumni at Google' or 'recruiter at Stripe']"
---

You are generating outreach messages for the user's job search. The user has described the target contact or company.

## STEP 1: Read the outreach templates

Read `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/career-tools.md` for the 6 outreach templates and personalization guidance. Read `${CLAUDE_PLUGIN_ROOT}/references/YOUR_PROFILE.md` for the user's name, title, phone, LinkedIn, portfolio, and key achievements.

## STEP 2: Identify the right template

Select based on the user's input:

| Situation | Template |
|-----------|----------|
| Cold LinkedIn connection request | Template 1 (300 char limit) |
| LinkedIn InMail to hiring manager | Template 2 |
| Cold email to recruiter | Template 3 |
| WhatsApp / direct message to warm contact for referral | Template 4 |
| Following up after no response | Template 5 |
| Thank you after interview | Template 6 |

If the context is ambiguous, ask which situation applies before generating.

## STEP 3: Check what was already sent

Before writing anything, read the `Contact` and `Last follow-up` columns for this company in
`${CLAUDE_PLUGIN_ROOT}/references/applications.md`, the tracker the `track-application` skill keeps.
A follow-up that repeats a message already sent costs the relationship. If the row shows a recent
touch, say so and confirm with the user before generating. If the tracker does not exist yet, or has
no row for this company, say that there is no record of earlier contact and continue. Never treat
the rows in `applications.example.md` as real history.

## STEP 4: Personalize the message

Mandatory personalizations:

- Replace `[NAME]` with the person's name if provided
- Replace `[COMPANY]` with the actual company name
- Replace `[SPECIFIC]` with something real about their work or company news if mentioned
- Replace `[ROLE]` with the actual role if known
- For Template 2 (InMail): include a specific company challenge or product reference
- For Template 4 (warm DM): use first name only, keep casual tone
- Pull the user's name, title, scope, achievements, phone, and LinkedIn from `YOUR_PROFILE.md`

Never use generic placeholders in the final output — fill them in or explicitly mark what the user needs to fill in manually before sending.

## STEP 5: Voice pass

Run the `humanizer` skill in this plugin on the drafted message before you output it. An outreach
draft that still reads as AI-written is not finished.

## STEP 6: Output the message

Output the ready-to-send message clearly formatted, followed by:

- Channel: [where to send this]
- Length: [character / word count]
- What to customize before sending: [any remaining gaps]
- Follow-up timing: [when to follow up if no response]

For warm outreach, include phone from `YOUR_PROFILE.md`. For email / InMail, include LinkedIn from `YOUR_PROFILE.md`.
