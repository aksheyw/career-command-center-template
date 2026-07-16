# Application Tracker — Template

**Purpose:** Machine-readable pipeline tracker. `CUSTOMIZATION_MEMORY.md` holds the *prose* learnings; this file holds the *structured* rows that the `patterns` (rejection analysis) and `followup` (cadence) skills query. The `track-application` skill maintains it for you — you rarely edit it by hand.

**How to fill in:** You don't, directly. Log each application with `track-application` and rows accumulate here. The two rows below are **fictional examples** (same fictional world as `examples/` — Northstar AI and BlueCart are not real companies). Delete them when your first real application lands.

---

| Num | Company | Role | Type | Status | Applied | Source | Score | Outcome reason | Contact | Last follow-up |
|-----|---------|------|------|--------|---------|--------|-------|----------------|---------|----------------|
| 1 | Northstar AI | Director of Product, AI Platform | AI | interview | {{YYYY-MM-DD}} | referral | 4.2 | — | jane.recruiter@northstar.example | {{YYYY-MM-DD}} |
| 2 | BlueCart | Senior PM, Growth | Consumer | rejected | {{YYYY-MM-DD}} | direct | 3.1 | Seniority mismatch — role scoped two levels below target | — | — |

---

## Field rules

- **Num** — sequential, never reused.
- **Type** — AI / Consumer / Enterprise / Fintech / Telco / Other.
- **Status** — one of: `evaluated`, `applied`, `screening`, `responded`, `interview`, `offer`, `rejected`, `discarded`, `skip`. Use these exact tokens — the `patterns` and `followup` skills classify on them.
  - `discarded` = went dead with no formal rejection (ghosted). `skip` = you self-filtered before applying.
- **Applied / Last follow-up** — `YYYY-MM-DD`.
- **Source** — `referral` / `direct` / `recruiter` (who initiated: a human vouched, you applied cold, or a recruiter came to you).
- **Score** — the `evaluate` skill's score (X.X/5) if the role was evaluated; else `—`.
- **Outcome reason** — on `rejected`/`discarded`/`skip`, the stated or inferred reason (e.g. "geo-restricted", "stack mismatch", "seniority gap"). This is what `patterns` mines — never leave it blank on a negative outcome.
- **Honesty rule** — `—` means "not known," never a guess. Record only what actually happened; a drafted follow-up is not a sent follow-up.
