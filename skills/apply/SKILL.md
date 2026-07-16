---
name: apply
description: "Paste a JD to get full analysis + tailored resume + cover letter. Argument: [paste JD text here]"
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

Work through ALL steps of the pre-generation checklist from `SKILL.md` (Step 0 through Step 9) before generating any document. Do not skip. **Step 0 — Locate Your Canonical Resume — is BLOCKING and must complete before Step 4.**

## STEP 4: Generate the resume from the user's canonical (NOT from templates)

**This is BLOCKING.** Per `SKILL.md` STEP 0 — once the user has a canonical generic resume on disk, the tailored resume MUST be built by copying that canonical and applying minimal targeted edits. NEVER rebuild from `detailed-context.md`, `star-stories.md`, or this skill's templates. (Only if no canonical exists yet — a fresh install — generate from the templates with an explicit warning, then save the approved result as the canonical, per `SKILL.md` STEP 0.)

**Procedure:**

1. Copy the canonical (default path `${CLAUDE_PLUGIN_ROOT}/references/generic-resume.docx`, or the user's override path per `SKILL.md` STEP 0) to the target `{{LastName}}_{{FirstName}}_Resume_{{Company}}.docx`.
2. Apply company-type-specific tilts as targeted edits ON the canonical copy:
   - **AI Companies:** verify the AI / side-projects section position; consider promoting a shipped-AI bullet to first in the current role; portfolio link prominent in header.
   - **Consumer Scale:** verify the headline scale metric + best growth multiplier are prominent.
   - **Enterprise / B2B:** verify Fortune 500 / partnership content sits inside role bullets (NOT a standalone section).
   - **Fintech:** consider promoting the GMV / TPV / payments bullet earlier in its role section.
   - **Telco:** consider promoting telco-partnership work to the lead bullet; explicit category match in the cover letter.
   - **Growth roles:** promote the activation / retention bullet to first in the current role.
3. Diff against the canonical (`unzip -p` both files' `word/document.xml` and `diff`) to SURFACE unexpected drops, then render the edited `.docx` to PDF and look at it to confirm 2 pages, section order, and clickable hyperlinks. The diff flags candidates; the render is what actually proves layout and links survived.

**Rules that are never optional (verified against the canonical, not regenerated):**

- Exactly 2 pages
- Bullets stay close to canonical lengths (40-55 words for senior bullets, 12-20 for early career)
- No special characters (use ISO currency codes; "to" not arrow; standard hyphens only)
- LinkedIn and portfolio as clickable hyperlinks
- Strongest credential in summary
- Current end dates and availability tags preserved exactly as the canonical has them (do NOT regress a real end date to "Present")
- Only use verified metrics that exist in the canonical and `YOUR_PROFILE.md`'s verified-metrics tables

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

## STEP 6.5: ATS screening questions (only if the application form has them)

Many ATS forms ask inline behavioral / screening questions ("Tell us about a time you led through ambiguity", "Why this company?", "Describe a product you scaled"). If the user pasted such questions, or the application clearly has them, map each to the story bank instead of improvising.

For each question:

1. Pick the best-fit STAR story from `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/story-bank-index.md` (already loaded in STEP 0) — match on the company TYPE row and the question's theme (scale, ambiguity, conflict, failure, data integrity, partnership).
2. Draft a tight answer in the user's voice (apply the humanizer checklist): situation in one line, action in their words, the quantified result. Keep to the form's word/char limit if one is given.
3. Never invent a metric — use only verified numbers from the story bank and `YOUR_PROFILE.md`.

Output each as:

```
Q: [the screening question]
Story: [story name (#n) from index]
Answer: [drafted response]
```

If the form has no behavioral questions, skip this step silently.

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
