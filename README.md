# Career Command Center Template

A Claude Code plugin template for an AI-native job-search workflow. Resume customization, JD evaluation, interview prep, outreach, salary negotiation, and application tracking, all driven by Claude Code skills and a structured profile of your own background.

This is a **template**. Clone it into your own private repo, fill in your profile, and the skills auto-load with your data. (For a job search, clone into a private repo rather than forking, because a fork of a public repo stays public; see **Privacy**.)

> **➡️ New here?** Start with [QUICKSTART.md](QUICKSTART.md): get from clone to your first generated resume in ~10 minutes. Install via `/plugin marketplace add aksheyw/career-command-center-template` then `/plugin install career-cc@aksheyw-cct`, copy `YOUR_PROFILE.example.md` to `YOUR_PROFILE.md` and fill its 3 sections marked ⭐ MINIMUM VIABLE, run `/career-cc:evaluate` and `/career-cc:apply`, and you're producing tailored applications. (For a job search, cloning into your own **private repo** is the recommended way to personalize, because a GitHub fork of a public repo stays public, so don't rely on forking; see **Privacy**.)

---

## 👀 Preview the output (no install required)

See exactly what `/career-cc:apply` produces before installing anything. The [`examples/`](examples/) directory ships a complete fictional profile + target JD + generated resume PDF (same plugin, end-to-end):

| File | What it shows |
|------|---------------|
| [📄 **`jane-doe-resume.pdf`**](examples/jane-doe-resume.pdf) | 2-page ATS-compliant resume for fictional Director PM Jane Doe, tailored to a fictional Director-AI-Platform role |
| [📋 `example-jd.md`](examples/example-jd.md) | The fictional Northstar AI job description the resume was tailored against |
| [👤 `EXAMPLE_PROFILE.md`](examples/EXAMPLE_PROFILE.md) | Jane's fully-filled `YOUR_PROFILE.md`: the input the plugin used |
| [🌐 `jane-doe-resume.html`](examples/jane-doe-resume.html) | Same resume in HTML if you want to inspect the layout |

**All content is fictional.** Jane Doe, RevenueFlow Inc, MetricFlow, ScalePay, BlueCart: none are real. The example exists so you can evaluate output quality in 10 seconds without installing the plugin.

---

## What this plugin does

Once personalized, the plugin gives you twelve skills for the full job-search loop (ten you invoke by name, plus `resume-customizer` and `humanizer` which run automatically):

