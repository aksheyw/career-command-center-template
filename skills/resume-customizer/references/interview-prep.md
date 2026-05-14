# Interview Preparation — Template

**Purpose:** Frameworks and preparation guides for director-level PM interviews.
**Contents:** 2-minute pitch template, common questions, RCA framework, guesstimate framework, case study framework, questions to ask.
**Personalize:** Replace placeholders with your own pitch and examples.

---

## 2-MINUTE PITCH (template)

```
"I'm a {{current title}} at {{current company}} where I {{primary ownership —
1 line; what you actually do day-to-day, not your job title}}. {{Scope sentence:
team size + market count + headline metric}}.

My biggest win: {{1 story in 2-3 sentences, with verified metrics from
YOUR_PROFILE.md}}.

{{Optional second proof point — different company or different domain to show
range}}.

I'm looking for a {{target title}} role where I can {{specific career
progression goal}}. I'm particularly interested in [COMPANY] because
[SPECIFIC REASON drawn from research about them]."
```

**Rehearse out loud.** Time it. Should be 90-120 seconds in normal speaking pace, not rushed.

---

## STAR STORY SELECTION (Cross-reference with `star-stories.md`)

| Question Type | Primary Story | Backup Story |
|--------------|---------------|--------------|
| "Tell me about scaling a product" | {{From your story-bank-index}} | {{From your story-bank-index}} |
| "Tell me about an AI product you built" | {{Story}} | {{Story}} |
| "Tell me about leading a team" | {{Story}} | {{Story}} |
| "Tell me about a failure" | {{Failure story}} | {{Failure story}} |
| "Tell me about a difficult trade-off" | {{Story}} | {{Story}} |
| "Tell me about building from zero" | {{Story}} | {{Story}} |
| "Tell me about payments / fintech" | {{Story}} | {{Story}} |
| "Tell me about partnerships" | {{Story}} | {{Story}} |
| "Tell me about a technical problem" | {{Story}} | {{Story}} |
| "Tell me about pushing back" | {{Story}} | {{Story}} |
| "Tell me about international expansion" | {{Story}} | {{Story}} |
| "Tell me about mentoring" | {{Story}} | {{Story}} |

---

## COMMON INTERVIEW QUESTIONS

### "Tell me about yourself"

Use the 2-minute pitch above. Customize the ending for the specific company.

### "Why are you looking for a new role?"

```
"I've had a great {{N}} years at {{current company}} - {{2-3 wins listed
compactly}}. But I've hit a ceiling. {{Specific honest reason — scope is bounded,
no upward path, want different domain}}. I'm looking for a {{target title}}
where I can {{specific growth goal}}. The timing is right - {{transition
readiness — team set up, project shipped, etc.}}."
```

### "What's your biggest failure?"

Pull a real failure story from `star-stories.md`. Failures need three things: (1) Specifics — what went wrong, (2) Honest ownership of YOUR role in it, (3) What you'd do differently and how it shaped you. Avoid generic answers like "I work too hard."

### "How do you handle conflict?"

Story from `star-stories.md` that involves pushing back on engineering, design, or leadership when you disagreed. Frame: principled decision-making, not stubbornness.

### "Tell me about a time you influenced without authority"

Cross-team / cross-company / cross-functional story. Bonus if a stakeholder didn't report to you and you got them to commit to your direction.

### "Why this company?"

Research the company and prepare 2-3 specific reasons:

- Recent news / product launch you find interesting
- Something about their approach that aligns with your experience
- A specific problem you could solve

**Never** say "I love your culture" without specifics.

### "What's your leadership style?"

Template:

```
"I lead by {{your style — context-not-control / coach-mode / hands-on}}. I
{{specific behavior 1}}, {{specific behavior 2}}, then {{specific behavior 3}}.
At {{current company}}, I {{concrete proof — e.g., built a team, promoted N,
shipped despite stakeholder disagreement}}."
```

### "How do you prioritize?"

