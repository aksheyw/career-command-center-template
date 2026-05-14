---
name: evaluate
description: "Evaluate a JD before applying — 7-block assessment with go/no-go score. Argument: [paste JD text or URL here]"
---

You are evaluating a job description using the 7-block evaluation framework. The user has pasted a JD or provided a URL.

## STEP 1: Read required files

- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/evaluation-framework.md` — the 7-block rubric and scoring dimensions
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/SKILL.md` — company-type strategies, verified metrics
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/star-stories.md` — STAR stories for Block F mapping
- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/story-bank-index.md` — cross-indexed story selection
- `${CLAUDE_PLUGIN_ROOT}/references/YOUR_PROFILE.md` — the user's verified background

## STEP 2: If URL provided, fetch the JD

If the user provided a URL instead of JD text, use WebFetch to retrieve the job description content.

## STEP 3: Run all 7 evaluation blocks

Follow `evaluation-framework.md` exactly:

- **Block A**: Classify the role (archetype, seniority, domain, remote, team size, fit level)
- **Block B**: Cross-reference every JD requirement against the user's verified experience. Use ONLY metrics from `YOUR_PROFILE.md`. Flag gaps with mitigation strategies.
- **Block C**: Assess seniority match and positioning strategy
- **Block D**: Research compensation using WebSearch (Glassdoor, Levels.fyi, Blind, regional equivalents). Cite exact sources with URLs.
- **Block E**: List top 5 resume customizations + top 3 LinkedIn changes
- **Block F**: Map STAR stories to JD requirements using `story-bank-index.md`. Flag any story gaps.
- **Block G**: Assess posting legitimacy (freshness, company health, red flags)

## STEP 4: Score and verdict

Calculate scores for all 6 dimensions (1-5 scale each):

- CV Match, North Star Alignment, Compensation, Culture, Red Flags, Global Score
- Compute average
- Apply threshold: >= 3.5 = GO | 2.5-3.4 = CAUTION | < 2.5 = SKIP

## STEP 5: Output the evaluation report

Use the exact output format from `evaluation-framework.md`. Include:

- All scores with brief justifications
- Verdict with reason
- Key strengths and gaps with mitigations
- Recommended STAR stories for interview prep
- Legitimacy assessment
- Clear next-step recommendation

## STEP 6: If CAUTION or SKIP

Explain specifically what would need to change for this to become a GO. Be honest — don't soft-pedal gaps.

## RULES

- Never invent metrics — only use verified data from `YOUR_PROFILE.md`
- Never overclaim ownership — follow the accuracy guardrails in `SKILL.md`
- Compensation research must cite sources with URLs and dates
- If posting is older than 60 days, flag it prominently
- If the role is clearly below the user's target level, note the downlevel risk
