# Application Tracker — EXAMPLE (committed reference)

**This is the committed example, not your real tracker.** It shows the schema and two
**fictional** rows (same fictional world as `examples/` — Northstar AI and BlueCart are not real
companies). Your real tracker lives at `references/applications.md`, which is **git-ignored** so your
real job-search data never gets committed (see the privacy note below). `track-application` creates
and maintains `applications.md` for you; copy this file to `applications.md` if you'd rather start by hand.

> ⚠️ **PRIVACY — read before you fork.** Once filled, `references/applications.md` holds PRIVATE
> job-search data: companies you applied to, recruiter names, and contact details. **Never commit that
> to a public repo.** Two safe options:
> 1. **Private standalone repo** — clone (don't fork; forks of a public repo stay public) into a private repository and keep your whole personalized copy there, or
> 2. **Git-ignore (default here)** — `references/applications.md` and `references/pattern-analysis-*.md`
>    are already in `.gitignore`, so your real tracker and generated reports stay local and untracked.
>
> This EXAMPLE file is safe to commit because every row is fictional.

**Purpose:** Machine-readable pipeline tracker. `CUSTOMIZATION_MEMORY.md` holds the *prose* learnings;
this file holds the *structured* rows that the `patterns` (rejection analysis) and `followup` (cadence)
skills query. The `track-application` skill maintains the real tracker for you — you rarely edit it by hand.

---

| Num | Company | Role | Type | Status | Applied | Responded | Interview | Source | Score | Outcome reason | Contact | Follow-ups | Last follow-up |
|-----|---------|------|------|--------|---------|-----------|-----------|--------|-------|----------------|---------|-----------|----------------|
| 1 | Northstar AI | Director of Product, AI Platform | AI | interview | 2026-06-10 | 2026-06-15 | 2026-06-28 | referral-warm | 4.2 | — | jane.recruiter@northstar.example | 1 | 2026-06-20 |
| 2 | BlueCart | Senior PM, Growth | Consumer | rejected | 2026-06-05 | — | — | cold-direct | 3.1 | Seniority mismatch — role scoped two levels below target | — | 0 | — |

---

## Field rules

- **Num** — sequential, never reused.
- **Type** — AI / Consumer / Enterprise / Fintech / Telco / Other.
- **Status** — one of: `evaluated`, `applied`, `screening`, `responded`, `interview`, `offer`, `rejected`, `discarded`, `skip`. Use these exact tokens — the `patterns` and `followup` skills classify on them.
  - `discarded` = went dead with no formal rejection (ghosted). `skip` = you self-filtered before applying.
- **Applied** — `YYYY-MM-DD` you submitted the application.
- **Responded** — `YYYY-MM-DD` the company/recruiter first responded with a real reply (not an auto-ack). `—` until it happens. Drives `followup` urgency, and marks that the row reached the screening stage even if it later goes terminal.
- **Interview** — `YYYY-MM-DD` of the first interview (scheduled or held). `—` until it happens. Drives `followup` momentum, and marks that the row reached the interview stage even if it later goes terminal.
- **Source** — `recruiter-outbound` / `referral-warm` / `referral-list` / `cold-direct`. A recruiter came to you; a person who knows you vouched for you; someone forwarded your name without vouching; or you applied cold. Keep the two referral kinds apart: a warm referral and a forwarded name may convert differently, and only separate values let your tracker show it.
- **Score** — the `evaluate` skill's score (X.X/5) if the role was evaluated; else `—`.
- **Outcome reason** — on `rejected`/`discarded`/`skip`, the stated or inferred reason (e.g. "geo-restricted", "stack mismatch", "seniority gap"). This is what `patterns` mines — never leave it blank on a negative outcome.
- **Follow-ups** — integer count of follow-ups you actually SENT (not drafted). Starts at `0`. `followup` treats `2+` as COLD and stops drafting.
- **Last follow-up** — `YYYY-MM-DD` of the most recent follow-up you sent, else `—`.
- **Honesty rule** — `—` means "not known," never a guess. Record only what actually happened; a drafted follow-up is not a sent follow-up.