```
"I use a combination of impact and confidence. Impact is straightforward - what's
the expected business value? Confidence is harder - how sure are we about the
impact estimate? For new markets or new features, I prioritize learning first
(experiments, user research) before committing to full builds."
```

Adapt to your actual approach.

---

## QUESTIONS TO ASK INTERVIEWER (signals director thinking)

### Strategic questions

- "What's the biggest product bet the company is making in the next 18 months?"
- "How does this role influence company strategy vs execute on it?"
- "What would success look like at 6 months vs 18 months?"
- "What's the product org's relationship with engineering leadership?"

### Team / culture questions

- "How are product decisions made when engineering disagrees?"
- "What happened to the last person in this role?"
- "How much autonomy would I have over team hiring and structure?"
- "How does the company approach experimentation and failure?"

### Red-flag probing questions

- "What's the biggest challenge the product org is facing right now?"
- "How does leadership view the product function - cost center or growth driver?"
- "What's the typical timeline from idea to launch here?"

---

## CASE STUDY FRAMEWORK

Many Director PM interviews require take-home cases or live product exercises.

### Structure (30-45 minute presentation)

**1. PROBLEM UNDERSTANDING (2 min)**

- Clarify the ask
- State assumptions explicitly
- Define scope and constraints

**2. USER ANALYSIS (5 min)**

- Who are the users? (Segment them)
- What are their pain points? (Prioritize)
- Which segment to focus on? (Justify)

**3. SOLUTION APPROACH (10 min)**

- 3 potential solutions (show you considered alternatives)
- Evaluation criteria (impact, effort, risk)
- Recommended solution with clear rationale

**4. SUCCESS METRICS (5 min)**

- North star metric (one primary goal)
- Supporting metrics (leading indicators)
- How to measure (instrumentation plan)

**5. ROADMAP (5 min)**

- Phase 1: MVP (0-3 months) - what's the smallest valuable thing?
- Phase 2: Scale (3-6 months) - what comes next?
- Phase 3: Expand (6-12 months) - long-term vision

**6. RISKS & MITIGATION (3 min)**

- Technical risks (what could fail?)
- Business risks (market, competition)
- User adoption risks (behavior change needed?)

### Your real examples to reference

Pull 3-4 cases from your `star-stories.md` that map to:

- **0-to-1 case:** {{Your best 0-to-1 story}}
- **Feature ideation:** {{Your best feature-ideation story}}
- **Fintech case (if applicable):** {{Story}}
- **Scale case:** {{Best scale-up story}}

---

## RCA (ROOT CAUSE ANALYSIS) FRAMEWORK

Common question: "DAU dropped 10% last week. Diagnose."

### Step 1: CLARIFY

- Which metric exactly? (DAU, WAU, MAU)
- Which segment? (All users, new, returning, specific market)
- What timeframe? (Sudden drop vs gradual)
- How much? (10% relative or absolute)

### Step 2: HYPOTHESIZE (MECE Categories)

**EXTERNAL FACTORS:**

- Seasonality (holidays, school calendar, weather)
- Competition (new entrant, feature launch)
- Market events (economic, regulatory, political)
- Platform changes (iOS / Android update, policy change)

**INTERNAL — PRODUCT:**

- Recent release (bug, UX change, regression)
- Feature deprecation or removal
- Performance issues (load time, crashes, errors)
- Content quality change

**INTERNAL — TECHNICAL:**

- Infrastructure issues (server, CDN, API)
- Data pipeline problems (are we measuring correctly?)
- Third-party dependency failure
- Integration issues

**INTERNAL — BUSINESS:**

- Marketing spend change
- Pricing change
- Partner relationship change
- Fraud / spam increase

### Step 3: PRIORITIZE & INVESTIGATE

- Most likely hypotheses first
- What data would prove / disprove each?
- Who needs to be involved?

### Step 4: RECOMMEND