| Skill | What it does |
|-------|--------------|
| `apply` | Paste a JD. Get JD analysis + tailored resume + cover letter + interview quick-hits |
| `evaluate` | 7-block JD assessment with go/no-go score before you invest in a full application |
| `interview` | Full interview prep pack for a named company: 2-min pitch, STAR stories, likely questions, 90-day plan, salary prep |
| `outreach` | The right outreach template for a contact (cold LinkedIn, InMail, recruiter email, warm referral), personalized |
| `generic-letter` | Network forwarding cover letter for warm intros and alumni networks |
| `salary-negotiate` | Compensation prep: target range by company type, scripts, counter-offer handling |
| `track-application` | Log applications to prose memory + a structured tracker; see pipeline conversion rates |
| `followup` | Cadence tracker: flags overdue/urgent applications and drafts the second-touch message most candidates never send. *(Adapted from [santifer/career-ops](https://github.com/santifer/career-ops) under MIT.)* |
| `patterns` | Rejection-pattern analysis: score thresholds, converting archetypes, blocker buckets, concrete targeting changes. *(Adapted from [santifer/career-ops](https://github.com/santifer/career-ops) under MIT.)* |
| `update-memory` | Capture what worked (or didn't) per application so future ones get smarter |
| `resume-customizer` | Auto-loads on any resume or cover letter request (the core engine) |
| `humanizer` | Auto-applied after every document generation to strip AI writing patterns. *(Authored by [@blader](https://github.com/blader/humanizer) under MIT, bundled here for convenience.)* |

---

## What you customize

The plugin ships each personal-data file as a committed **`*.example.md` placeholder skeleton**. You **copy it to the real filename** (which is **git-ignored**) and fill the copy, and every skill then picks up your data via the `${CLAUDE_PLUGIN_ROOT}` path variable. Because the real filenames are git-ignored, following this path in a public repo can never commit your real data. (In your own private repo you can version them freely; see **Privacy** below.)

> **The safest path is your own PRIVATE repo, not a fork.** This is a job-search template; your filled copy holds private data. A GitHub fork of a public repo is always public, so instead clone this template into a brand-new **private** repo (see **Privacy** for the exact commands), and everything below is moot; fill and version freely. The `*.example.md` + git-ignore machinery is the belt-and-suspenders for anyone who keeps their repo public.

### Files to fill in (8 personal-data files: copy the `.example.md`, fill the `.md`)

| Copy this (committed) → to this (git-ignored, you fill) | What goes here |
|------|----------------|
| `references/YOUR_PROFILE.example.md` → `references/YOUR_PROFILE.md` | Your background, current role, achievements with verified metrics, contact info, target compensation, references |
| `references/CUSTOMIZATION_MEMORY.example.md` → `references/CUSTOMIZATION_MEMORY.md` | Application learning log: fills as you log outcomes |
| `references/applications.example.md` → `references/applications.md` | Structured pipeline tracker: auto-created/maintained by `track-application` (you rarely copy this by hand), queried by `patterns` and `followup` |
| `references/STRATEGIC_GAP_ASSESSMENT.example.md` → `references/STRATEGIC_GAP_ASSESSMENT.md` | Your honest assessment of positioning gaps to address |
| `skills/resume-customizer/references/star-stories.example.md` → `.../star-stories.md` | Your STAR stories (success + failure) with selection guide |
| `skills/resume-customizer/references/detailed-context.example.md` → `.../detailed-context.md` | Full work history, certifications, side projects, strengths |
| `skills/resume-customizer/references/story-bank-index.example.md` → `.../story-bank-index.md` | Cross-index of your STAR stories by company type and question |
| `skills/resume-customizer/references/interview-prep.example.md` → `.../interview-prep.md` | Your filled interview prep: 2-min pitch, STAR selection, company angles (generic RCA/guesstimate/case-study frameworks stay as-is) |

Plus one binary you drop in (not a skeleton): `references/generic-resume.docx`, which is your maintained generic resume and the canonical file the resume skills copy from (also git-ignored). See **Setup** step 4 and `resume-customizer` STEP 0.

### Files you usually don't touch

Everything else is methodology (the rules, frameworks, templates, language guidance) that works across users.

---

## Privacy: don't publish your own job-search data

Your filled files hold private job-search data: contact details and compensation (`YOUR_PROFILE.md`, `detailed-context.md`), the companies and recruiters in your pipeline (`applications.md`, `CUSTOMIZATION_MEMORY.md`), your positioning gaps and network (`STRATEGIC_GAP_ASSESSMENT.md`), your real stories and filled interview prep (`star-stories.md`, `story-bank-index.md`, `interview-prep.md`), your maintained resume (`generic-resume.docx`), and every tailored resume and cover letter you generate (in `output/`). None of that should reach a public repo.

### 1. Recommended: personalize in a PRIVATE standalone repo (NOT a fork)

**A GitHub fork of a public repo is always public: you cannot make a fork private.** So the safe way to personalize is to clone this template into a brand-new **private repository of your own**, not to fork it:

```bash
git clone https://github.com/aksheyw/career-command-center-template.git my-job-search
cd my-job-search
git remote remove origin
# create a new PRIVATE repo and push into it (GitHub CLI shown; or make one in the UI and add it as origin):
gh repo create my-job-search --private --source=. --remote=origin
git push -u origin main
```

Now your repo is private and disconnected from the public template, so you can fill every file in place and version it freely, and nothing is ever public. If you go this route the git-ignore machinery below is just a backstop. (You can still pull template updates later: `git remote add template https://github.com/aksheyw/career-command-center-template.git`, then `git pull template main`.)

### 2. If your repo must stay public: the `.example.md` + git-ignore machinery (default here)

The template is built so the documented happy path **cannot** commit your real data even in a public repo:

- Every personal-data file ships as a committed **`*.example.md` placeholder skeleton**. You **copy it to the real filename** and fill the copy. The real filenames (`references/YOUR_PROFILE.md`, `.../star-stories.md`, `references/generic-resume.docx`, etc.) are all listed in `.gitignore`, so git never tracks them, which means filling and committing normally leaves your real data untouched on disk and out of every commit.
- `references/applications.md` is created for you by `track-application` from `applications.example.md`; it (and generated `references/pattern-analysis-*.md` reports) are git-ignored too.
- **Generated resumes and cover letters are git-ignored by design.** `apply` writes every tailored resume and cover letter into `output/`, which is git-ignored (only its `README.md` is tracked); the generated-document filename patterns (`*_Resume_*.docx`, `*_CoverLetter_*.docx`, and their `.pdf` siblings) are ignored as a backstop too, so a `git add .` can never stage a generated application even if you save it elsewhere.
- The `.local.md` suffix is also git-ignored, for any extra personal copy you want to keep out of git.

### 3. If you ALREADY committed or pushed real data

Git-ignore only stops files that were **never** tracked. If a real-named file (a filled `YOUR_PROFILE.md`, a generated resume in `output/`, etc.) is already in your repo's history, you have to actively remove it, and if it was pushed to a public remote, treat it as exposed:

- **Committed locally, but never pushed yet?** Untracking alone is NOT enough, because the file still lives in the earlier commit, so an ordinary `git push` later would publish it. You MUST purge it from history BEFORE your first push: run the history purge below (`git filter-repo --invert-paths --path <file>` or BFG), then copy from the `.example.md` and refill so it stays local going forward.
- **Already pushed to a public remote?** The data was publicly visible, so **treat it as compromised** (assume it was crawled, cached, or forked while public). Then purge it from history: [`git filter-repo`](https://github.com/newren/git-filter-repo) (`git filter-repo --path references/YOUR_PROFILE.md --invert-paths`) or [BFG](https://rtyley.github.io/bfg-repo-cleaner/) strips the file from every commit, after which you force-push. Often the simplest, safest option is to **delete the public repo entirely and recreate a private one** from a clean clone (section 1).
- A history rewrite or repo deletion does **not** un-expose what was already seen while the data was public. That is why section 1 (private from the start) is the recommendation: cleanup is damage control, not prevention.

As shipped, every committed file is safe (placeholders and fictional rows only). Decide private-standalone-repo vs public-repo **before** your first real entry, because it is far cheaper than cleaning up after.

---

## Setup

1. **Clone** this template, ideally into your own **private repo** (see **Privacy** above; forking a public repo keeps it public, so clone-into-private instead), under your Claude Code plugins folder, or wherever your harness loads plugins from.
2. **Rename the plugin** in `.claude-plugin/plugin.json` (`name`, `version`, `description`) to be yours. Do NOT add an `author` field with your real identity unless you intend to PUBLISH your fork publicly, because `plugin.json` is a tracked file, so anything you put there becomes public the moment the repo is pushed. For a private job-search setup (the normal case), leave `author` out entirely; it is optional publisher metadata, not required for the plugin to work.
3. **Copy each `*.example.md` to its real filename, then fill the copy.** Every personal-data file ships as a committed placeholder skeleton; you fill the git-ignored real file, not the `.example.md`. At minimum, start with your profile:
   ```bash
   cp references/YOUR_PROFILE.example.md references/YOUR_PROFILE.md
   # then copy the rest as you need them (see the "Files to fill in" table above)
   ```
   (`applications.md` is the exception: you don't copy it by hand; `track-application` creates it from `applications.example.md`.)
4. **Drop in your canonical resume.** Once you maintain a generic resume, save it as `references/generic-resume.docx` (git-ignored). The `resume-customizer` / `apply` skills copy from this fixed path and apply targeted edits, and they never rebuild from templates once it exists. No canonical yet? The first resume you generate and approve is saved there and becomes the canonical (see `resume-customizer` STEP 0).
5. **Update `hooks/hooks.json`** only if you renamed `YOUR_PROFILE.md` to something else (this file is auto-loaded at session start; it prints a copy-me hint until the real file exists). ⚠️ **If you rename it, the new name is NOT automatically git-ignored**, because `.gitignore` protects the exact path `references/YOUR_PROFILE.md` only. Either give the new file a `.local.md` suffix (e.g. `MY_PROFILE.local.md`, since the `*.local.md` pattern is already ignored), or add your custom path to `.gitignore` in the same step. A renamed profile without one of these gets committed like any other file.
6. **Try a skill.** Paste any JD into `apply` and watch the workflow run end-to-end.

No external services. No API keys. Works entirely from your local files.

---

## Verify install worked

After loading the plugin, in a fresh Claude Code session:

- Check `~/.claude/settings.json`: `enabledPlugins` should list this plugin (or, if you used `claude --plugin-dir`, the plugin shows in the session's plugin list at startup).
- Type `/`, and autocomplete should show the 12 namespaced skills (e.g., `/career-cc:evaluate`, `/career-cc:apply`, `/career-cc:interview`, etc., based on the plugin name you set in `.claude-plugin/plugin.json`).
- The session-start hook should print a one-line confirmation that `YOUR_PROFILE.md` loaded.

Test without filling in your profile first: run `/career-cc:evaluate` on any JD (it works on JD alone, no profile required). If a 7-block analysis comes back with a GO / CAUTION / SKIP verdict, the plugin is wired correctly.

If something's off, see **Troubleshooting** below.

## Example output

Abbreviated `/career-cc:evaluate` output for a fictional Senior PM job description:

```
JD: Senior Product Manager, Growth, ExampleCo (SaaS, Series C)

Block 1: CV alignment (60% weight)
- Strong match: experience with B2B SaaS funnels, activation experiments
- Gap: no explicit revenue-attribution stack experience (HubSpot/Segment)
- Score: 7.5/10

Block 2: Compensation reality
- Public glassdoor range: ₹68-95 LPA fixed + ESOPs (Series C SaaS, India)
- Your target floor: ₹70 LPA (feasible)
- Score: 8/10

Block 3: Likely interview process
- 5 rounds: recruiter → HM → case study → panel → leadership
- Estimated effort: 12-18 hours total prep
- Score: 6/10

Block 4: Story mapping
- Lead story: 47% activation lift via onboarding cohort experiments (strong match)
- Weak slot: revenue-attribution narrative (needs reframing from analytics work)

[Blocks 5-7 abbreviated]

Verdict: GO with conditions. Apply within 7 days.
Required prep before applying: rewrite the activation bullet to mirror their language,
prepare 1 weak-area honesty story for the attribution gap.
```

The skill never fabricates JD details and never invents salary ranges. Instead it tells you what it knows, flags gaps, and gives a defensible verdict.

## Troubleshooting

- **`/career-cc:<skill>` doesn't autocomplete:** the plugin name in `.claude-plugin/plugin.json` is what gets prefixed. If you kept the default `career-command-center-template`, your skills are `/career-command-center-template:evaluate` (long but functional). Rename the plugin to something shorter (e.g., `career-cc`) before invoking.
- **Session-start hook isn't loading `YOUR_PROFILE.md`:** check `hooks/hooks.json` references the correct filename. If you renamed `YOUR_PROFILE.md`, update the hook's path, and make sure the new name is still git-ignored: use a `.local.md` suffix (already covered by `*.local.md` in `.gitignore`) or add the custom path to `.gitignore`, because only the exact path `references/YOUR_PROFILE.md` is ignored by default.
- **Generated resume has placeholder text instead of your details:** the skills are designed to flag missing data rather than fabricate. Fill in the section the placeholder points to and regenerate.
- **`/career-cc:evaluate` works but `/career-cc:apply` doesn't:** `apply` requires `YOUR_PROFILE.md` to have at least the 3 ⭐ MINIMUM VIABLE sections filled. `evaluate` works on JD alone, which is why it's the first skill to test.
- **Plugin loaded but skills aren't namespaced:** confirm you installed it as a plugin (not by copying individual `SKILL.md` files to `~/.claude/skills/`). Plugin install gives you `/career-cc:apply`; loose-skill install gives bare `/apply` and bypasses the session-start hook.

---

## Why this exists

Job search done well is iterative work over months. Each application teaches you something: which hook a recruiter responded to, which STAR story landed, what comp range a company actually has. Most people lose that compounding knowledge between applications.

This plugin's value isn't the resume templates but the **memory loop**. `update-memory` and `track-application` make every future application smarter than the last. `patterns` turns the accumulated tracker into targeting changes (which score floor, which archetypes, which blockers), and `followup` catches the second touch most candidates never send. After 10 applications you have your own personal model of what works for which company type.

The methodology (STAR weaving, narrative-arc cover letters, ATS compliance rules, per-claim defensibility audits, humanizer pass) is preserved from a real director-PM job search. You bring your own substance.

---

## Plugin structure

```
career-command-center-template/
├── .claude-plugin/
│   └── plugin.json
├── hooks/
│   └── hooks.json                       # auto-loads YOUR_PROFILE.md at session start
├── CHANGELOG.md
├── QUICKSTART.md                        # 10-minute setup → first generated resume
├── output/                              # generated resumes + cover letters land here, git-ignored (only README.md tracked)
│   └── README.md
├── references/                          # copy each .example.md → real name, fill the copy
│   ├── YOUR_PROFILE.example.md          # ⭐ committed skeleton: copy to YOUR_PROFILE.md, fill 3 MINIMUM VIABLE sections
│   ├── CUSTOMIZATION_MEMORY.example.md  # committed skeleton → CUSTOMIZATION_MEMORY.md (git-ignored)
│   ├── STRATEGIC_GAP_ASSESSMENT.example.md  # committed skeleton → STRATEGIC_GAP_ASSESSMENT.md (git-ignored)
│   └── applications.example.md          # committed fictional reference; track-application makes applications.md (git-ignored)
│                                        # (the real YOUR_PROFILE.md, generic-resume.docx, …  are all git-ignored)
├── skills/
│   ├── apply/SKILL.md
│   ├── evaluate/SKILL.md
│   ├── followup/SKILL.md                # follow-up cadence tracker + second-touch drafts
│   ├── generic-letter/SKILL.md
│   ├── humanizer/SKILL.md               # bundled from blader/humanizer (MIT); see Credits
│   ├── interview/SKILL.md
│   ├── outreach/SKILL.md
│   ├── patterns/SKILL.md                # rejection-pattern / conversion analysis
│   ├── resume-customizer/
│   │   ├── SKILL.md                     # core engine
│   │   └── references/
│   │       ├── career-tools.md           # outreach + negotiation + 90-day methodology (don't fill; your comp/refs live in YOUR_PROFILE.md)
│   │       ├── detailed-context.example.md   # committed skeleton → detailed-context.md (git-ignored)
│   │       ├── evaluation-framework.md   # 7-block JD scoring (methodology)
│   │       ├── github_in_resume_pattern.md
│   │       ├── interview-prep.example.md     # committed skeleton → interview-prep.md (git-ignored); generic frameworks stay as-is
│   │       ├── referral_email_pattern.md
│   │       ├── star-stories.example.md       # committed skeleton → star-stories.md (git-ignored)
│   │       └── story-bank-index.example.md   # committed skeleton → story-bank-index.md (git-ignored)
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
2. Only verified metrics from your profile go in (no fabricated numbers)
3. Humanizer pass runs on every generated document
4. Resume is exactly 2 pages
5. Bullets 40-55 words for senior roles, 12-20 for early career
6. ATS compliance: INR not currency symbol, "to" not arrow, standard hyphens only
7. STAR structure is woven into bullets, never labeled with `(S) (T) (A) (R)` prefixes
8. Per-claim defensibility audit before declaring any document "final"
9. Once you maintain a canonical generic resume, tailored resumes start from it (copy + targeted edits + diff to surface drops + render to confirm layout), never rebuilt from templates. On a FORMAT/layout/voice conflict the generic wins; on a contested factual metric, re-derive from the primary source instead of silently picking either

These rules are codified in `skills/resume-customizer/SKILL.md` and apply to every generation.

---

## Customizing the methodology

The default templates assume a director / principal PM job search in India. To use this for a different role or geography:

> ⚠️ **Privacy note before you personalize:** every file named below (except `YOUR_PROFILE.md`) is a TRACKED methodology file. Editing it to match YOUR geography, role archetypes, or seniority writes your real job-search targets into files that become public if this repo is public. Do methodology personalization only in a **private** clone (see **Privacy** above), or leave the tracked methodology generic and keep your specifics in the git-ignored `YOUR_PROFILE.md`, which the skills always read first.

- **Different geography:** edit currency formatting + phone format in `skills/resume-customizer/SKILL.md` ATS rules; set your actual target in `references/YOUR_PROFILE.md` (git-ignored), and re-theme the company-type calibration buckets in `skills/resume-customizer/references/career-tools.md` if needed
- **Different role family:** rewrite the company-type strategies in `SKILL.md` (`AI`, `Consumer Scale`, `Enterprise/B2B`, `Fintech`, `Telco`) to match the role archetypes you target
- **Different seniority:** adjust bullet length norms (40-55 words is calibrated for senior PM)

The 7-block evaluation framework, narrative-arc cover letter, humanizer skill, and STAR weaving rules generalize across roles.

---

## Companion repos

Part of my Claude Code config series:

- [`claude-code-deep-review`](https://github.com/aksheyw/claude-code-deep-review): 14-lens iterative review skill
- [`claude-code-pm-agents`](https://github.com/aksheyw/claude-code-pm-agents): 7 product-builder subagents (PM, growth, brand, ASO, SEO, YouTube, comms triage)
- [`claude-code-rules`](https://github.com/aksheyw/claude-code-rules): opinionated global rules (honesty / earned-confidence, TDD, branching)
- [`claude-code-learned-skills`](https://github.com/aksheyw/claude-code-learned-skills): 12 skills auto-extracted from real debugging and research sessions (Docker/SSH/VPS, ML pipelines, prompting guides, quality tooling, a project wiki)

## Credits

The `humanizer` skill bundled at `skills/humanizer/SKILL.md` is authored by [@blader](https://github.com/blader/humanizer) and is used here under the MIT license, and all credit for that skill goes to them. For the newest version (29+ patterns with voice calibration), pull directly from [github.com/blader/humanizer](https://github.com/blader/humanizer).

The cadence and analysis models in the `followup` and `patterns` skills are adapted from the corresponding modes of [santifer/career-ops](https://github.com/santifer/career-ops), used here under the MIT license, and rebuilt to run on this plugin's own tracker schema. Credit for those two models goes to that project.

The rest of the template is original work derived from a real director-PM job search workflow.

## License

MIT (see [LICENSE](LICENSE)). Two components are third-party MIT and stay under their original terms, with attribution in Credits above: the bundled `humanizer/SKILL.md` ([@blader/humanizer](https://github.com/blader/humanizer)) and the cadence/analysis models adapted into the `followup` and `patterns` skills ([santifer/career-ops](https://github.com/santifer/career-ops)). MIT-into-MIT adaptation is clean; this repo's MIT license covers the combined work.

---

## Origin

This template was extracted from a real director-PM job search workflow. All personal data has been replaced with skeletons; the underlying methodology is preserved.

If you find this useful, share the result, or fork it and make it better.
