---
name: patterns
description: "Analyze the application tracker for what converts and what wastes time. Surfaces score thresholds, winning archetypes, and the blockers driving rejections, then proposes targeting changes. Argument: none."
---

You are running rejection-pattern analysis on the user's job search. The goal is a feedback loop: stop applying to the patterns that reject them, double down on the ones that convert.

Analysis model adapted from career-ops's `patterns` mode (santifer/career-ops), rebuilt to read this plugin's tracker. No external scripts — reason over the data directly.

## STEP 1: Load the data

Read `${CLAUDE_PLUGIN_ROOT}/references/applications.md` (the structured tracker maintained by the `track-application` skill). Also read `${CLAUDE_PLUGIN_ROOT}/references/CUSTOMIZATION_MEMORY.md` for prose context.

If `applications.md` does not exist, or contains only the shipped example rows, tell the user: "No structured tracker yet. Log outcomes with `track-application` first." Stop.

## STEP 2: Minimum-data gate (do not skip)

Classify each row's status into an outcome group:
- **positive** → `applied`, `screening`, `responded`, `interview`, `offer`
- **negative** → `rejected`, `discarded`
- **self_filtered** → `skip`
- **pending** → `evaluated`

Count rows with status beyond `evaluated` (i.e. any positive, negative, or self_filtered). If that count is **< 5**, stop and say:

> "Not enough signal yet — {N}/5 applications have progressed beyond evaluation. Pattern analysis on fewer than 5 outcomes is noise, not signal. Keep applying and come back."

This gate is the whole point. Never hand-wave an analysis on thin data — a vague report built on 3 data points is worse than no report.

## STEP 3: Compute the dimensions

From the tracker rows, compute:

1. **Conversion funnel** — count per stage (evaluated → applied → screening → interview → offer), each as a count and % of total.
2. **Score thresholds** — average / min / max evaluation **Score** for the positive group vs the negative group. If positives cluster above a score that negatives rarely clear, that score is the recommended GO floor.
3. **Archetype / company-type breakdown** — per **Type** (AI / Consumer / Enterprise / Fintech / Telco / Other): total, positive, negative, and conversion rate (positive ÷ total). Rank by conversion.
4. **Blocker analysis** — tally the **Outcome reason** column across negatives + self_filtered. Group into buckets (geo-restriction, stack/skill mismatch, seniority mismatch, onsite/relocation, comp, timing). Rank most-frequent first.
5. **Source breakdown** — conversion rate by **Source** (referral vs direct vs recruiter). Referrals usually convert higher; quantify the gap.

## STEP 4: Write the report

Write to `${CLAUDE_PLUGIN_ROOT}/references/pattern-analysis-{YYYY-MM-DD}.md`:

```markdown
# Pattern Analysis — {YYYY-MM-DD}

**Applications analyzed:** {total} ({positive} positive, {negative} negative, {self_filtered} self-filtered, {pending} pending)
**Date range:** {earliest applied} to {latest}

## Conversion Funnel
| Stage | Count | % |
|-------|-------|---|

## Score Threshold
Positives average {X.X}, negatives {Y.Y}. Recommended GO floor: {Z.Z}/5 — {one-line reasoning}.

## What Converts (by company type)
| Type | Total | Positive | Conversion |
Ranked best-first. Name the top archetype to lean into.

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
