---
name: salary-negotiate
description: Full salary negotiation prep — current comp, target, scripts, and counter-offer handling. Argument: [company name] [optional: offer details]
---

You are preparing the user for salary negotiation. Read ALL of the following before responding:

- `${CLAUDE_PLUGIN_ROOT}/skills/resume-customizer/references/career-tools.md` — full salary negotiation section including current comp template, target ranges by company type, scripts, counter-offer handling, notice-period negotiation
- `${CLAUDE_PLUGIN_ROOT}/references/YOUR_PROFILE.md` — current compensation context

## STEP 1: Assess the situation

Based on the user's input, determine:

- Company type (MNCs / Top Local / Growth Startup — adapt categories to user's geography)
- What stage of negotiation: first offer / counter / final push
- Whether an offer has been received or if preparing pre-offer

## STEP 2: Output the full negotiation brief

### CURRENT COMPENSATION CONTEXT

Pull from `YOUR_PROFILE.md` (Job Search Status → Current Compensation table). Include:

- Base
- Equity (units, value, liquidity status)
- Vested / unvested percentages
- Key point: any liquidity, restriction, or forfeit risk

### TARGET RANGE FOR THIS COMPANY

Pull the correct target from `career-tools.md` based on company type. Match to the user's stated target from `YOUR_PROFILE.md`.

### READY-TO-USE SCRIPTS

- Script 1 — When asked "What are your salary expectations?": pull exact script from `career-tools.md`. Do not paraphrase.
- Script 2 — When asked "What are you currently making?": pull exact script from `career-tools.md`. Focus on the user's leverage point (illiquid equity argument, restricted vesting, etc.).
- Script 3 — When receiving an offer below target: pull counter-offer guidance from `career-tools.md`. Expand with company-specific framing.

### WHAT TO NEGOTIATE BEYOND BASE SALARY

From `career-tools.md`: signing bonus (to cover unvested equity forfeit), equity, title, start date.

Calculate unvested forfeit value if an offer has been received. This is the minimum signing bonus to ask for.

### COUNTER-OFFER HANDLING

If the current employer counters, use the response template from `career-tools.md`. Emphasize: the decision was about scope and growth, not compensation.

### NOTICE-PERIOD STRATEGY

Pull from `YOUR_PROFILE.md`'s notice period. Options:

- Ask new company for signing bonus to cover notice buyout
- Ask current employer for early release
- Offset with unused PTO

### NEGOTIATION PRINCIPLES (NON-NEGOTIABLE)

1. Never give a number first — always ask for their range first
2. Give a range, not a single number, when pressed
3. Use the user's specific leverage argument from `YOUR_PROFILE.md` (illiquid equity, restricted vesting, etc.) if applicable
4. Multiple processes = stronger position. Only mention if true.
5. Always negotiate — base, signing, equity, title — even if you plan to accept
