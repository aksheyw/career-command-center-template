---
name: resume-customizer
description: Director-level / senior PM resume + cover letter toolkit. Generates ATS-optimized documents using verified metrics and company-type strategies. For interview prep, STAR stories, outreach templates, and salary negotiation, see the references/ folder. Personalize `references/YOUR_PROFILE.md` first.
---

# Resume Customizer — Senior PM Toolkit

## QUICK REFERENCE

**Core function:** Generate ATS-optimized resumes and cover letters for director-level PM roles.

**Reference files (use when needed):**
- `references/star-stories.md` — your STAR stories (success + failure)
- `references/interview-prep.md` — RCA, guesstimate, case study, questions to ask
- `references/career-tools.md` — outreach templates, salary scripts, LinkedIn optimization, 90-day plans
- `references/detailed-context.md` — full work history, certifications, side projects, strengths
- `references/evaluation-framework.md` — 7-block JD scoring before generation
- `references/story-bank-index.md` — cross-indexed STAR story selection
- `references/github_in_resume_pattern.md` — GitHub introduction pattern
- `references/referral_email_pattern.md` — forwardable referral email pattern

**Profile source:** `${CLAUDE_PLUGIN_ROOT}/references/YOUR_PROFILE.md` is the single source of truth for the user's background.

---

## MISTAKES TO AVOID

### Section structure — permanent removals

- **No Strategic Focus section.** It duplicates Summary positioning and bores the reader. Pillars, themes, focus areas — all redundant when the Summary already anchors the narrative.
- **No Key Achievements section.** It duplicates Experience bullets.
- **No standalone "OEM & Telco Partnerships" section.** Fold partnership content into the role bullets where it was earned.
- **No standalone "Earlier Career" section.** Fold early roles directly into Professional Experience with one compact bullet each.

### STAR framework — implicit, never labeled

- **NEVER write `(S)`, `(T)`, `(A)`, `(R)` prefixes on resume bullets.** That reads kiddish and undermines senior positioning. STAR is an internal checklist for writing bullets, not scaffolding to display.
- **Weave Situation, Task, Action, Result into natural narrative prose.** A good bullet opens with context, flows through action, and lands on measurable results — the reader gets STAR structure without seeing the framework.
- **Bullet format:** bold theme prefix + flowing narrative. 40-55 words typical for senior roles with depth; 12-20 words for early career single-line bullets.

**Bad (kiddish, never do this):**
> **Market entry (STAR):** (S) Company needed entry... (T) Build distribution... (A) Ran user research... (R) 60X growth...

**Good (natural, senior-level):**
> **Market entry from scratch:** Entered a new region when monetization was {Nx} the baseline market but no playbook existed. Ran user research, built a {strategy descriptor} strategy, navigated relevant compliance, and led product integration for distribution partners post-contract. Scaled {start size} to {end size} ({growth multiplier}) in {timeframe}; key metric improved {X to Y}; retention improved by {Z}.

### Content and claims

- Do NOT invent metrics not in `YOUR_PROFILE.md`'s verified tables.
- Do NOT claim experiences the user doesn't have.
- Do NOT exaggerate scope or impact.
- Do NOT use any metric the user has explicitly marked as "REMOVED" in `YOUR_PROFILE.md`.
- Match the user's accuracy guardrails from `YOUR_PROFILE.md`'s "Never say" / "Always say" lists.
- If the user joined an existing platform, do NOT claim "scaling from 0 to N" — clarify their actual contribution.
- If the user is one of several peers (e.g., one GPM of many on a roadmap), use collaborative framing ("Collaborated with the broader product team to...") rather than ownership claims ("I own...").

### Always verify

- Every metric must come from the verified tables in `YOUR_PROFILE.md`.
- Every achievement must trace to actual experience.
- If uncertain, use conservative framing or omit.
- Be specific about what the user actually owns (team, markets, product areas).

---

## LANGUAGE RULES

### Avoid vague language

**Never use:**
- "Lead the platform" — lead WHAT specifically?
- "Responsible for" — what did you ACHIEVE?
- "Worked on" — what was YOUR contribution?
- "Helped with" — junior language

**Use instead:**
- "Own [specific area] including [scope]"
- "Drive [metric] through [action]"
- "Built [thing] that achieved [result]"
- "Manage [team size] across [geographies]"

### Avoid passive/weak language (cover letters)