- Root cause identified
- Fix proposed with timeline
- Prevention for future (monitoring, alerts)

### Your real example

Pull from `star-stories.md` — your strongest RCA story. Common shape:

```
"At {{company}}, {{metric}} dropped {{N%}} despite {{paradox condition — sales
up while DAU down, etc.}}. I led the RCA covering external and internal factors.
We discovered {{root cause}} — {{specific finding}}.

Fixed within {{timeline}}, recovered {{outcome}}. Root cause identified in
{{N hours}} through cross-functional coordination with engineering, data
science, and ops.

Key learning: I now {{prevention you put in place}}."
```

---

## GUESSTIMATE FRAMEWORK

Common at MBB consulting roles and at big tech (FAANG, Indian unicorns): "Estimate X in {region}."

### Approach: state whether top-down or bottom-up

**EXAMPLE: "Estimate daily food delivery orders in {city}"**

**TOP-DOWN:**

1. {City} population: {N million}
2. Households: {N / avg household size}
3. Smartphone penetration: {%} = {N households}
4. Food delivery app users: {%} = {N households}
5. Order frequency: {N per week} = {fraction per day}
6. Daily orders: {N} × {fraction} = {result}

**BOTTOM-UP:**

1. Major players: {list 2-3}
2. Leader's market share: {%}
3. Leader claims {N orders / day} country-wide
4. {City} is {%} of leader's business = {N}
5. Total market (Leader = {%}): {N} ÷ {decimal} = {result}

**RECONCILE:**

State which assumptions could vary and the sensitivity. The two methods should be within 2x of each other; if not, one assumption is way off.

### Tips

- Always state your approach (top-down vs bottom-up)
- Round numbers are fine (easier to calculate)
- Show your math (out loud)
- Acknowledge uncertainties
- Sanity check the final number

### Common estimation types

- Market size (users, revenue, units)
- Capacity planning (servers, drivers, inventory)
- Financial (revenue, cost, margin)
- Operational (time to complete, resources needed)

---

## INTERVIEW PREPARATION CHECKLIST

### 1 hour before interview

- [ ] Review this document
- [ ] Review 3-4 STAR stories relevant to company type
- [ ] Review company-specific strategy from `SKILL.md`
- [ ] Review recent company news (last 30 days)
- [ ] Prepare 3 questions to ask
- [ ] Review your resume (what they saw)

### Night before

- [ ] Research company deeply
- [ ] Identify 2-3 ways your experience maps to their problems
- [ ] Practice 2-minute pitch out loud
- [ ] Prepare salary range and negotiation points

### For panel interviews

- [ ] Research each interviewer on LinkedIn
- [ ] Prepare different angles for different interviewers (PM vs Eng vs Design)
- [ ] Have multiple STAR stories ready (don't repeat the same one across panelists)

---

## COMPANY-SPECIFIC INTERVIEW ANGLES

Pull these from `SKILL.md`'s company-type strategies — adapt the angle for the specific company. Each angle is one sentence that frames your unique value for that archetype.

### For AI Companies (Anthropic, OpenAI, AI startups)

"{{Your hands-on AI shipping angle — distinguish strategy from execution}}"

### For Consumer Scale (Google, Meta, big consumer platforms)

"{{Your scale + 0-to-1 + 1-to-N angle}}"

### For Enterprise / B2B (Atlassian, Salesforce, SaaS)

"{{Your B2B2C / Fortune 500 partnership angle}}"

### For Fintech (Stripe, payments, neobanks)

"{{Your trust + GMV + reliability angle, especially if you've shipped fintech inside a non-fintech company}}"

### For Telcos (regional carriers, OEM partnerships)

"{{Your distribution + telco partnerships angle}}"

### For Director+ Roles

"{{Your strategic-influence angle — a story where YOUR insight changed company direction}}"

---

**For outreach templates, salary negotiation, and 90-day plans, see: `career-tools.md`**
**For full STAR stories, see: `star-stories.md`**
