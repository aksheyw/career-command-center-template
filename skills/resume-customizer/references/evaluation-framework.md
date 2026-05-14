# JD Evaluation Framework

**Purpose:** Systematic 7-block evaluation of job descriptions before applying.
**When to use:** Before generating any resume or cover letter. Run via the `evaluate` skill or automatically as Step 0 of `apply`.

---

## SCORING DIMENSIONS (1-5 scale each)

| Dimension | 1 (Poor) | 3 (Acceptable) | 5 (Strong) |
|---|---|---|---|
| **CV Match** | <30% requirement overlap | 50-70% overlap | >85% overlap with proof points |
| **North Star Alignment** | No career progression value | Lateral move, decent brand | Clear step toward target role |
| **Compensation** | Below current, no equity | Market rate, standard equity | Above current + meaningful equity / upside |
| **Culture & Team** | Red flags present | Neutral / unknown | Strong signals of good culture + right team size |
| **Red Flags** | Multiple concerns | Minor concerns | Clean — legitimate posting, healthy company |
| **Global Score** | Would not recommend applying | Worth considering with caveats | Strong match, prioritize |

**Go / No-Go Threshold:**

- Average score >= 3.5 = **GO** (proceed to resume generation)
- Average score 2.5-3.4 = **CAUTION** (flag concerns, ask user if they want to proceed)
- Average score < 2.5 = **SKIP** (recommend not applying, explain why)

---

## 7-BLOCK EVALUATION PROCESS

### Block A: Role Classification

Detect role archetype and map to the user's strengths (pulled from `YOUR_PROFILE.md`).

| Archetype | Lead With |
|---|---|
| **AI / ML Product** | Shipped-AI achievements, side AI projects, AI certifications |
| **Consumer Scale** | Headline scale metric, best growth multiplier, multi-market scope |
| **Enterprise / B2B** | Fortune 500 / enterprise partnerships, regulatory expertise, B2B2C model |
| **Fintech** | GMV / TPV, payment infra, bank partnerships |
| **Telco** | Telco partnerships, OEM + Telco integration, B2B2C distribution |
| **Transformation / Strategy** | 0-to-1 launches, strategic influence stories, MBA / equivalent credential |

Output:

```
ROLE CLASSIFICATION
Archetype: [type]
Seniority: [IC / Manager / Director / VP]
Domain: [specific industry / function]
Remote: [Yes / No / Hybrid]
Team Size: [estimated]
User Fit Level: [Strong / Moderate / Weak]
```

### Block B: CV-to-JD Alignment

Cross-reference each JD requirement against `YOUR_PROFILE.md`'s verified experience.

For EACH requirement:

- **Match:** cite specific proof point from profile (max 125 chars)
- **Partial:** identify the closest experience + how to bridge
- **Gap:** flag explicitly + suggest mitigation strategy

Rules:

- Only use verified metrics from `YOUR_PROFILE.md` metrics tables
- Match the user's accuracy guardrails (`YOUR_PROFILE.md` "Never say" / "Always say" lists)

Output a match percentage and gap analysis table.

### Block C: Seniority Strategy

Compare JD seniority level vs. the user's natural fit (Director-level PM by default — adjust if the user's profile targets a different level).

- If role is **below** target: assess if worth it for brand / opportunity. Frame as "looking for high-impact IC role" if the user is open to that.
- If role is **at level**: standard positioning.
- If role is **above**: frame trajectory + strongest credential + breadth of scale responsibility.

Output positioning recommendation.

### Block D: Compensation Research

Research compensation data using WebSearch:

- Target sources: Glassdoor, Levels.fyi, Blind, TeamBlind, region-specific equivalents
- Document EXACT source URLs and dates
- Compare against the user's current compensation baseline (from `YOUR_PROFILE.md`)
- Factor in: base, equity (RSU / ESOP), bonus, location adjustment

Output compensation bracket with sources cited.

### Block E: Personalization Roadmap

Top 5 resume customizations for this specific role:

1. [specific change + example text]
2. [specific change + example text]
3. [specific change + example text]
4. [specific change + example text]
5. [specific change + example text]

Top 3 LinkedIn optimization items:

1. [change]
2. [change]
3. [change]

### Block F: Story Mapping

Map STAR stories from `star-stories.md` to this JD's requirements:

| JD Requirement | Best Story | Why | Backup Story |
|---|---|---|---|
| [requirement 1] | [story name] | [fit reason] | [alternative] |
| [requirement 2] | [story name] | [fit reason] | [alternative] |
| ... | ... | ... | ... |

Flag any JD requirements where no existing story is a strong fit — these are **story gaps** to add to `story-bank-index.md`'s GAP TRACKER.

### Block G: Legitimacy Assessment

Evaluate posting legitimacy:

**High Confidence (proceed):**

- Posted within 30 days
- Company has active hiring signals (LinkedIn headcount growing, recent funding)
- Clear JD with specific requirements (not generic)
- Named hiring manager or team

**Proceed with Caution:**

- Reposted multiple times (phantom role risk)
- Vague JD ("wear many hats", "fast-paced environment")
- Company in recent layoff news
- No salary range in markets that require it

**Suspicious (flag to user):**

- Posting older than 60 days
- Requirements don't match title (Director title, IC requirements)
- Company has negative Glassdoor reviews for PM org
- "Urgently hiring" but posting keeps resurfacing

---

## OUTPUT FORMAT

```
JD EVALUATION REPORT

Company: [name]
Role: [title]
Archetype: [type]
Date Evaluated: [date]

SCORES:
  CV Match:           [X/5]
  North Star:         [X/5]
  Compensation:       [X/5]
  Culture:            [X/5]
  Red Flags:          [X/5]
  Global:             [X/5]
  AVERAGE:            [X.X/5]

VERDICT: [GO / CAUTION / SKIP]
REASON: [1-2 sentence explanation]

KEY STRENGTHS:
- [strength 1]
- [strength 2]

KEY GAPS:
- [gap 1 + mitigation]
- [gap 2 + mitigation]

RECOMMENDED STORIES: [story names for interview prep]
LEGITIMACY: [High Confidence / Caution / Suspicious]

NEXT STEP: [Proceed to `apply` | Investigate further | Skip]
```