**Never use:**
- "I am exploring opportunities"
- "I would welcome the chance"
- "I'd welcome a conversation about..." (FORBIDDEN — passive)
- "Please feel free to reach out"
- "I am open to"
- "I believe I would be a good fit"
- "X years of experience" — years don't matter, impact does

**Use instead:**
- "I own..." / "I drive..." / "I built..."
- "Let's connect — {{phone}}." (confident close with contact)
- "Happy to connect: {{phone}}" (action-oriented)
- "My direct wins include..." (ownership language)

### Avoid AI-sounding language

**Never use:** pivotal moment, key turning point, evolving landscape, serves as a testament, underscores the importance, comprehensive, robust, streamlined, fostering, cultivating, showcasing, at its core, in order to, "Additionally" at sentence start, em dashes for emphasis.

**Write like a human:** simple constructions (is/are/has), natural sentence length variation, specific over inflated, have opinions where appropriate, acknowledge uncertainty when relevant.

### MANDATORY: Use Humanizer Skill

Before outputting ANY resume or cover letter, Claude MUST:

1. Generate the document using this skill's templates.
2. Read `${CLAUDE_PLUGIN_ROOT}/skills/humanizer/SKILL.md`.
3. Apply humanizer checklist to all generated text.
4. Remove any AI-sounding patterns that slipped through.

---

## ATS COMPLIANCE (MANDATORY)

### Character replacements

| Replace | With | Example |
|---------|------|---------|
| Currency symbols (₹, €) | ISO code ("INR", "EUR", "USD") | "USD 5M ARR" or "EUR 12M GMV" |
| → (arrow) | "to" | "$10 to $15" |
| 0→1 | "0-to-1" | Hyphenated |
| — (em-dash) | "-" | Standard hyphen only |

### Output format — Golden Standard

- **File Type:** .docx (primary), PDF if requested
- **Font:** Calibri (not Arial)
- **Filename:** `{{LastName}}_{{FirstName}}_Resume_{{Company}}.docx`
- **Hyperlinks:** LinkedIn and portfolio must be clickable

**Exact styling (match these values for golden-standard output):**

- Name: size 28 (14pt), bold, color `#2E5090`
- Contact line: size 18 (9pt), color `#555555`
- Section headings: size 22 (11pt), bold, color `#2E5090`, bottom border (single, sz=4, color `#2E5090`, space=1)
- Body text: size 20 (10pt), color `#1A1A1A`
- Sub-descriptions: size 20, italic, color `#555555`
- Role headers: size 20, title bold `#1A1A1A`, company normal, dates right-aligned via tab stop pos=9026

**Page layout:** US Letter (12240 x 15840 DXA); margins top=620, right=720, bottom=620, left=720; line spacing 276 (1.15), lineRule=auto.

**Bullet style:** Word ListParagraph style with numPr numbering (or dash `- ` equivalent). Bullet character: dash. Indent: left=720, hanging=360. Spacing: before=20, after=20.

### What to avoid

- Tables, columns, text boxes
- Graphics, images, icons
- Headers/footers with content
- Special characters (use ASCII equivalents)
- Multiple font styles

### Date format

Use: "January 2023 - Present". Not: "Jan 2023", not "01/2023".

### 2-page limit (HARD)

If exceeding 2 pages, cut in this order:

1. Trim current-role bullets to 5 max (from 6).
2. Drop second-tier achievement bullets.
3. Condense previous-role bullets.
4. Shorten side-project descriptions.
5. Trim Expertise line length.

---

## PER-CLAIM DEFENSIBILITY AUDIT (MANDATORY before "final")

### The rule

**Before declaring any resume / email / cover letter "final" or "95% confident," build a per-claim audit table.** Each claim → source → confidence percentage. Surface anything below 90% to user before they ship.

### Audit table format

