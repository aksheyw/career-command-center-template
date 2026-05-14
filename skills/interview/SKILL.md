---
name: interview
description: "Full interview prep for a specific company. Argument: [company name] [optional: role title]"
---

You are preparing the user for a director-level PM interview. The user has provided a company name and optionally a role title.

## STEP 1: Read required files

Read all of these:

- `${CLAUDE_PLUGIN_ROOT}/references/YOUR_PROFILE.md` — the user's verified background
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/SKILL.md` — company-type strategies, interview angles
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/star-stories.md` — all the user's STAR stories
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/story-bank-index.md` — cross-indexed story selection by company type
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/interview-prep.md` — frameworks, questions, pitch
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/career-tools.md` — 90-day plans, salary strategy

## STEP 2: Identify company type

Based on the company name, determine:

- Company Type: AI / Consumer Scale / Enterprise / B2B / Fintech / Telco
- Interview focus: what they will care most about
- Fit level: how strong the match is

## STEP 3: Output complete prep pack

### 2-MINUTE PITCH (company-customized)

Adapt the standard pitch template from `interview-prep.md` to reference the specific company in the closing line. Pull the user's actual achievements from `YOUR_PROFILE.md`.

### TOP 4 STAR STORIES FOR THIS COMPANY

Use `story-bank-index.md` to select stories by company type. Cross-reference with `star-stories.md` for full story details.

For each story, provide:

- Story name
- Why it is relevant to this specific company
- The 60-second version (crisp retelling)
- Watch out for (common stumbles in telling this story)

Also include one failure story and why it works for this company.

### QUESTIONS THEY WILL LIKELY ASK

10 specific questions based on the JD / company type, with guidance on how to answer each:

- 3 behavioral (use STAR stories)
- 3 product / strategy (use company-type interview angle from `SKILL.md`)
- 2 leadership (team building, stakeholder management)
- 1 failure (use one of the user's failure stories)
- 1 "why this company" (prepare specific answer)

### COMPANY-TYPE INTERVIEW ANGLE

Pull the relevant interview angle from `SKILL.md` and expand it for this specific company.

### 90-DAY PLAN

Pull the relevant 90-day plan from `career-tools.md` and customize for this company. Make it specific — reference their actual products and challenges if known.

### QUESTIONS TO ASK INTERVIEWER

5 strong questions that signal director-level thinking. Pull from `interview-prep.md` and adapt for this company. Include at least one red-flag probing question.

### SALARY PREP

From `career-tools.md`:

- Target range for this company type
- Response to "what are you making now?"
- Response to "what are your salary expectations?"
- Key negotiation lever (from user's profile — e.g., illiquid equity)

### PRE-INTERVIEW CHECKLIST

- [ ] Review 2-minute pitch out loud
- [ ] Practice all 4 STAR stories timed (2 min each max)
- [ ] Research company news from last 30 days
- [ ] Prepare 3 questions to ask
- [ ] Review your resume (what they saw)
- [ ] Know salary range and be ready to hold it

## STEP 4: Update story bank

After generating prep, check if any stories were improvised or if gaps were exposed:

- If a new story was created → suggest adding it to `star-stories.md` with full STAR format
- If no story fit a requirement → add the gap to the GAP TRACKER in `story-bank-index.md`
- Update the company-type priority table if story selection order should change
