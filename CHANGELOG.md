# Changelog — Career Command Center Template

## 2.0.5 — 2026-07

Comprehensive, converging privacy sweep. Prior rounds fixed personal-data files one batch at a time and an
independent reviewer kept finding more tracked files that solicited real data. This release enumerates and
classifies **every** tracked file into DATA / METHODOLOGY / SKILL-INSTRUCTION, so no tracked file can lead a
user to commit real personal data.

### Privacy (the convergence fix) — no tracked file solicits real data anymore

- **`interview-prep.md` is now a DATA file.** It told users to "replace placeholders with your own pitch and
  examples," so a public-repo user filling it in place would commit their real pitch, story mapping, and worked
  examples. It now ships as `skills/resume-customizer/references/interview-prep.example.md` (placeholders only,
  committed) with the standard copy-to-fill privacy banner; the real `interview-prep.md` is git-ignored. The
  generic RCA / guesstimate / case-study frameworks stay in the committed `.example` as reusable methodology.
- **`career-tools.md` stays committed methodology, with its two data-soliciting sections moved out.** The
  "Current compensation (fill from YOUR_PROFILE.md)" table, the "Your stated target" line, and the "Your
  potential references (fill in)" table all invited real comp and reference contacts into a tracked file. They
  now point to `YOUR_PROFILE.md` (git-ignored): comp + target already lived there, and a new **References**
  section was added to `YOUR_PROFILE.example.md` as the git-ignored home for reference contacts. What remains in
  `career-tools.md` is pure methodology — outreach templates, negotiation scripts + principles, a company-type
  compensation *calibration scaffold* (illustrative buckets, not your data), 90-day plans, LinkedIn optimization.
- **`github_in_resume_pattern.md`** no longer says "fill in your own repo names above" — the placeholders are
  reframed as illustration you swap in when *generating* output, not by editing the committed file.

### Consistency

- `.gitignore` adds `skills/resume-customizer/references/interview-prep.md`.
- README "Files to fill in" is now **8 personal-data files** (was 7), with the interview-prep row added; the
  Privacy enumeration, the plugin structure tree, and the "different geography" customization note all updated to
  the new state. No instruction anywhere routes real comp, references, or interview substance into a tracked file.

## 2.0.3 — 2026-07

Third independent-review pass (Codex). The 2.0.2 fixes were confirmed working; this release closes the
generated-document leak plus residual privacy, cadence, and consistency issues.

### Privacy (critical) — generated resumes + cover letters could still be committed

- **Generated application documents are now git-ignored by design.** 2.0.2 protected the hand-filled
  input files but not the tool's *output*: the tailored resumes and cover letters `apply` /
  `resume-customizer` produce (`{{LastName}}_{{FirstName}}_Resume_{{Company}}.docx`, `..._CoverLetter_...`)
  carry the user's real name, history, and target company, yet only `references/generic-resume.*` was
  ignored — a `git add .` could stage them. Fixed: all generated documents now write into a new,
  git-ignored `output/` directory (only its `README.md` is tracked), and the generated-document
  filename patterns (`*_Resume_*.docx`, `*_CoverLetter_*.docx`, `.pdf` siblings) are ignored as a
  backstop. `apply` and `resume-customizer` "Save as" instructions now target `output/`. README Privacy
  + QUICKSTART state the output is git-ignored by design.

- **"Private fork" guidance corrected to "private standalone repo."** A GitHub fork of a public repo is
  always public — fork visibility cannot be changed — so the previous primary recommendation was wrong.
  README + QUICKSTART now recommend cloning the template into a brand-new **private** repository (with the
  exact `git clone` + `gh repo create --private` commands), and the word "fork" is reserved for where it
  is technically accurate (e.g. contributing improvements back to the template).

- **New "if you already committed or pushed real data" recovery branch** in the README Privacy section:
  untrack-and-commit for local-only, history purge via `git filter-repo` / BFG (or delete-and-recreate
  the repo) for already-pushed, plus an exposure-response note that anything pushed public must be treated
  as compromised. Previously the guidance only covered untracking, which does not remove pushed history.

### Cadence correctness (`followup`)

- **Interview urgency now has a bounded lifecycle.** An interview with no logged thank-you was URGENT
  forever, so a months-old interview stayed permanently URGENT. Now: URGENT (24h thank-you) applies only
  when the interview is today or within ~1 day; past that window with no logged thank-you it ages to
  OVERDUE (late thank-you), not perpetual URGENT; and an interview more than ~30 days past with no
  progression ages into COLD (stale). Every interview state now has a dated exit, matching how
  `responded` already worked.

