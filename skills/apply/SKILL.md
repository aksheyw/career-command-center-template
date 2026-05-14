---
name: apply
description: Paste a JD to get full analysis + tailored resume + cover letter. Argument: [paste JD text here]
---

You are generating job application materials. The user has pasted a job description. Follow this exact workflow.

## STEP 0: Quick evaluation (go/no-go check)

Read the evaluation framework first:

- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/evaluation-framework.md`
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/story-bank-index.md`

Run a rapid version of the 7-block evaluation. Score all 6 dimensions (1-5). If average score < 2.5, warn the user: "This JD scores [X.X/5] — below the GO threshold. Key concerns: [list]. Do you want to proceed anyway?" Wait for confirmation before continuing.

If score >= 2.5, show the score summary and continue to Step 1.

## STEP 1: Read the skill files

Read these before generating anything:

- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/SKILL.md` — resume templates, ATS rules, pre-generation checklist, cover letter spec
- `${CLAUDE_PLUGIN_ROOT}/skills/humanizer/SKILL.md` — AI writing pattern removal
- `${CLAUDE_PLUGIN_ROOT}/references/YOUR_PROFILE.md` — the user's verified background

Also read these if relevant to the role:

- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/detailed-context.md` — full work history, certifications, AI projects
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/career-tools.md` — cover letter hooks, company-specific strategies

## STEP 2: Analyze the JD

Output a JD analysis block:

```
JD ANALYSIS

Company: [name]
Role: [title]
Company Type: [AI / Consumer / Enterprise / Fintech / Telco / Other]

Top 3 Must-Haves:
1. [requirement]
2. [requirement]
3. [requirement]

ATS Keywords to Mirror:
[list 8-10 keywords directly from the JD]

Fit Score: [X/10]
Strengths: [what matches perfectly]
Gaps: [what to address or de-emphasize]

Strategy: [which company-type template to apply and why]
```

## STEP 3: Complete the pre-generation checklist

Work through ALL 8 steps of the pre-generation checklist from `SKILL.md` before generating any document. Do not skip.

## STEP 4: Generate the resume

Apply the correct company-type strategy from `SKILL.md`:

- AI Companies: Lead with shipped-AI achievements in Experience; AI / Side Projects section after Experience; portfolio link prominent in header
- Consumer Scale: Lead with headline scale metric, best growth multiplier
- Enterprise / B2B: Fortune 500 / partnership work folded into Experience bullets (no standalone section)
- Fintech: Lead with GMV / TPV, payment infra, bank partnerships
- Telco: Lead with telco partnerships, B2B2C distribution, explicit category match in cover letter

Rules that are never optional:

- Exactly 2 pages
- Bullets max ~55 words for senior roles, ~20 for early career
- No special characters (use ISO currency codes; "to" not arrow; standard hyphens only)
- LinkedIn and portfolio as clickable hyperlinks
- Strongest credential in summary
- Only use verified metrics from `YOUR_PROFILE.md`'s verified-metrics tables

Save the resume as a `.docx` file named: `{{LastName}}_{{FirstName}}_Resume_{{Company}}.docx`

## STEP 5: Generate the cover letter

250-300 words. Follow the cover letter specification in `SKILL.md` exactly:

- Hook: strong, specific, NOT passive ("I am exploring..." is forbidden)
- Strongest credential mentioned in opening paragraph
- Specific ownership language
- Research hook: reference something specific about the company (news, product, initiative)
- Proof points mapped to JD requirements
- Confident close WITH phone number ("Let's connect — {{phone}}")
- NO passive phrases: never use "I would welcome", "Please feel free", "I am open to"

Save as: `{{LastName}}_{{FirstName}}_CoverLetter_{{Company}}.docx`

## STEP 6: Apply humanizer

Re-read `${CLAUDE_PLUGIN_ROOT}/skills/humanizer/SKILL.md` and apply the checklist to ALL generated text in both documents before finalizing. Remove any AI-sounding patterns that slipped through. The humanizer pass is mandatory, not optional.

## STEP 7: Output summary

After generating both files, output:

```
GENERATION SUMMARY

Pre-Generation Checklist: COMPLETED
Company Type Strategy Applied: [type]
ATS Keywords Mirrored: [list]

Customizations Made:
- [what was reordered/emphasized]
- [which company-type template used]
- [any special sections added/removed]

Files Generated:
- {{LastName}}_{{FirstName}}_Resume_{{Company}}.docx
- {{LastName}}_{{FirstName}}_CoverLetter_{{Company}}.docx

EVALUATION SCORE: [X.X/5] — [GO/CAUTION/SKIP]

INTERVIEW PREP QUICK HITS:
Top 3 STAR stories for this company (from story-bank-index.md):
1. [story name + why relevant]
2. [story name + why relevant]
3. [story name + why relevant]

Questions they will likely ask:
- [question 1]
- [question 2]
- [question 3]
```
