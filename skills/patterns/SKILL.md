---
name: patterns
description: "Analyze the application tracker for what converts and what wastes time. Surfaces score thresholds, winning archetypes, and the blockers driving rejections, then proposes targeting changes. Argument: none."
---

You are running rejection-pattern analysis on the user's job search. The goal is a feedback loop: stop applying to the patterns that reject them, double down on the ones that convert.

Analysis model adapted from the `patterns` mode of [santifer/career-ops](https://github.com/santifer/career-ops) (MIT), rebuilt to read this plugin's tracker. No external scripts — reason over the data directly.

## STEP 1: Load the data

Read `${CLAUDE_PLUGIN_ROOT}/references/applications.md` (the user's real tracker, maintained by `track-application`; git-ignored). Also read `${CLAUDE_PLUGIN_ROOT}/references/CUSTOMIZATION_MEMORY.md` for prose context.

If `applications.md` does not exist, or contains only the shipped fictional example rows, tell the user: "No structured tracker yet. Log outcomes with `track-application` first." Stop. (The committed `applications.example.md` is a schema reference only — never analyze its rows as real.)

## STEP 2: Classify each row, then apply the minimum-data gate (do not skip)

Give each row TWO independent classifications — keep them separate, they answer different questions and must never be summed together.

### A. Outcome class — each row lands in EXACTLY ONE (this is what every OUTCOME rate uses)

The terminal (or current-terminal) state of the row. Mutually exclusive by construction, so no row is ever counted in two outcome buckets:

- **`offer`** — status = `offer`. Terminal positive.
- **`rejected`** — status ∈ {`rejected`, `discarded`}. Terminal negative (`discarded` = went dead / ghosted with no formal rejection — still a dead end).
- **`self_filtered`** — status = `skip`. You withdrew or never applied by choice. Excluded from every conversion denominator (it says nothing about how the market responds to you).
- **`in_flight`** — applied but no terminal decision yet: status ∈ {`applied`, `screening`, `responded`, `interview`}. Still active, so the outcome is genuinely unknown — EXCLUDED from outcome rates (never counted as converted OR as rejected).
- **`pending`** — status = `evaluated` (never applied). Sits outside the funnel and every outcome rate.

Because these are mutually exclusive, **a row that reached an interview and was then rejected is `rejected` — only `rejected`.** Its interview progress is recorded in the funnel below, not as a second outcome. Nothing is double-counted.

### B. Funnel stage reached — cumulative, a row can satisfy several (this is what the FUNNEL uses)

How far the row got, independent of its outcome class, using status ordering plus the Responded/Interview dates as evidence that a stage was passed even on a row that later went terminal:

- **reached applied** — actually submitted: status ∈ {`applied`, `screening`, `responded`, `interview`, `offer`, `rejected`, `discarded`} (everything except `evaluated` and `skip`).
- **reached screening** — status ∈ {`screening`, `responded`, `interview`, `offer`}, **or** a **Responded** date is present, **or** an **Interview** date is present.
- **reached interview** — status ∈ {`interview`, `offer`}, **or** an **Interview** date is present.
- **reached offer** — status = `offer`.

A `rejected` row with an Interview date reached applied + screening + interview in the funnel, while its outcome class stays exactly `rejected`.

### Minimum-data gate (do not skip)

Count the rows that carry a REAL market signal:

> a row counts toward the gate if its **outcome class is `rejected` or `offer`** (a terminal decision landed), **OR** it **reached screening or interview** (a Responded or Interview date is present — it moved past bare "applied").

Bare `in_flight` rows (applied, no Responded/Interview date, not terminal), `self_filtered`, and `pending` rows do NOT count — they carry no signal about what converts. If the real-signal count is **< 5**, stop and say:

> "Not enough signal yet — {N}/5 applications carry a real signal (a reply, an interview, a rejection, or an offer). Bare 'applied, no response yet' rows and self-skips don't count. Pattern analysis on fewer than 5 is noise, not signal. Keep applying and come back."

This gate is the whole point. Never hand-wave an analysis on thin data — a vague report built on 3 data points is worse than no report.

## STEP 3: Compute the dimensions

Use the **outcome classes** (STEP 2A) for outcome buckets and the **cumulative stages** (STEP 2B) for the funnel — never mix them, and never let a row fall into two outcome buckets.

**Zero-denominator guard (applies to EVERY rate below):** if a denominator is 0, print "insufficient data for this rate" and move on. Never divide by zero, never report a rate as 0% when what you mean is "no data."

**Denominator base:** `applied` = the count of rows that **reached applied** (this excludes `pending` and `self_filtered`). For a clean, no-double-count binary in the rate calcs, define **progressed = reached screening** — a row either moved past bare "applied" or it didn't, so it is in exactly one side.

Then compute:

1. **Conversion funnel** — count of rows that reached at least each stage: applied → screening → interview → offer. Show each count, its % of the applied count (top of funnel), and the step-to-step conversion (screening/applied, interview/screening, offer/interview). Guard EACH ratio with the zero rule — if a step's denominator stage count is 0, print "insufficient data for this rate" for that step. `pending` and `self_filtered` rows sit above the funnel and are reported separately, never inside these counts.
2. **Score thresholds** — compare the average / min / max evaluation **Score** of **progressed** rows (reached screening) against rows that are `rejected` and did NOT reach screening (rejected at the top of the funnel). `in_flight` rows that never progressed, and any row with no Score, are excluded. If either group is empty, report "insufficient data for a score threshold." If progressed rows cluster above a score the early-rejected rarely clear, that score is the recommended GO floor.
3. **Archetype / company-type breakdown** — per **Type** (AI / Consumer / Enterprise / Fintech / Telco / Other): applied count (rows of that type that reached applied), progressed count (reached screening), and progression rate = progressed ÷ applied for that type. If a type's applied count is 0, print "—", not a division. Rank by rate.
4. **Blocker analysis** — tally the **Outcome reason** column across `rejected` + `self_filtered` rows. Group into buckets (geo-restriction, stack/skill mismatch, seniority mismatch, onsite/relocation, comp, timing). Rank most-frequent first.
5. **Source breakdown** — progression rate by **Source** (`recruiter-outbound`, `referral-warm`, `referral-list`, `cold-direct`) = progressed ÷ applied for that source, same zero-denominator guard. Keep the two referral kinds apart: merging a warm referral with a forwarded name hides any difference between them. Quantify the gaps where the denominators allow.

## STEP 4: Write the report

Write to `${CLAUDE_PLUGIN_ROOT}/references/pattern-analysis-{YYYY-MM-DD}.md`:

```markdown
# Pattern Analysis — {YYYY-MM-DD}

**Applications analyzed:** {total} — outcomes: {offer} offer, {rejected} rejected, {self_filtered} self-filtered, {in_flight} in flight (no terminal outcome yet), {pending} evaluated-only
**Date range:** {earliest applied} to {latest}

## Conversion Funnel (reached at least each stage)
| Stage | Count | % of applied | Step conversion |
|-------|-------|--------------|-----------------|
| Applied | {a} | 100% | — |
| Screening | {s} | {s/a}% | {s/a}% |
| Interview | {i} | {i/a}% | {i/s}% |
| Offer | {o} | {o/a}% | {o/i}% |

(Any cell whose denominator is 0 reads "insufficient data" — never a divide.)

## Score Threshold
Progressed rows (reached screening) average {X.X}; rows rejected before screening average {Y.Y}. Recommended GO floor: {Z.Z}/5 — {one-line reasoning}. (If either group is empty: "insufficient data for a score threshold.")

## What Converts (by company type)
| Type | Applied | Progressed | Progression rate |
Progression rate = progressed ÷ applied (reached screening ÷ reached applied). Ranked best-first; "—" where a type has 0 applied. Name the top archetype to lean into.

## What Wastes Time (top blockers)
| Blocker | Count | Example |
Ranked most-frequent first.

## Source Performance
Recruiter-outbound {A}% · referral-warm {B}% · referral-list {C}% · cold-direct {D}%.

## Top 5 Targeting Changes
1. [specific, actionable — e.g. "Raise GO floor to 3.5; 4 of 5 rejections scored below it"]
...
```

## STEP 5: Close the loop into memory

Propose 1–3 concrete additions to the learnings sections of `CUSTOMIZATION_MEMORY.md` based on the findings (e.g. "Avoid geo-restricted roles — 3/3 self-filtered or rejected"). Show the diff; on approval, write it back. This is what makes the analysis compound instead of being a one-off report.

## Boundaries

Reads the tracker and reports; the only write is the dated report + (on approval) the memory diff. Never invents outcomes or reasons not present in the tracker — if the **Outcome reason** column is blank on a negative, flag it as missing data, do not guess the reason.