### Analysis correctness (`track-application`)

- **Zero-denominator guard added to the pipeline conversion rates.** `patterns` had this guard; the
  `track-application` STEP 5 summary (applications→screens, screens→interviews, interviews→offers) did
  not. It now prints "insufficient data for this rate" on a zero denominator instead of dividing by zero
  or printing a misleading `0%`.

### Consistency fixes

- **Reconciled contradictory KEY ACHIEVEMENTS guidance.** `references/YOUR_PROFILE.example.md` said
  "always include in resume KEY ACHIEVEMENTS section" while `resume-customizer` says the resume has **no**
  Key Achievements section. The profile now clarifies that its "KEY ACHIEVEMENTS" heading is a profile
  storage bucket (feed it into Summary + Experience bullets) and defers to `resume-customizer` as
  authoritative on resume structure.
- **Fixed a mixed-currency figure** in `examples/EXAMPLE_PROFILE.md` ("₹560M USD" → "$560M"), consistent
  with the example's USD figures elsewhere. Fictional, cosmetic.

## 2.0.2 — 2026-07

Second independent-review pass (Codex). The 2.0.1 privacy + funnel fixes were confirmed working; this
release closes 6 remaining issues.

### Privacy (critical) — the other personal-data files could still be committed on a public fork

- **Every hand-filled personal-data file now ships as a committed `*.example.md` skeleton; the real
  filename is git-ignored.** 2.0.1 fixed only `applications.md`. The other files (`YOUR_PROFILE.md`,
  `CUSTOMIZATION_MEMORY.md`, `STRATEGIC_GAP_ASSESSMENT.md`, `star-stories.md`, `detailed-context.md`,
  and `story-bank-index.md`) were tracked skeletons — a public-fork user who filled them in place would
  commit real data, because `.gitignore` can't suppress edits to already-tracked files. They are now
  `*.example.md` (placeholders only, committed) and you **copy to the real filename** (git-ignored) and
  fill the copy. The documented happy path can no longer commit real personal data on a public fork.
- **Primary guidance is a PRIVATE standalone repo** (clone, don't fork — GitHub forks of a public repo stay public), stated prominently in the README and QUICKSTART. The
  `.example.md` + git-ignore machinery is the belt-and-suspenders for public forks. README documents
  `git rm --cached <file>` for anyone upgrading whose real-named skeleton is already tracked.
- Session-start hook, `track-application`, and `update-memory` degrade gracefully when a real file
  doesn't exist yet (hook prints a copy-me hint; the write skills seed from the `.example.md`).

### Analysis correctness (`patterns`)

- **Outcome classes are now mutually exclusive** — `offer` / `rejected` / `self_filtered` / `in_flight`
  (+ `pending` for evaluated-only). 2.0.1 let a progressed-then-rejected row count as both "converted"
  and "negative," double-counting it. The FUNNEL stays separate and cumulative ("reached at least stage
  X"), so a rejected-after-interview row still counts toward reached-interview but its OUTCOME is exactly
  `rejected`. No row is ever in two outcome buckets.
- **The minimum-data gate now requires real signal** — ≥5 rows that are terminal (`rejected`/`offer`)
  OR reached a forward stage (a Responded/Interview date). Pure `in_flight` and `self_filtered` rows no
  longer satisfy it, so 5 skips can't pass a gate that then produces zero-denominator rates.
- **Every rate denominator is zero-guarded** — s/a, i/s, o/i and all per-type/per-source rates report
  "insufficient data for this rate" instead of dividing by zero.

### Resume canonical path (`resume-customizer`, `apply`)

- **The canonical generic resume now has a real default path** — `references/generic-resume.docx`
  (git-ignored). 2.0.1's `{{path/to/your/generic-resume.docx}}` placeholder was never wired, so the
  BLOCKING canonical lookup had nothing to read. The skills read the fixed path first; the optional
  `{{…}}` override remains for a custom location; and the "first generated resume becomes canonical"
  fallback now actually saves there.

### Follow-up cadence (`followup`)

- **Interview urgency is now dated, with an exit.** It was permanently URGENT. Now: a future Interview
  date is `upcoming` (not actionable); a just-held interview is URGENT for a 24h thank-you that exits
  once a follow-up dated on/after the interview is logged; then a 5-7 business-day status-check (OVERDUE);
  then COLD at 2 touches.
- **Write-boundary contradiction resolved** — a confirmed send writes BOTH the Last-follow-up date AND
  the incremented Follow-ups count (the Boundaries note wrongly said "the only write is the Last
  follow-up date").

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
