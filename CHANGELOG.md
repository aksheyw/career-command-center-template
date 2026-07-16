# Changelog — Career Command Center Template

## 2.0.1 — 2026-07

Fixes to the 2.0.0 refresh from an independent review — a user-privacy flaw, tracker/skill schema
mismatches, and a few doc contradictions.

### Privacy (critical)

- **The tracker no longer leads users to publish their own job-search data.** `references/applications.md`
  (real companies, recruiters, contacts) is now **git-ignored** and untracked; the committed reference is
  the new **`references/applications.example.md`** (fictional rows only). `track-application` creates and
  maintains the real, local tracker. Generated `references/pattern-analysis-*.md` reports are git-ignored too.
- Added prominent privacy warnings to every personal-data skeleton (`YOUR_PROFILE.md`,
  `CUSTOMIZATION_MEMORY.md`, `STRATEGIC_GAP_ASSESSMENT.md`, `star-stories.md`, `detailed-context.md`) and a
  new **Privacy** section in the README (private-fork vs git-ignore, with a documented `.local.md` convention).

### Tracker schema + skill logic (bug fixes)

- **One authoritative schema, now 14 columns** (was 11): added **Responded** date, **Interview** date, and a
  **Follow-ups** sent-count. Applied across `applications.example.md`, `track-application`, `followup`, and `patterns`.
- **`followup`** now keys urgency off the real Responded/Interview dates and the Follow-ups count, and records a
  send by incrementing that count. Removed the `responded` contradiction (was both "3 days" and "within 24h").
- **`patterns`** funnel is now correct: it counts **"reached at least stage X"** (cumulative, using status ordering
  plus the Responded/Interview dates as stage evidence), so an `interview` row still counts toward the stages it
  passed. The minimum-data gate no longer counts a bare `applied` (no response) as a positive conversion — "converted"
  now means an actual forward signal (screening/responded/interview/offer), which corrects every downstream rate.

### Docs

- **`resume-customizer`**: resolved the conflict-rule contradiction into one two-domain rule (generic wins on
  FORMAT/layout/voice; contested metrics re-derive from the primary source). Softened the XML-diff overclaim and
  added an explicit render-to-PDF-and-look step (diff surfaces drops; the render proves layout/links).
- Reconciled bullet word-counts to one set (40-55 senior / 12-20 early) across QUICKSTART/README/skills.
- Reconciled counts (twelve skills; six personal-data files). Added `santifer/career-ops` (MIT) attribution to the
  `followup`/`patterns` skills, the README skill table, Credits, and the License note.

## 2.0.0 — 2026-07

Content refresh porting the generic mechanisms that evolved in the upstream (private) plugin since the template was first extracted. Everything ported is methodology only — all personal data replaced with this repo's `{{PLACEHOLDER}}` conventions and the fictional `examples/` world (Jane Doe, Northstar AI, BlueCart).

### New skills (10 → 12)

- **`followup`** — follow-up cadence tracker. Reads the structured tracker, flags URGENT / OVERDUE / COLD applications by status-based cadence rules (responded = 3 days, interview = 1 day, applied = 7 days, 2+ touches = suggest closing), then drafts the second-touch email or LinkedIn message. Records a follow-up only after the user confirms it was actually sent — a draft is never logged as sent.
- **`patterns`** — rejection-pattern / conversion analysis. Computes the conversion funnel, score thresholds (recommended GO floor), company-type conversion ranking, blocker buckets, and source performance from the tracker, then proposes concrete targeting changes and closes the loop into `CUSTOMIZATION_MEMORY.md`. Hard minimum-data gate: refuses to analyze fewer than 5 progressed outcomes.

### New reference

- **`references/applications.md`** — structured, machine-readable application tracker (one table, fixed 11-column schema, 9 canonical status tokens). Maintained by `track-application`, queried by `patterns` and `followup`. Ships with two fictional example rows to delete.

### Upgraded skills

- **`resume-customizer`** — three disciplines ported:
  - **Canonical-artifact-first generation (new STEP 0, BLOCKING):** once you maintain a generic resume `.docx`, every tailored resume is built by copying it and applying minimal targeted edits — never rebuilt from the skill's templates — with a programmatic `document.xml` diff afterward to prove nothing validated was dropped. Templates teach style; the canonical is truth about content.
  - **Generic-resume-as-authoritative-benchmark banner:** mirror + render + diff against your maintained generic; never copy a prior company's build script as the spec; when the skill and the generic conflict, the generic wins.
  - **Anti-self-reinforcing metric rules:** unit labels stay attached to every figure; a metric's own guard-rule is never its source of truth; corrections propagate to every copy in one pass.
- **`apply`** — STEP 4 now generates from the canonical (copy + targeted company-type tilts + diff) instead of from templates; new STEP 6.5 maps ATS screening questions to the story bank instead of improvising answers; checklist reference updated to include the blocking Step 0.
- **`track-application`** — now persists the structured tracker (`references/applications.md`) alongside the prose memory, with the fixed schema and status vocabulary the analysis skills depend on; suggests `patterns` at 5+ outcomes and `followup` when applications age past cadence.

### Housekeeping

- README + QUICKSTART: skill inventory updated to 12; structure tree, fill-in file list, and memory-loop description updated.
- Plugin version bumped to 2.0.0 in `.claude-plugin/plugin.json`.
- Note: the upstream plugin's recruiter-lens evaluation reference already exists here in templated form as `references/STRATEGIC_GAP_ASSESSMENT.md` — deliberately not duplicated.

## 1.0.0

Initial template release. 10 skills, skeleton profile/references, fictional end-to-end example (Jane Doe), extracted from a real director-PM job search workflow with all personal data replaced by placeholders.
