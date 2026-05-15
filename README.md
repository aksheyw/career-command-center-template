# Career Command Center — Template

A Claude Code plugin template for an AI-native job-search workflow. Resume customization, JD evaluation, interview prep, outreach, salary negotiation, and application tracking — all driven by Claude Code skills and a structured profile of your own background.

This is a **template**. Fork it, fill in your profile, and the skills auto-load with your data.

> **➡️ New here?** Start with [QUICKSTART.md](QUICKSTART.md) — get from clone to your first generated resume in ~10 minutes. Install via `/plugin marketplace add aksheyw/career-command-center-template` then `/plugin install career-cc@aksheyw-cct`, fill 3 sections of `YOUR_PROFILE.md` (marked ⭐ MINIMUM VIABLE), run `/career-cc:evaluate` and `/career-cc:apply`, and you're producing tailored applications.

---

## 👀 Preview the output (no install required)

See exactly what `/career-cc:apply` produces before installing anything. The [`examples/`](examples/) directory ships a complete fictional profile + target JD + generated resume PDF — same plugin, end-to-end:

| File | What it shows |
|------|---------------|
| [📄 **`jane-doe-resume.pdf`**](examples/jane-doe-resume.pdf) | 2-page ATS-compliant resume for fictional Director PM Jane Doe, tailored to a fictional Director-AI-Platform role |
| [📋 `example-jd.md`](examples/example-jd.md) | The fictional Northstar AI job description the resume was tailored against |
| [👤 `EXAMPLE_PROFILE.md`](examples/EXAMPLE_PROFILE.md) | Jane's fully-filled `YOUR_PROFILE.md` — the input the plugin used |
| [🌐 `jane-doe-resume.html`](examples/jane-doe-resume.html) | Same resume in HTML if you want to inspect the layout |

**All content is fictional.** Jane Doe, RevenueFlow Inc, MetricFlow, ScalePay, BlueCart — none are real. The example exists so you can evaluate output quality in 10 seconds without installing the plugin.

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
| `humanizer` | Auto-applied after every document generation to strip AI writing patterns. *(Authored by [@blader](https://github.com/blader/humanizer) under MIT — bundled here for convenience.)* |

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

## Verify install worked

After loading the plugin, in a fresh Claude Code session:

- Check `~/.claude/settings.json` — `enabledPlugins` should list this plugin (or, if you used `claude --plugin-dir`, the plugin shows in the session's plugin list at startup).
- Type `/` — autocomplete should show the 10 namespaced skills (e.g., `/career-cc:evaluate`, `/career-cc:apply`, `/career-cc:interview`, etc., based on the plugin name you set in `.claude-plugin/plugin.json`).
- The session-start hook should print a one-line confirmation that `YOUR_PROFILE.md` loaded.

Test without filling in your profile first: run `/career-cc:evaluate` on any JD — it works on JD alone, no profile required. If a 7-block analysis comes back with a GO / CAUTION / SKIP verdict, the plugin is wired correctly.

If something's off, see **Troubleshooting** below.

## Example output

Abbreviated `/career-cc:evaluate` output for a fictional Senior PM job description:

```
JD: Senior Product Manager, Growth — ExampleCo (SaaS, Series C)

Block 1: CV alignment (60% weight)
- Strong match: experience with B2B SaaS funnels, activation experiments
- Gap: no explicit revenue-attribution stack experience (HubSpot/Segment)
- Score: 7.5/10

Block 2: Compensation reality
- Public glassdoor range: ₹68-95 LPA fixed + ESOPs (Series C SaaS, India)
- Your target floor: ₹70 LPA — feasible
- Score: 8/10

Block 3: Likely interview process
- 5 rounds: recruiter → HM → case study → panel → leadership
- Estimated effort: 12-18 hours total prep
- Score: 6/10

Block 4: Story mapping
- Lead story: 47% activation lift via onboarding cohort experiments — strong match
- Weak slot: revenue-attribution narrative — needs reframing from analytics work

[Blocks 5-7 abbreviated]

Verdict: GO with conditions. Apply within 7 days.
Required prep before applying: rewrite the activation bullet to mirror their language,
prepare 1 weak-area honesty story for the attribution gap.
```

The skill never fabricates JD details, never invents salary ranges — it tells you what it knows, flags gaps, and gives a defensible verdict.

## Troubleshooting

- **`/career-cc:<skill>` doesn't autocomplete:** the plugin name in `.claude-plugin/plugin.json` is what gets prefixed. If you kept the default `career-command-center-template`, your skills are `/career-command-center-template:evaluate` (long but functional). Rename the plugin to something shorter (e.g., `career-cc`) before invoking.
- **Session-start hook isn't loading `YOUR_PROFILE.md`:** check `hooks/hooks.json` references the correct filename. If you renamed `YOUR_PROFILE.md`, update the hook's path.
- **Generated resume has placeholder text instead of your details:** the skills are designed to flag missing data rather than fabricate. Fill in the section the placeholder points to and regenerate.
- **`/career-cc:evaluate` works but `/career-cc:apply` doesn't:** `apply` requires `YOUR_PROFILE.md` to have at least the 3 ⭐ MINIMUM VIABLE sections filled. `evaluate` works on JD alone — that's why it's the first skill to test.
- **Plugin loaded but skills aren't namespaced:** confirm you installed it as a plugin (not by copying individual `SKILL.md` files to `~/.claude/skills/`). Plugin install gives you `/career-cc:apply`; loose-skill install gives bare `/apply` and bypasses the session-start hook.

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
├── QUICKSTART.md                        # 10-minute setup → first generated resume
├── references/                          # FILL THESE IN
│   ├── YOUR_PROFILE.md                  # ⭐ start here — 3 sections marked MINIMUM VIABLE
│   ├── CUSTOMIZATION_MEMORY.md
│   └── STRATEGIC_GAP_ASSESSMENT.md
├── skills/
│   ├── apply/SKILL.md
│   ├── evaluate/SKILL.md
│   ├── generic-letter/SKILL.md
│   ├── humanizer/SKILL.md               # bundled from blader/humanizer (MIT) — see Credits
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

## Credits

The `humanizer` skill bundled at `skills/humanizer/SKILL.md` is authored by [@blader](https://github.com/blader/humanizer) and is used here under the MIT license — all credit for that skill goes to them. For the newest version (29+ patterns with voice calibration), pull directly from [github.com/blader/humanizer](https://github.com/blader/humanizer).

The rest of the template is original work derived from a real director-PM job search workflow.

## License

MIT — see [LICENSE](LICENSE). The bundled `humanizer/SKILL.md` retains its original MIT terms; attribution above.

---

## Origin

This template was extracted from a real director-PM job search workflow. All personal data has been replaced with skeletons; the underlying methodology is preserved.

If you find this useful, share the result — or fork it and make it better.
