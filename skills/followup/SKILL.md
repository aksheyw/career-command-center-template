---
name: followup
description: "Follow-up cadence tracker. Flags overdue and urgent applications, then drafts the second-touch email or LinkedIn message in your voice. Argument: none, or a company name to follow up on one."
---

You are managing follow-up cadence for the user's active applications. Most candidates leak opportunities by never sending the second touch — this skill catches the aging ones and drafts the follow-up.

Cadence model adapted from career-ops's `followup` mode (santifer/career-ops), rebuilt to read this plugin's tracker and to write in the user's own voice.

## STEP 1: Load the data

Read `${CLAUDE_PLUGIN_ROOT}/references/applications.md` (the structured tracker maintained by the `track-application` skill). If it does not exist, or contains only the shipped example rows, say: "No tracker yet — log applications with `track-application` first." Stop.

Today's date is the system date. Use it for all aging math.

## STEP 2: Apply cadence rules

For each row, compute **days since the relevant date** (last follow-up if present, else applied date) and assign urgency by status:

| Status | Cadence | Becomes... |
|--------|---------|-----------|
| `responded` | 3 days | **URGENT** — they replied; respond within 24h regardless |
| `interview` | 1 day | **URGENT** — keep momentum |
| `applied` / `screening` | 7 days | **OVERDUE** once past 7 days with no follow-up |
| any, 2+ follow-ups sent | — | **COLD** — suggest closing, do not draft a third |
| within cadence window | — | **waiting** (on track) |

Skip rows with status `offer`, `rejected`, `discarded`, `skip`, `evaluated`.

If a single company was passed as the argument, filter to it.

## STEP 3: Display the cadence dashboard

```
Follow-up Cadence — {date}   ({N} active, {M} actionable)

| # | Company | Role | Status | Days | Follow-ups | Urgency | Contact |
|---|---------|------|--------|------|-----------|---------|---------|
```

Sort URGENT → OVERDUE → waiting → COLD. If nothing is actionable, say so and stop.

## STEP 4: Draft follow-ups (URGENT and OVERDUE only)

For each, read the company's evaluation context (the matching evaluation output or `CUSTOMIZATION_MEMORY.md` notes) and the user's proof points from `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/story-bank-index.md` and `${CLAUDE_PLUGIN_ROOT}/references/YOUR_PROFILE.md`.

**Voice is non-negotiable:** draft every message in the user's voice — plain, direct, specific. Apply `${CLAUDE_PLUGIN_ROOT}/skills/humanizer/SKILL.md` to every draft before presenting it. Never use generic AI-recruiter phrasing.

### First follow-up (0 sent) — email, 3–4 sentences, under 150 words
1. Reference the specific role + when applied (company + title, not "your team").
2. One concrete, quantified proof point that maps to the role's top requirement (from the evaluation's CV-match block or a story-bank metric — verified metrics only).
3. Soft ask + a specific window ("this week", "next Tuesday").
4. (optional) One relevant recent project.

Include a subject line. **Banned:** "just checking in", "just following up", "touching base", "circling back", "I wanted to reach out". Lead with value, never with the ask. Never sound desperate.

### Second follow-up (1 sent) — shorter, 2–3 sentences, NEW angle
A fresh insight, article, or project update — do not repeat the first. Still name the role.

### No email contact found
Draft a LinkedIn version: 3 sentences, 300 char max (hook specific to company → proof point → soft ask), and suggest running `outreach` to find the right person first.

Present each draft as:

```
## Follow-up: {Company} — {Role} (#{n})
**To:** {contact or "no contact — run outreach first"}
**Subject:** {subject}
**Channel:** Email / LinkedIn   **Days since:** {N}   **Sent so far:** {N}

{draft}
```

## STEP 5: Record only what was actually sent

After the user confirms they sent one, update that row's **Last follow-up** date in `applications.md` (rewrite the row) and bump an implicit follow-up count in the Notes/Outcome column (e.g. "fu1 2026-06-30"). **Never** record a draft as sent. Only the user's confirmation counts.

## Boundaries

Reads the tracker + references; the only write is the **Last follow-up** date on confirmed sends. Drafts are proposals — the user reviews every one before it goes out.
