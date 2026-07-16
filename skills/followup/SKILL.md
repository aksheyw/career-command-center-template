---
name: followup
description: "Follow-up cadence tracker. Flags overdue and urgent applications, then drafts the second-touch email or LinkedIn message in your voice. Argument: none, or a company name to follow up on one."
---

You are managing follow-up cadence for the user's active applications. Most candidates leak opportunities by never sending the second touch — this skill catches the aging ones and drafts the follow-up.

Cadence model adapted from the `followup` mode of [santifer/career-ops](https://github.com/santifer/career-ops) (MIT), rebuilt to read this plugin's tracker and to write in the user's own voice.

## STEP 1: Load the data

Read `${CLAUDE_PLUGIN_ROOT}/references/applications.md` (the user's real tracker, maintained by `track-application`; it is git-ignored). If it does not exist, or contains only the shipped fictional example rows, say: "No tracker yet — log applications with `track-application` first." Stop. (The committed `applications.example.md` is a schema reference only — never treat its rows as real.)

Today's date is the system date. Use it for all aging math. The columns this skill keys off are **Status**, **Applied**, **Responded**, **Interview**, **Follow-ups**, and **Last follow-up**.

## STEP 2: Apply cadence rules

Assign urgency per row using the status and the relevant date column. "Days since" always uses the **Last follow-up** date if present, otherwise the driving date named below. For the interview rows, "thank-you already logged" means a follow-up dated **on or after** the Interview date exists (Last follow-up ≥ Interview date) — that is the dated exit out of the thank-you window.

| Status | Driving date | Rule | Becomes... |
|--------|--------------|------|-----------|
| `responded` | Responded | reply within 24h of their response | **URGENT** — actionable until you log a follow-up dated on/after the Responded date |
| `interview`, **Interview date in the FUTURE** | Interview | the interview hasn't happened — nothing to send yet | **upcoming** — not actionable |
| `interview`, Interview date today/past, **no thank-you logged yet** (Last follow-up empty or before the Interview date) | Interview | send a thank-you within 24h of the interview | **URGENT** (thank-you) — exits the moment you log a follow-up dated on/after the Interview date |
| `interview`, **thank-you already logged**, ~5-7 business days since the last touch, no reply | Last follow-up | send one status-check | **OVERDUE** (status-check) |
| `applied` / `screening` | Last follow-up, else Applied | past 7 days with no follow-up | **OVERDUE** |
| any status, **Follow-ups ≥ 2** | — | don't draft a third | **COLD** — suggest closing |
| within a window above, or an upcoming interview waiting to happen | — | on track | **waiting** / **upcoming** |

Precedence when more than one rule could apply: **COLD** (Follow-ups ≥ 2) overrides everything — never draft a third touch. A **future-dated interview is `upcoming`, never urgent** — there is nothing to follow up on until it happens. Otherwise `responded` and a just-held interview still inside its 24h thank-you window → URGENT; an interview past its thank-you window (thank-you logged, 5-7 business days quiet) or an `applied`/`screening` row past 7 days → OVERDUE. Every interview state has a dated exit: future → upcoming; held → 24h thank-you (URGENT) → exits on the logged thank-you → 5-7 day status-check (OVERDUE) → COLD at 2 touches.

Skip rows with status `offer`, `rejected`, `discarded`, `skip`, `evaluated`.

If a single company was passed as the argument, filter to it.

## STEP 3: Display the cadence dashboard

```
Follow-up Cadence — {date}   ({N} active, {M} actionable)

| # | Company | Role | Status | Days | Follow-ups | Urgency | Contact |
|---|---------|------|--------|------|-----------|---------|---------|
```

Sort URGENT → OVERDUE → waiting → upcoming → COLD. Only URGENT and OVERDUE are actionable (STEP 4 drafts those); upcoming (future interview), waiting, and COLD are shown but not drafted. If nothing is actionable, say so and stop.

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

After the user confirms they sent one, rewrite that row in `applications.md`: set **Last follow-up** to today's date and increment the **Follow-ups** count by 1 (0 → 1, 1 → 2). Once **Follow-ups** reaches 2, the row is COLD on the next run and this skill will stop drafting. **Never** record a draft as sent. Only the user's confirmation counts.

## Boundaries

Reads the tracker + references; on a confirmed send it writes exactly two fields on that row — the **Last follow-up** date (today) and the incremented **Follow-ups** count (per STEP 5). Nothing else is written. Drafts are proposals — the user reviews every one before it goes out, and a draft is never recorded as sent.
