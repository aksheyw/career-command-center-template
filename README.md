# Career Command Center — Template

A Claude Code plugin template for an AI-native job-search workflow. Resume customization, JD evaluation, interview prep, outreach, salary negotiation, and application tracking — all driven by Claude Code skills and a structured profile of your own background.

This is a **template**. Fork it, fill in your profile, and the skills auto-load with your data.

---

## What this plugin does

Once personalized, the plugin gives you eight commands for the full job-search loop:

| Skill | What it does |
|-------|--------------|
| `apply` | Paste a JD. Get JD analysis + tailored resume + cover letter + interview quick-hits |
| `evaluate` | 7-block JD assessment with go/no-go score before you invest in a full application |
| `interview` | Full interview prep pack for a named company: 2-min pitch, STAR stories, likely questions, 90-day plan, salary prep |
| `outreach` | The right outreach template for a contact (cold LinkedIn, InMail, recruiter email, warm referral) — personalized |
| `generic-letter` | Network forwarding cover letter for warm intros and alumni networks |
| `salary-negotiate` | Compensation prep — target range by company type, scripts, counter-offer handling |
| `track-application` | Log applications, see your pipeline conversion rates, surface what's working |
| `update-memory` | Capture what worked (or didn't) per application so future ones get smarter |
| `resume-customizer` | Auto-loads on any resume or cover letter request — the core engine |
| `humanizer` | Auto-applied after every document generation to strip AI writing patterns |

---

## What you customize

The plugin ships with **skeleton files** in `references/` and `skills/resume-customizer/references/`. Fill these in once with your own background, and every skill picks up your data via the `${CLAUDE_PLUGIN_ROOT}` path variable.

### Files to fill in (5 personal-data files)

| File | What goes here |
|------|----------------|
| `references/YOUR_PROFILE.md` | Your background, current role, achievements with verified metrics, contact info, target compensation |
| `references/CUSTOMIZATION_MEMORY.md` | Application learning log — fills as you log outcomes |
| `references/STRATEGIC_GAP_ASSESSMENT.md` | Your honest assessment of positioning gaps to address |
| `skills/resume-customizer/references/star-stories.md` | Your STAR stories (success + failure) with selection guide |
| `skills/resume-customizer/references/detailed-context.md` | Full work history, certifications, side projects, strengths |

### Files you usually don't touch

Everything else is methodology — the rules, frameworks, templates, language guidance — that works across users.

---

## Setup

1. **Fork or clone** this template into your Claude Code plugins folder, or wherever your harness loads plugins from.
2. **Rename the plugin** in `.claude-plugin/plugin.json` (`name`, `version`, `description`, `author`) to be yours.
3. **Fill in your data** in the 5 files listed above. Each ships as a skeleton with placeholders and section headings.
4. **Update `hooks/hooks.json`** if you renamed `YOUR_PROFILE.md` to something else (this file is auto-loaded at session start).
5. **Try a skill.** Paste any JD into `apply` and watch the workflow run end-to-end.

No external services. No API keys. Works entirely from your local files.

---

## Why this exists

Job search done well is iterative work over months. Each application teaches you something: which hook a recruiter responded to, which STAR story landed, what comp range a company actually has. Most people lose that compounding knowledge between applications.

This plugin's value isn't the resume templates — it's the **memory loop**. `update-memory` and `track-application` make every future application smarter than the last. After 10 applications you have your own personal model of what works for which company type.

The methodology (STAR weaving, narrative-arc cover letters, ATS compliance rules, per-claim defensibility audits, humanizer pass) is preserved from a real director-PM job search. You bring your own substance.

---

## Plugin structure

```
career-command-center-template/
├── .claude-plugin/
│   └── plugin.json
├── hooks/
│   └── hooks.json                       # auto-loads YOUR_PROFILE.md at session start
├── references/                          # FILL THESE IN
│   ├── YOUR_PROFILE.md
│   ├── CUSTOMIZATION_MEMORY.md
│   └── STRATEGIC_GAP_ASSESSMENT.md
├── skills/
│   ├── apply/SKILL.md
│   ├── evaluate/SKILL.md
│   ├── generic-letter/SKILL.md
│   ├── humanizer/SKILL.md               # reusable as-is
│   ├── interview/SKILL.md
│   ├── outreach/SKILL.md
│   ├── resume-customizer/
│   │   ├── SKILL.md                     # core engine
│   │   └── references/
│   │       ├── career-tools.md           # templates with placeholders
│   │       ├── detailed-context.md       # FILL THIS IN
│   │       ├── evaluation-framework.md   # 7-block JD scoring
│   │       ├── github_in_resume_pattern.md
│   │       ├── interview-prep.md         # RCA, guesstimate, case study frameworks
│   │       ├── referral_email_pattern.md
│   │       ├── star-stories.md           # FILL THIS IN
│   │       └── story-bank-index.md       # FILL THIS IN
│   ├── salary-negotiate/SKILL.md
│   ├── track-application/SKILL.md
│   └── update-memory/SKILL.md
├── LICENSE
└── README.md
```

---

## Critical rules (preserved from the original)

The plugin enforces these every time it generates a document:

1. Pre-generation checklist completes before any resume or cover letter
2. Only verified metrics from your profile go in — no fabricated numbers
3. Humanizer pass runs on every generated document
4. Resume is exactly 2 pages
5. Bullets max ~55 words for senior roles, ~20 for early career
6. ATS compliance: INR not currency symbol, "to" not arrow, standard hyphens only
7. STAR structure is woven into bullets — never labeled with `(S) (T) (A) (R)` prefixes
8. Per-claim defensibility audit before declaring any document "final"

These rules are codified in `skills/resume-customizer/SKILL.md` and apply to every generation.

---

## Customizing the methodology

The default templates assume a director / principal PM job search in India. To use this for a different role or geography:

- **Different geography:** edit currency formatting + phone format in `skills/resume-customizer/SKILL.md` ATS rules; update target compensation table in `skills/resume-customizer/references/career-tools.md`
- **Different role family:** rewrite the company-type strategies in `SKILL.md` (`AI`, `Consumer Scale`, `Enterprise/B2B`, `Fintech`, `Telco`) to match the role archetypes you target
- **Different seniority:** adjust bullet length norms (40-55 words is calibrated for senior PM)

The 7-block evaluation framework, narrative-arc cover letter, humanizer skill, and STAR weaving rules generalize across roles.

---

## Companion repos

Part of my Claude Code config series:

- [`claude-code-deep-review`](https://github.com/aksheyw/claude-code-deep-review) — 14-lens iterative review skill
- [`claude-code-pm-agents`](https://github.com/aksheyw/claude-code-pm-agents) — 7 product-builder subagents (PM, growth, brand, ASO, SEO, YouTube, comms triage)
- [`claude-code-rules`](https://github.com/aksheyw/claude-code-rules) — opinionated global rules (honesty / earned-confidence, TDD, branching)
- [`claude-code-learned-skills`](https://github.com/aksheyw/claude-code-learned-skills) — 3 Docker / SSH / VPS skills auto-extracted from real debugging sessions

## License

MIT — see [LICENSE](LICENSE).

---

## Origin

This template was extracted from a real director-PM job search workflow. All personal data has been replaced with skeletons; the underlying methodology is preserved.

If you find this useful, share the result — or fork it and make it better.
