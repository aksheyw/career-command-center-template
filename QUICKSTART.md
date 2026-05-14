# Quickstart

Get from clone to your first generated resume in ~10 minutes.

## What you need

- Claude Code installed ([install guide](https://docs.claude.com/claude-code))
- A real job description (any role you might apply to)

---

## 1. Install the plugin

This is a Claude Code plugin in the standard format (`.claude-plugin/plugin.json` + `skills/` + `hooks/`). Pick the install path that matches how you want to use it:

### Option A — Marketplace install (recommended, permanent)

The repo ships with a `.claude-plugin/marketplace.json` so it can be installed directly from GitHub. Inside a Claude Code session:

```
/plugin marketplace add aksheyw/career-command-center-template
/plugin install career-cc@aksheyw-cct
```

The marketplace name is `aksheyw-cct` and the plugin name is `career-cc`. Once installed, skills become `/career-cc:evaluate`, `/career-cc:apply`, etc. (See `.claude-plugin/marketplace.json` for the source of these names.)

### Option B — Local dev install (session-only, for forks)

For iterating on a fork before publishing it:

```bash
git clone https://github.com/aksheyw/career-command-center-template.git
cd career-command-center-template
claude --plugin-dir ./
```

This loads the plugin for the current session only. Re-run each time. Useful while customizing — once you have a working fork, set up your own marketplace using the same `marketplace.json` pattern (point `source` to your repo) and switch to Option A.

### Either way

Once installed, the plugin's session-start hook auto-loads your `references/YOUR_PROFILE.md` so every skill sees your background as canonical context.

## 2. Confirm the install — run `/career-cc:evaluate` (no profile required)

The `evaluate` skill works on a JD alone. Test it first to confirm wiring.

In Claude Code, paste a job description and ask:

> Run `/career-cc:evaluate` on this JD: [paste here]

You'll get back a 7-block analysis (CV match, compensation research, story mapping, legitimacy, etc.) with a **GO / CAUTION / SKIP** verdict. 2-3 minutes. No profile needed yet.

If this works, the plugin is wired correctly.

## 3. Minimum viable profile (3 minutes)

Open `references/YOUR_PROFILE.md`. The full template has many sections — for your first real application you only need three.

Fill in the sections marked with **`⭐ MINIMUM VIABLE`** in `YOUR_PROFILE.md`:

1. **Contact info** — name, email, phone, LinkedIn, location, optional portfolio
2. **Current role & responsibilities** — title, company, scope, what you actually own
3. **Verified achievements** — 3-5 specific metrics from your current or past roles, each with the verbatim phrasing you'd defend in an interview

Leave the rest as placeholders for now. You'll fill them in as your applications create real data (STAR stories surface during interview prep, regulatory expertise gets added per JD, etc.).

## 4. Generate your first resume + cover letter

Now run:

> Run `/career-cc:apply` on this JD: [paste the same JD from step 2]

You'll get:

- JD analysis with fit score
- Tailored resume (`.docx`) — 2 pages, Calibri, ATS-compliant, 35-word bullets, mirrored JD keywords
- Cover letter (`.docx`) — 250-300 words, narrative arc, no passive language
- 3 interview-prep "quick hits" (suggested STAR stories + likely questions)

Both documents are auto-passed through the bundled humanizer skill before output.

## 5. Track it (one line)

> Run `/career-cc:track-application` for [company] [role] applied

This logs the application to `references/CUSTOMIZATION_MEMORY.md`. After 3-5 applications, the memory file starts surfacing patterns ("which hooks got screens", "which company types respond"). That compounding loop is where the plugin's long-term value lives — it gets smarter per application.

---

## Where to go next

Once your profile has substance and you have a few applications logged:

| Skill | Use it for |
|-------|-----------|
| `/career-cc:interview [company]` | Full prep pack: 2-min pitch + 4 STAR stories + likely questions + 90-day plan + salary prep |
| `/career-cc:outreach [target]` | Cold or warm outreach messages, personalized by template |
| `/career-cc:salary-negotiate [company]` | Negotiation prep with scripts, counter-offer handling, notice-period strategy |
| `/career-cc:generic-letter` | Network forwarding cover letter for warm intros and alumni networks |
| `/career-cc:update-memory` | After each application outcome — what worked, what didn't, what to change |

## Filling in the rest of `YOUR_PROFILE.md`

The full profile pays off when:

- You have 5+ verified achievements across multiple roles → resume bullets get richer
- You have 15-25 STAR stories in `skills/resume-customizer/references/star-stories.md` → the `interview` skill becomes meaningful
- You've logged 3-5 application outcomes → `update-memory` finds patterns

Build these out over a few weeks as you apply, not in one sitting. The `update-memory` and `track-application` skills are designed to fill these files for you as outcomes come in.

## Strategic gap assessment (optional but useful)

Once your profile is substantive, fill in `references/STRATEGIC_GAP_ASSESSMENT.md`. This is the "what's broken about my recruiter visibility beyond the resume" worksheet — covers LinkedIn headline, thought-leadership gaps, warm-intro mapping, etc. The resume skill handles part 5 of a 5-part job-search strategy; this worksheet helps you identify parts 1-4.

## Troubleshooting

**"My skills aren't activating."** Check the `description` in each `SKILL.md` frontmatter — Claude Code matches skills by description against your conversation context. If a skill isn't firing, the description may not be specific enough.

**"The hook isn't loading my profile at session start."** Check that `hooks/hooks.json` references the correct filename. If you renamed `YOUR_PROFILE.md` to something else, update the hook's `command` path.

**"Generated resume has fields I haven't filled in."** The skills are designed to ask before fabricating. If you see placeholder text in the output, that's the skill flagging a gap rather than inventing data. Fill in the missing profile section and regenerate.

---

## A note on this template's philosophy

The methodology (resume rules, ATS compliance, STAR weaving, narrative-arc cover letters, per-claim defensibility audit, humanizer pass) is preserved verbatim from a real director-PM job search. What you bring is your substance.

The plugin **enforces honesty over impressiveness** — verified metrics only, no scope overclaim, no fabricated numbers. That's the part that's hard to copy from any other resume tool.
