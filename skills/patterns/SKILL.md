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

First classify each row into an outcome group. **A bare `applied` with no response is NOT a conversion** — it is still in flight and tells you nothing yet. Use the **Responded** and **Interview** date columns as the forward-signal evidence, since a terminal row (rejected/discarded) still carries the date of how far it got:

- **converted (forward signal)** → status ∈ {`screening`, `responded`, `interview`, `offer`}, **or** the row has a **Responded** date, **or** it has an **Interview** date. (An actual reply/interview happened.)
- **negative** → status ∈ {`rejected`, `discarded`}.
- **self_filtered** → status = `skip`.
- **in_flight** → status = `applied` with no Responded/Interview date (submitted, no reply yet).
- **pending** → status = `evaluated` (not yet applied).

**Minimum-data gate:** count the rows that carry a real signal — `converted` + `negative` + `self_filtered` (this deliberately EXCLUDES `in_flight` bare-applied and `pending` rows, which are not outcomes yet). If that count is **< 5**, stop and say:

> "Not enough signal yet — {N}/5 applications have a real outcome (a reply, interview, rejection, or self-filter). Bare 'applied, no response yet' rows don't count. Pattern analysis on fewer than 5 outcomes is noise, not signal. Keep applying and come back."

This gate is the whole point. Never hand-wave an analysis on thin data — a vague report built on 3 data points is worse than no report.

## STEP 3: Compute the dimensions

The tracker stores only each row's CURRENT status, so compute the funnel as **"reached at least stage X"** (cumulative, monotonic), using status ordering plus the Responded/Interview dates as stage evidence — an `interview` row still counts toward the `applied` and `screening` stages it passed through, and a `rejected` row with an Interview date reached interview before it died.

Per row, mark the furthest stage reached:
- **reached applied** — any row that was actually submitted: status ∈ {`applied`, `screening`, `responded`, `interview`, `offer`, `rejected`, `discarded`} (everything except `evaluated` and `skip`).
- **reached screening** — status ∈ {`screening`, `responded`, `interview`, `offer`}, **or** a Responded date is present, **or** an Interview date is present.
- **reached interview** — status ∈ {`interview`, `offer`}, **or** an Interview date is present.
- **reached offer** — status = `offer`.

Then compute:

1. **Conversion funnel** — count of rows that reached at least each stage: applied → screening → interview → offer. Show each count and its % of the applied count (the top of the funnel), plus the step-to-step conversion (screening/applied, interview/screening, offer/interview). `evaluated`-only and `skip` rows sit above the funnel and are reported separately, not inside these counts.
2. **Score thresholds** — average / min / max evaluation **Score** for the `converted` group vs the `negative` group. (Bare `in_flight` rows are excluded — no outcome yet.) If converted rows cluster above a score that negatives rarely clear, that score is the recommended GO floor.
3. **Archetype / company-type breakdown** — per **Type** (AI / Consumer / Enterprise / Fintech / Telco / Other): applied count, converted, negative, and conversion rate = converted ÷ (applied count for that type, i.e. converted + negative + in_flight). Rank by conversion.
4. **Blocker analysis** — tally the **Outcome reason** column across negatives + self_filtered. Group into buckets (geo-restriction, stack/skill mismatch, seniority mismatch, onsite/relocation, comp, timing). Rank most-frequent first.
5. **Source breakdown** — conversion rate by **Source** (referral vs direct vs recruiter), same converted ÷ applied denominator. Referrals usually convert higher; quantify the gap.

## STEP 4: Write the report

Write to `${CLAUDE_PLUGIN_ROOT}/references/pattern-analysis-{YYYY-MM-DD}.md`:

```markdown
# Pattern Analysis — {YYYY-MM-DD}

**Applications analyzed:** {total} ({converted} converted, {negative} negative, {self_filtered} self-filtered, {in_flight} in flight, {pending} evaluated-only)
**Date range:** {earliest applied} to {latest}

## Conversion Funnel (reached at least each stage)
| Stage | Count | % of applied | Step conversion |
|-------|-------|--------------|-----------------|
| Applied | {a} | 100% | — |
| Screening | {s} | {s/a}% | {s/a}% |
| Interview | {i} | {i/a}% | {i/s}% |
| Offer | {o} | {o/a}% | {o/i}% |

## Score Threshold
Converted rows average {X.X}, negatives {Y.Y}. Recommended GO floor: {Z.Z}/5 — {one-line reasoning}.

## What Converts (by company type)
| Type | Applied | Converted | Conversion |
Conversion = converted ÷ applied. Ranked best-first. Name the top archetype to lean into.

## What Wastes Time (top blockers)
| Blocker | Count | Example |
Ranked most-frequent first.

## Source Performance
Referral {X}% vs direct {Y}% vs recruiter {Z}%.

## Top 5 Targeting Changes
1. [specific, actionable — e.g. "Raise GO floor to 3.5; 4 of 5 rejections scored below it"]
...
```

## STEP 5: Close the loop into memory

Propose 1–3 concrete additions to the learnings sections of `CUSTOMIZATION_MEMORY.md` based on the findings (e.g. "Avoid geo-restricted roles — 3/3 self-filtered or rejected"). Show the diff; on approval, write it back. This is what makes the analysis compound instead of being a one-off report.

## Boundaries

Reads the tracker and reports; the only write is the dated report + (on approval) the memory diff. Never invents outcomes or reasons not present in the tracker — if the **Outcome reason** column is blank on a negative, flag it as missing data, do not guess the reason.
