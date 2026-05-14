---
name: generic-letter
description: Generate the network forwarding cover letter for friends, alumni, or general network outreach.
---

You are generating a generic forwarding cover letter for sharing with the user's network.

## STEP 1: Read the template

Read `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/SKILL.md` and locate the "Generic Cover Letter (for network forwarding)" section. Read `${CLAUDE_PLUGIN_ROOT}/references/YOUR_PROFILE.md` for the user's current role, achievements, and contact info.

## STEP 2: Read the humanizer

Read `${CLAUDE_PLUGIN_ROOT}/skills/humanizer/SKILL.md` and apply the checklist to the generated letter.

## STEP 3: Generate the letter

Use the Generic Cover Letter template from `SKILL.md` exactly. The letter must include:

- Salutation: "Dear Friends and Network,"
- Brief context of current role and what the user is looking for
- Bullet list of target roles (helps forwarders know who to share with)
- Bullet list of key achievements (helps forwarders make the pitch)
- Request line: "Feel free to forward this note"
- Phone number from `YOUR_PROFILE.md`
- LinkedIn URL from `YOUR_PROFILE.md`
- Portfolio URL from `YOUR_PROFILE.md` (if any)

The tone must be warm, confident, and direct. Not passive. Not "I am exploring" — use "I am looking for" or "I am ready for."

Apply humanizer check before finalizing.

## STEP 4: Ask if customization is needed

After generating the standard version, ask: "Would you like a version customized for a specific person (e.g., an alumni connection or a recruiter in a specific sector)?"

If yes, apply the warm-referral template from `career-tools.md` (Template 4) and personalize for the context.

## STEP 5: Output

Print the final letter ready to copy-paste. No placeholders in the output — fill everything in from `YOUR_PROFILE.md` or ask the user for anything missing.