| Claim | Source | Confidence | Risk |
|---|---|---|---|
| [each verbatim claim from draft] | [profile metric, STAR story #, public source, or USER INPUT] | [%] | [LOW / MEDIUM / HIGH] |

### Three categories of miss to specifically watch for

**1. Math errors**

- Always verify percent calculations against the underlying numbers. AND specify the metric type when a percent could be ambiguous. Example: "$10 to $15 (+25% YoY)" — clear that the percent is annualized growth, not the math result of the lifetime $5 increase. Without "YoY," readers will calculate $10→$15 lifetime as +50% and the parenthetical reads as a math error.
- Always verify multiplier claims. Arithmetic: "{start} to N×{start}" is N times, not whatever sounds bigger. Example: "20% to 80%" is 4X (not 60% better — that's a different operation). When numbers are inherited from prior resumes, RE-VERIFY against `YOUR_PROFILE.md`. Do not trust.
- When numbers are inherited from prior resumes, RE-VERIFY. Do not trust.

**2. Scope overclaims — verbs that overstate role**

| Wrong (overclaim) | Right (honest) | Why |
|---|---|---|
| "Closed [partner] distribution" | "Led product integration for [partner] post-contract" | BD closes contracts; product integrates after MoU |
| "Architected the SDK" | "Framed the architecture problem and drove the design with engineering" | Product gives problem statement; engineering designs |
| "I own X feature/roadmap" | "Collaborated with the broader product team to ship..." | Match `YOUR_PROFILE.md`'s explicit ownership boundaries |
| "Scaled X from 0 to N" | "Led GTM and 0-to-1 launches for [specific market/segment]" | If user joined an existing platform |
| "The same pattern as [X]" | "A similar [structural element] to [X]" / "The kind of [X] that..." | Identity claim → analogy claim. Defensible if probed. |

**3. Inherited awkward phrasings — phrases lifted from rules/templates that read odd in context**

- "Our [team type] team" / "broader [team type] team" → use specific org name from profile
- "Tight latency budget" without numbers → drop or anchor with a real number
- Buzzword taglines as keywords ("Distributed Team Leadership") → reads as filler unless backed by specifics
- Bare labels like "AI/ML" → fine for cert blocks; reads thin in email body. Use "AI building" or specific subfield.

### Process

1. Draft the content
2. Run humanizer skill pass (em dashes, copula avoidance, AI tics)
3. **Build the per-claim audit table**
4. For each claim below 90% confidence: propose softening or dropping, surface to user
5. Only after the user resolves the flagged items, declare "ready"
6. Do NOT say "95% confidence" without having built the table

### Referrer-feedback corollary

If a referrer is reviewing the artifacts before forwarding, expect 4-7 iterations. Each round is more data about what the recruiter will read. **Don't lock after v1.** See `referral_email_pattern.md` for the full iteration pattern.

---

## PRE-GENERATION CHECKLIST

Before generating ANY resume or cover letter:

### Step 1: JD Analysis

- [ ] Company name and role title
- [ ] Company type: AI / Consumer / Enterprise / Fintech / Telco / Other
- [ ] Top 3 must-haves
- [ ] Top 3 nice-to-haves
- [ ] 8-10 keywords to mirror
- [ ] Honest fit score (1-10)

### Step 2: Resume Structure — LOCKED ORDER

1. **Summary** (3-4 line narrative anchor; lead with strongest credential)
2. **Expertise** (ATS keyword row — placed HERE for maximum ATS scoring, before Experience)
3. **Professional Experience** (ALL roles including early career folded in)
4. **AI Product Building / Side Projects** (ALWAYS after Experience, even for AI companies — credibility first)
5. **Education / Certifications / Recognition**

**Critical rules:**

- NO Strategic Focus. NO Key Achievements. NO standalone partnership section. NO standalone Earlier Career section.
- Section heading: "PROFESSIONAL EXPERIENCE" (not "Career Experience", not "Experience").
- Early career roles fold INTO Professional Experience with roleHeader + one compact bullet (12-20 words each). No depth, no STAR treatment.
- Side projects / AI building always after Professional Experience (credibility first, even for AI companies).

**Header:**

- [ ] Name from `YOUR_PROFILE.md` contact section
- [ ] Location (City, Country)
- [ ] Email (clickable)
- [ ] Phone
- [ ] LinkedIn (clickable)
- [ ] Portfolio (clickable, if any)
- [ ] GitHub (only when relevant to the role family — see `github_in_resume_pattern.md`)

**Summary (3-4 lines) — Narrative Anchor:**

- [ ] Open with strongest credential (degree, certification, or current title — choose what hooks fastest)
- [ ] Describe HOW the user works (methodology, not just what)
- [ ] Minimal metrics — scope references are fine; specific numbers go in Experience
- [ ] Sounds like a human, not a list of facts

**Expertise Section (after Summary, before Professional Experience):**

- [ ] Single line or two lines, pipe-separated
- [ ] Mirror exact JD keywords where user has real experience
- [ ] Include: skills, methodologies, tools, domain terms from JD

**Professional Experience bullets — mandatory elements:**

- [ ] Product description (italic subheading) under each company name
- [ ] Bold theme prefix + natural narrative body
- [ ] PM craft signals (discovery, roadmap, stakeholder management)
- [ ] Decision context (WHY you did it, not just WHAT)
- [ ] Measurable result with verified metric from `YOUR_PROFILE.md`
- [ ] STAR elements WOVEN — never labeled
- [ ] Each bullet 40-55 words for senior roles; 12-20 words for early career

**Side Projects / AI Product Building (if relevant):**

- [ ] Portfolio link first (if any)
- [ ] List specific projects with one-line proof points
- [ ] Tech stack categorized

**Education:**

- [ ] Pull from `YOUR_PROFILE.md` education section
- [ ] Honors / awards if any

**Recognition (if included):**

- [ ] Aggregate awards with prestige framing (consecutive-year patterns, top-X language)
- [ ] Do NOT list cute internal award names that read odd externally
- [ ] One or two named awards max if multi-year, with the prestige descriptor

### Step 3: Cover Letter

- [ ] Company name used (not "your organization")
- [ ] Explicit product category match if relevant
- [ ] Strongest credential in opening paragraph
- [ ] Specific ownership language
- [ ] Research hook (company news/initiative/product)
- [ ] NO passive phrases (see Language Rules)
- [ ] Strong confident close WITH phone number ("Let's connect — {{phone}}.")
- [ ] 250-300 words max

### Step 4: Metrics Verification

Pull from `YOUR_PROFILE.md`'s verified metrics tables. **If a metric is NOT in those tables, DO NOT USE IT.**

### Step 5: ATS Compliance

- [ ] No special characters
- [ ] LinkedIn and Portfolio are clickable hyperlinks
- [ ] Font: Calibri
- [ ] Dates: "January 2023 - Present" format
- [ ] Filename: `{{LastName}}_{{FirstName}}_Resume_{{Company}}.docx`
- [ ] Section heading: "PROFESSIONAL EXPERIENCE"

### Step 6: Page Check

- [ ] Exactly 2 pages (not 1, not 3)

### Step 7: Company-Type Checks

**For AI Companies:**
- [ ] AI / side-project section after Experience (not before)
- [ ] Portfolio link prominent
- [ ] Shipped-AI achievements in Experience bullets
- [ ] AI certifications included

**For Consumer Scale:**
- [ ] Headline scale metric prominent in sub-description
- [ ] Best-growth bullet as lead
- [ ] Multi-market scope emphasized (if applicable)

**For Enterprise / B2B:**
- [ ] Partnership / Fortune 500 work folded into bullets (NOT standalone section)
- [ ] Regulatory expertise mentioned (if applicable)
- [ ] B2B2C model explained where relevant

**For Fintech:**
- [ ] Payment / GMV work prominent
- [ ] Bank / processor partnerships mentioned
- [ ] Compliance language (PCI, RBI, etc.) if applicable

**For Telcos:**
- [ ] Telco partnerships visible
- [ ] B2B2C distribution model explained
- [ ] Explicit product category match in cover letter

### Step 8: Humanizer Check (MANDATORY)

- [ ] Read `${CLAUDE_PLUGIN_ROOT}/skills/humanizer/SKILL.md`
- [ ] Apply humanizer checklist to ALL generated text
- [ ] Sentence lengths vary naturally
- [ ] Specific over inflated language

### Step 9: Skills Form Mapping (for application forms)

When filling an application form's skills field:

- [ ] Extract exact keywords from JD first
- [ ] Verify EACH keyword against the user's actual experience
- [ ] Include only skills with real, demonstrable experience
- [ ] Flag marginal skills and ask before including
- [ ] Never add skills that appear in JD but NOT in profile
- [ ] Format: comma-separated list

---

## RESUME OUTPUT SPECIFICATION

### Header Format

```
{{FULL NAME}}
{{City}}, {{Country}} | {{email}} | {{phone}}
LinkedIn: {{linkedin URL}} | Portfolio: {{portfolio URL}}
```

Both LinkedIn and Portfolio must be clickable hyperlinks.

### Summary Template (3-4 lines — Narrative Anchor)

**Purpose:** Establish WHO the user is and HOW they work. Lead with strongest credential. Minimal metrics.

**Structure:** Credential + current title + approach/methodology + scope hint.

**Default (Platform Leader anchor):**

```
{{Positioning tagline — 3-5 words pipe-separated}}

{{Credential}} and {{Current Title}} at {{Company}}. {{2-3 sentences describing
HOW you work — methodology, not what you do. Use first person. Read it aloud:
does it sound like a human or a press release?}}
{{One scope-hint sentence — team size, market count, headline metric.}}
```

The reference files have company-type-specific summary variants. Adapt the language to match the JD's tone (more technical for AI, more business for fintech).

### Expertise Section (immediately after Summary)

**Purpose:** ATS keyword row. Recruiters and ATS systems scan skills first.
**Format:** Single line or two lines max, pipe-separated.

```
EXPERTISE
{{Keyword 1}} | {{Keyword 2}} | {{Keyword 3}} | {{Keyword 4}} | {{Keyword 5}} |
{{Keyword 6}} | {{Keyword 7}} | {{Keyword 8}} | {{Keyword 9}}
```

**Customize per JD:** Swap in exact keywords from the job description where the user has real experience. Mirror the JD's exact phrasing where possible.

### Professional Experience — Bullet Structure

**Format:** Natural narrative prose with bold theme prefix. STAR woven implicitly — never labeled.

**Section heading:** "PROFESSIONAL EXPERIENCE"

**Bullet length guidance:**

- Senior roles: 40-55 words; STAR depth implicit
- Early career: single compact line, 12-20 words

**Example structure (replace bracketed content with user's actual experience):**

```
{{Current Title}} | {{Current Company}} | {{Start month/year}} - Present
{{One-line italic product description — what the product is, key scale metric}}

- {{Theme prefix in bold}}: {{Context that explains why this work mattered.
  Action you took with method (not just outcome). Result with verified metric
  from profile.}} 40-55 words.

- {{Theme prefix}}: {{Same structure — context, action with method, result.}}

[3-5 bullets per senior role]
```

### Early Career — Single Compact Bullet

**Format:** roleHeader (title, company, month+year range) + one single-line bullet (12-20 words). NO depth, NO STAR treatment.

```
{{Title}} | {{Company}} | {{Date range}}
- {{One-line achievement with verified metric.}}
```

### Side Projects / AI Product Building Section

**Always after Professional Experience.**

```
AI PRODUCT BUILDING (or SIDE PROJECTS — pick what matches user's portfolio)
{{One-line framing about why these projects exist — keep technical edge, ship daily, etc.}}

- {{Project name}}: {{Problem solved + tech stack hint + concrete result}}
- {{Project name}}: {{Same structure}}
- {{Project name}}: {{Same structure}}

Tech: {{Stack categorized — LLMs | automation | data | integrations}}
```

### Education

```
EDUCATION
{{Institution}} | {{Degree}} | {{Years}} | {{Honors if any}}
{{Institution}} | {{Degree}} | {{Years}} | {{Location}}
```

### Certifications (5 max, categorized)

```
CERTIFICATIONS
{{Category 1}}: {{Cert 1}} | {{Cert 2}} | {{Cert 3}}
{{Category 2}}: {{Cert 4}} | {{Cert 5}}
```

### Recognition (aggregate with prestige framing)

**Always lead with the pattern (consecutive years, top-X) and name the prestigious-sounding award specifically. Do NOT list cute internal award names that read odd externally.**

```
RECOGNITION
{{Pattern statement — e.g., "Company top performer recognition X consecutive years
({{years}}), including the {{prestigious award name}} {{N}} times ({{years}}) —
the company's highest individual contribution award."}}
{{Other recognition — alumni boards, external awards}}
```

---

## COVER LETTER SPECIFICATION

### Format

- **Length:** 250-300 words
- **Tone:** Confident, specific
- **Structure:** Narrative arc (not checklist)

### Narrative Arc (preferred — scores 9/10 vs 7/10 for checklist)

- **Para 1 — WHY this move:** Honest motivation for why this company makes sense. Open with a specific product/market observation; include strongest credential naturally.
- **Para 2 — What you bring:** Connected story with method. Research first, strategy, iterate on data. Weave credential naturally (if not in para 1).
- **Para 3 — Specific JD mapping:** 2 proof points told with depth, not 3 points told thin. Show the journey (diagnosed X, did Y, result Z).
- **Para 4 — Direct close:** Phone number required. No passive language.

### Strong openers

- "I build products in markets where there are zero users and zero playbook."
- "I don't just strategize about AI — I ship it."
- "I build the same type of product you're building."
- "When [COMPANY NEWS], I recognized a challenge I've solved before."

### Strong closes (MUST include phone)

- "Let's connect — {{phone}}."
- "Call me on {{channel}}: {{phone}}."
- "Happy to discuss in detail: {{phone}}."

### FORBIDDEN closes

- "I'd welcome a conversation about..." (passive — FORBIDDEN)
- "I am exploring opportunities..."
- "Please feel free to reach out..."
- "Happy to discuss..." (without phone number)
- "Looking forward to discussing how I can contribute..." (generic)

### Template

```
[Date]

Dear {{Hiring Manager / Hiring Team}},

{{PARA 1 — WHY this move, 3-4 sentences. Specific product/market observation.
Include strongest credential.}}

{{PARA 2 — What you bring, 3-4 sentences. Method, not list.}}

{{PARA 3 — Two proof points with depth. Situation → action → result.}}

Let's connect — {{phone}}.

{{Full Name}}
{{phone}} | {{email}}
{{LinkedIn}} | {{Portfolio}}
```

### Generic Cover Letter (for network forwarding)

```
Dear Friends and Network,

I'm exploring my next role and would appreciate your help. After {{N years}} at
{{Current Company}} {{brief scope description}}, I'm seeking senior product roles.

What I'm looking for:
- {{Role types — e.g., "Senior PM / Director of Product / Principal PM / Head of Product"}}
- {{Company categories — e.g., "AI-first companies, Fortune 500, or GCCs"}}
- {{Domains — e.g., "Consumer platforms, B2B2C, or Fintech"}}

What I bring:
- {{Headline win 1 with verified metric}}
- {{Headline win 2}}
- {{Headline win 3}}
- {{Headline win 4}}

If you know of relevant opportunities or people I should talk to, I'd be grateful
for an introduction. Feel free to forward this note.

Best,
{{First name}}
{{phone}} | {{email}} | {{LinkedIn}}
```

---

## COMPANY-SPECIFIC STRATEGIES

For each archetype: what to lead with, where to place the side-projects section, and the interview angle to rehearse.

### For AI Companies (Anthropic, OpenAI, Google AI, etc.)

**Lead with:** Shipped-AI achievements in Experience, side AI projects, AI certifications, hands-on building philosophy.

**Resume order:** AI / Side Projects after Experience (credibility first). Shipped-AI achievements prominent in Experience bullets. Portfolio link in header.

**Interview angle:** Speak to the gap between AI capabilities and real product value. Show how you've crossed it personally.

### For Consumer Scale (Google, Meta, Netflix, Flipkart, etc.)

**Lead with:** Headline scale metric, growth multipliers, multi-market scope (if applicable).

**Interview angle:** Both 0-to-1 (greenfield market entry) AND 1-N (scale-up) experience. Specific examples of moving needle on a platform that's already live.

### For Enterprise / B2B (Atlassian, Salesforce, Microsoft, etc.)

**Lead with:** Fortune 500 / enterprise partnerships, regulatory expertise (if applicable), B2B2C platform model.

**Resume order:** Partnership work folded into Experience bullets (no standalone section). Emphasize partnership complexity, stakeholder management, compliance expertise.

**Interview angle:** Distribution thinking (selling through partners to reach end users), enterprise procurement, ability to land partner-defined outcomes.

### For Fintech (Stripe, Razorpay, PhonePe, etc.)

**Lead with:** GMV / TPV / payments work, payment gateway integrations, settlement / reliability metrics, bank partnerships.

**Interview angle:** Building trust in a financial context (especially if the user built fintech inside a non-fintech company — that's harder).

### For Telcos (Deutsche Telekom, Verizon, T-Mobile, SoftBank, Vodafone, etc.)

**Lead with:** Direct telco partnerships, OEM + Telco integration experience, B2B2C distribution model, engagement / lock-screen / connectivity products.

**Resume approach:** Summary mentions OEM/telco partnerships; Experience bullets emphasize telco work; product description uses explicit category match.

### For Director+ Roles

**Lead with:** Team building (X to N PMs), cross-functional leadership, strategic influence (any company-direction story), P&L language (GMV, ARPU, unit economics).

**Interview angle:** Director-level impact = shaping company direction, not just executing. Strategic insights that changed where the company invested.

---

## SOURCE OF VERIFIED METRICS

Every numeric claim in a generated resume MUST trace to a row in `YOUR_PROFILE.md`'s verified-metrics tables. If a metric is not in those tables:

1. Do NOT use it.
2. Ask the user whether to add it (with source) or omit it from the bullet.
3. If the user adds it, update `YOUR_PROFILE.md`'s verified-metrics table at the same time.

---

## VERSION HISTORY

- **v1.0** (Template): Generic version extracted from a real director-PM job search workflow. All personal data replaced with placeholders. Methodology preserved verbatim.

---

**END OF SKILL**
