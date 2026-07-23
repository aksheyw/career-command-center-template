<div align="center">

# 📄 Career Command Center Template: an AI-native job search

### Twelve skills, built so the tenth application starts from what the first nine taught you.

![requires](https://img.shields.io/badge/requires-Claude%20Code-D97757)
![skills](https://img.shields.io/badge/skills-12-0E9384)
![setup](https://img.shields.io/badge/setup-no%20API%20keys-1B2A4A)
![license](https://img.shields.io/badge/license-MIT-green)

</div>

---

Claude Code is Anthropic's AI coding assistant. It runs in your terminal, reads the files in your
project, and can change them for you. A **skill** is a markdown file of instructions it follows when a
matching job comes up, and a **plugin** bundles skills so they install in one step.

This one runs a job search: fill in your profile once, paste a job description, and get back a tailored
resume, a cover letter and interview prep.

<img src="docs/the-memory-loop.svg" width="100%"
     alt="Why the tenth application is better than the first. Four of the twelve skills run on every job you apply to, and the fourth one is why the loop compounds. First, evaluate: is this job worth a day of your time? Second, apply: the tailored resume, letter and prep. Third, track-application: where it went, and what came back. Fourth, update-memory: what worked, while you still remember. That fourth step writes into a store of what the loop remembers, holding which opening line a recruiter actually answered, which story landed in the room, where your applications keep stalling, and which kind of role keeps rejecting you. That store then feeds the next application, so the cycle returns to evaluate. Once installed the four are invoked as slash career-cc colon evaluate, slash career-cc colon apply, and so on.">

## What the twelve skills cover

The whole loop, not just the writing: score a job description before you spend a day on it, generate
the tailored resume and cover letter, prep the interview and the salary conversation, write the
outreach, log the outcome, and turn the accumulated tracker into changes to who you target next.

Ten you invoke by name: `evaluate`, `apply`, `interview`, `outreach`, `generic-letter`,
`salary-negotiate`, `track-application`, `followup`, `patterns` and `update-memory`. The other two run
on their own whenever a document is generated. `resume-customizer` is the engine behind any resume or
cover letter, and `humanizer` cleans up every generated draft by applying Wikipedia's "Signs of AI
writing" checklist, which is a writing-quality pass and not a way to dodge detection. The engine's own
rules also make it build a per-claim audit table before it will call anything final, and put its
weakest claims in front of you to soften or drop rather than quietly shipping them. There is a full
table of what each one does in the collapsed section headed *The twelve skills*, further down.

## Why the memory matters more than the templates

A job search done properly is months of iterative work, and each application teaches you something
real: which hook a recruiter responded to, which STAR story landed, what comp range a company actually
has. STAR is the interview answer format: situation, task, action, result. Most panels are listening
for it even when they don't name it. Most people lose all of that between applications and start the
next one cold.

The value here isn't the resume templates but the **memory loop**. `update-memory` and
`track-application` make every future application smarter than the last, `patterns` turns the
accumulated tracker into targeting changes (which score floor, which archetypes, which blockers), and
`followup` catches the second touch most candidates never send.

The methodology it runs on (STAR weaving, narrative-arc cover letters, applicant-tracking-system
compliance rules, per-claim defensibility audits, the humanizer pass) is preserved from a real
director-PM job search. An applicant tracking system, or ATS, is the software that parses your resume
before a person ever reads it, which is why the formatting rules are strict. You bring your own
substance.

## See what it produces, without installing anything

The [`examples/`](examples/) directory ships a complete fictional profile, the job description it was
aimed at, and the resume PDF that came out, all from this same plugin end to end. It is there so you
can judge the output quality in 10 seconds without installing anything.

| File | What it shows |
|------|----------------|
| [📄 **`jane-doe-resume.pdf`**](examples/jane-doe-resume.pdf) | 2-page ATS-compliant resume for fictional Director PM Jane Doe, tailored to a fictional Director-AI-Platform role |
| [📋 `example-jd.md`](examples/example-jd.md) | The fictional Northstar AI job description the resume was tailored against |
| [👤 `EXAMPLE_PROFILE.md`](examples/EXAMPLE_PROFILE.md) | Jane's fully-filled `YOUR_PROFILE.md`: the input the plugin used |
| [🌐 `jane-doe-resume.html`](examples/jane-doe-resume.html) | Same resume in HTML if you want to inspect the layout |

**All content is fictional.** Jane Doe, RevenueFlow Inc, MetricFlow, ScalePay, BlueCart: none are real.

## Privacy: don't publish your own job-search data

Once you fill this in, it holds the private half of a job search: your contact details and
compensation, the companies and recruiters in your pipeline, your positioning gaps, your real stories,
your maintained resume, and every tailored document it generates. **None of that should reach a public
repo.** The exact file list is in the section headed *Which files hold your data*, which you can
open just below.

**Where your data does go.** There is no server to run, no database, and no API key to set up. What
does leave your machine is worth knowing before you fill anything in, so here is the whole of it.

- **The model sees your profile.** This runs inside Claude Code, so whatever is in your profile goes
  to the model the same way the rest of your prompt does.
- **A session-start hook loads that profile automatically, in every project, not just this one.** It
  is unfiltered and it does not wait for you to run a skill, so if you open Claude Code inside your
  employer's repo with the plugin enabled, your compensation targets and pipeline go into that
  session too. Remove the `SessionStart` block from `hooks/hooks.json` if you would rather load it
  by hand.
- **`evaluate` searches the open web for compensation data**, on Glassdoor, Levels.fyi and Blind. That
  means the company and role you are researching leave your machine as a search query. If your search
  is confidential, this is the line to read twice.
- **Some skills fetch a URL**, to read a job description you paste as a link, or to check a public
  number before you cite it.
- **The private-repo route below pushes the whole filled repo to GitHub.** Private, but hosted, so it
  is off your machine too.

**A GitHub fork of a public repo is always public: you cannot make a fork private.** So the safe way to personalize is to clone this template into a brand-new **private repository of your own**, not to fork it:

```bash
git clone https://github.com/aksheyw/career-command-center-template.git my-job-search
cd my-job-search
git remote remove origin
# create a new PRIVATE repo and push into it (GitHub CLI shown; or make one in the UI and add it as origin):
gh repo create my-job-search --private --source=. --remote=origin
git push -u origin main
```

Now your repo is private and disconnected from the public template, so you can fill every file in place and version it freely, and nothing is ever public. If you go this route the git-ignore machinery described under *Which files hold your data* is just a backstop. (You can still pull template updates later: `git remote add template https://github.com/aksheyw/career-command-center-template.git`, then `git pull template main`.)

**Git-ignore only stops files that were never tracked.** If you have already committed or pushed a
filled file, open *If you ALREADY committed or pushed real data* below before you do anything else,
because ignoring it now will not
help you.

As shipped, every committed file is safe (placeholders and fictional rows only). Decide private-standalone-repo vs public-repo **before** your first real entry, because it is far cheaper than cleaning up after.

<details>
<summary><b>🔍 Which files hold your data, and the git-ignore machinery that keeps them out of a public repo</b></summary>

Your filled files hold private job-search data: contact details and compensation (`YOUR_PROFILE.md`, `detailed-context.md`), the companies and recruiters in your pipeline (`applications.md`, `CUSTOMIZATION_MEMORY.md`), your positioning gaps and network (`STRATEGIC_GAP_ASSESSMENT.md`), your real stories and filled interview prep (`star-stories.md`, `story-bank-index.md`, `interview-prep.md`), your maintained resume (`generic-resume.docx`), and every tailored resume and cover letter you generate (in `output/`). None of that should reach a public repo.

If your repo must stay public, the template is built so the documented happy path **cannot** commit your real data:

- Every personal-data file ships as a committed **`*.example.md` placeholder skeleton**. You **copy it to the real filename** and fill the copy. The real filenames (`references/YOUR_PROFILE.md`, `.../star-stories.md`, `references/generic-resume.docx`, etc.) are all listed in `.gitignore`, so git never tracks them, which means filling and committing normally leaves your real data untouched on disk and out of every commit.
- `references/applications.md` is created for you by `track-application` from `applications.example.md`; it (and generated `references/pattern-analysis-*.md` reports) are git-ignored too.
- **Generated resumes and cover letters are git-ignored by design.** `apply` writes every tailored resume and cover letter into `output/`, which is git-ignored (only its `README.md` is tracked); the generated-document filename patterns (`*_Resume_*.docx`, `*_CoverLetter_*.docx`, and their `.pdf` siblings) are ignored as a backstop too, so a `git add .` can never stage a generated application even if you save it elsewhere.
- The `.local.md` suffix is also git-ignored, for any extra personal copy you want to keep out of git.

To check it is working on a file you have filled: `git check-ignore -v references/YOUR_PROFILE.md` should name the `.gitignore` line that covers it.

</details>

<details>
<summary><b>⏳ If you ALREADY committed or pushed real data</b></summary>

Git-ignore only stops files that were **never** tracked. If a real-named file (a filled `YOUR_PROFILE.md`, a generated resume in `output/`, etc.) is already in your repo's history, you have to actively remove it, and if it was pushed to a public remote, treat it as exposed:

- **Committed locally, but never pushed yet?** Untracking alone is NOT enough, because the file still lives in the earlier commit, so an ordinary `git push` later would publish it. You MUST purge it from history BEFORE your first push: run the history purge below (`git filter-repo --invert-paths --path <file>` or BFG), then copy from the `.example.md` and refill so it stays local going forward.
- **Already pushed to a public remote?** The data was publicly visible, so **treat it as compromised** (assume it was crawled, cached, or forked while public). Then purge it from history: [`git filter-repo`](https://github.com/newren/git-filter-repo) (`git filter-repo --path references/YOUR_PROFILE.md --invert-paths`) or [BFG](https://rtyley.github.io/bfg-repo-cleaner/) strips the file from every commit, after which you force-push. Often the simplest, safest option is to **delete the public repo entirely and recreate a private one** from a clean clone, using the private-repo steps above.
- A history rewrite or repo deletion does **not** un-expose what was already seen while the data was public. That is why going private from the start is the recommendation: cleanup is damage control, not prevention.

</details>

## Install

You need [Claude Code](https://docs.claude.com/claude-code) installed, and a job description to try it
on. There are two ways in, and which one you want depends on whether you are trying it or using it.

### Just trying it

Start Claude Code by running `claude` in your terminal. These two lines are then typed **inside that
session**, not back in your shell:

```
/plugin marketplace add aksheyw/career-command-center-template
/plugin install career-cc@aksheyw-cct
```

`aksheyw-cct` is the marketplace name and `career-cc` is the plugin name, both set in
`.claude-plugin/marketplace.json`, which is why the skills arrive as `/career-cc:evaluate` and so on.

Now run the one skill that needs no profile:

> Run `/career-cc:evaluate` on this JD: [paste a job description]

If a 7-block analysis comes back with a GO, CAUTION or SKIP verdict, it is wired correctly. Stop here
if you are only looking. **Do not fill in your real profile on this path**: the plugin lives inside
Claude Code's own plugin directory, not in a repo you control, so none of the git-ignore protection
below applies to anything you put there.

### Actually running a job search on it

Work from your own **PRIVATE** clone, using the commands in the **Privacy** section above. Those need
the [GitHub CLI](https://cli.github.com) installed and signed in, or you can create the empty private
repo in the GitHub web interface and add it as `origin` yourself.

From inside that clone, in your shell:

```bash
cp references/YOUR_PROFILE.example.md references/YOUR_PROFILE.md
claude --plugin-dir ./
```

The first line makes your own profile from the committed skeleton. The second starts Claude Code with
this clone loaded as a plugin, and it lasts for that session only, so it is how you start work each
time. Fill the three sections marked ⭐ MINIMUM VIABLE in `YOUR_PROFILE.md`, then run
`/career-cc:apply` on a job description to get the tailored documents.

[QUICKSTART.md](QUICKSTART.md) walks the whole path step by step. The full setup, the checks that it
worked, and the troubleshooting list are in the collapsed sections below.

<details>
<summary><b>🔧 The twelve skills, and what each one does</b></summary>

Ten you invoke by name, plus `resume-customizer` and `humanizer`, which run on their own whenever a
document is being generated.

| Skill | What it does |
|-------|--------------|
| `apply` | Paste a JD. Get JD analysis + tailored resume + cover letter + interview quick-hits |
| `evaluate` | 7-block JD assessment with go/no-go score before you invest in a full application |
| `interview` | Full interview prep pack for a named company: 2-min pitch, STAR stories, likely questions, 90-day plan, salary prep |
| `outreach` | The right outreach template for a contact (cold LinkedIn, InMail, recruiter email, warm referral), personalized |
| `generic-letter` | Network forwarding cover letter for warm intros and alumni networks |
| `salary-negotiate` | Compensation prep: target range by company type, scripts, counter-offer handling |
| `track-application` | Log applications to prose memory + a structured tracker; see pipeline conversion rates |
| `followup` | Cadence tracker: flags overdue/urgent applications and drafts the second-touch message most candidates never send. *(Cadence model adapted from [santifer/career-ops](https://github.com/santifer/career-ops) under MIT.)* |
| `patterns` | Rejection-pattern analysis: score thresholds, converting archetypes, blocker buckets, concrete targeting changes. *(Analysis model adapted from [santifer/career-ops](https://github.com/santifer/career-ops) under MIT; the funnel staging, the in-flight exclusion and the zero-denominator guards are rebuilt here.)* |
| `update-memory` | Capture what worked (or didn't) per application so future ones get smarter |
| `resume-customizer` | Auto-loads on any resume or cover letter request (the core engine) |
| `humanizer` | Auto-applied after every document generation to strip AI writing patterns. *(Authored by [@blader](https://github.com/blader/humanizer) under MIT, bundled here for convenience.)* |

</details>

<details>
<summary><b>📋 The eight files you fill in, and what goes in each</b></summary>

Each personal-data file ships as a committed **`*.example.md` placeholder skeleton**. You **copy it to the real filename** (which is **git-ignored**) and fill the copy, and every skill then picks up your data via the `${CLAUDE_PLUGIN_ROOT}` path variable. Because the real filenames are git-ignored, following this path in a public repo can never commit your real data. (In your own private repo you can version them freely; see **Privacy** above.)

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

Plus one binary you drop in (not a skeleton): `references/generic-resume.docx`, which is your maintained generic resume and the canonical file the resume skills copy from (also git-ignored). See *Full setup* below and `resume-customizer` STEP 0.

Everything else in the repo is methodology (the rules, frameworks, templates, language guidance) that works across users, and you usually don't touch it.

</details>

<details>
<summary><b>📦 Full setup step by step, checking it worked, and troubleshooting</b></summary>

1. **Clone** this template, ideally into your own **private repo** (see **Privacy** above; forking a public repo keeps it public, so clone-into-private instead), under your Claude Code plugins folder, or wherever your harness loads plugins from.
2. **Rename the plugin** in `.claude-plugin/plugin.json` (`name`, `version`, `description`) to be yours. Do NOT add an `author` field with your real identity unless you intend to PUBLISH your fork publicly, because `plugin.json` is a tracked file, so anything you put there becomes public the moment the repo is pushed. For a private job-search setup (the normal case), leave `author` out entirely; it is optional publisher metadata, not required for the plugin to work.
3. **Copy each `*.example.md` to its real filename, then fill the copy.** Every personal-data file ships as a committed placeholder skeleton; you fill the git-ignored real file, not the `.example.md`. At minimum, start with your profile:
   ```bash
   cp references/YOUR_PROFILE.example.md references/YOUR_PROFILE.md
   ```
   (`applications.md` is the exception: you don't copy it by hand; `track-application` creates it from `applications.example.md`.)
4. **Drop in your canonical resume.** Once you maintain a generic resume, save it as `references/generic-resume.docx` (git-ignored). The `resume-customizer` / `apply` skills copy from this fixed path and apply targeted edits, and they never rebuild from templates once it exists. No canonical yet? The first resume you generate and approve is saved there and becomes the canonical (see `resume-customizer` STEP 0).
5. **Update `hooks/hooks.json`** only if you renamed `YOUR_PROFILE.md` to something else (this file is auto-loaded at session start; it prints a copy-me hint until the real file exists). ⚠️ **If you rename it, the new name is NOT automatically git-ignored**, because `.gitignore` protects the exact path `references/YOUR_PROFILE.md` only. Either give the new file a `.local.md` suffix (e.g. `MY_PROFILE.local.md`, since the `*.local.md` pattern is already ignored), or add your custom path to `.gitignore` in the same step. A renamed profile without one of these gets committed like any other file.
6. **Try a skill.** Paste any JD into `apply` and watch the workflow run end-to-end.

The marketplace name is `aksheyw-cct` and the plugin name is `career-cc`, so the skills install as `/career-cc:evaluate`, `/career-cc:apply` and so on. (See `.claude-plugin/marketplace.json` for the source of those names.)

**Checking it worked, and what to do when it hasn't**

After loading the plugin, in a fresh Claude Code session:

- Check `~/.claude/settings.json`: `enabledPlugins` should list this plugin (or, if you used `claude --plugin-dir`, the plugin shows in the session's plugin list at startup).
- Type `/`, and autocomplete should show the 12 namespaced skills (e.g., `/career-cc:evaluate`, `/career-cc:apply`, `/career-cc:interview`, etc., based on the plugin name you set in `.claude-plugin/plugin.json`).
- The session-start hook prints your profile into the session when it loads, or a one-line copy-me hint if `YOUR_PROFILE.md` does not exist yet.

**Troubleshooting**

- **`/career-cc:<skill>` doesn't autocomplete:** the plugin name in `.claude-plugin/plugin.json` is what gets prefixed. If you kept the default `career-command-center-template`, your skills are `/career-command-center-template:evaluate` (long but functional). Rename the plugin to something shorter (e.g., `career-cc`) before invoking.
- **Session-start hook isn't loading `YOUR_PROFILE.md`:** check `hooks/hooks.json` references the correct filename. If you renamed `YOUR_PROFILE.md`, update the hook's path, and make sure the new name is still git-ignored: use a `.local.md` suffix (already covered by `*.local.md` in `.gitignore`) or add the custom path to `.gitignore`, because only the exact path `references/YOUR_PROFILE.md` is ignored by default.
- **Generated resume has placeholder text instead of your details:** the skills are designed to flag missing data rather than fabricate. Fill in the section the placeholder points to and regenerate.
- **`/career-cc:evaluate` works but `/career-cc:apply` doesn't:** `apply` requires `YOUR_PROFILE.md` to have at least the 3 ⭐ MINIMUM VIABLE sections filled. `evaluate` works on JD alone, which is why it's the first skill to test.
- **Plugin loaded but skills aren't namespaced:** confirm you installed it as a plugin (not by copying individual `SKILL.md` files to `~/.claude/skills/`). Plugin install gives you `/career-cc:apply`; loose-skill install gives bare `/apply` and bypasses the session-start hook.

</details>


<details>
<summary><b>📄 What an <code>/evaluate</code> verdict actually looks like</b></summary>

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

</details>

<details>
<summary><b>🔧 The rules it enforces on every document it generates, preserved from the original</b></summary>

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

</details>

<details>
<summary><b>🌉 Using this for a different role, seniority or country</b></summary>

The default templates assume a director / principal PM job search in India.

> ⚠️ **Privacy note before you personalize:** every file named below (except `YOUR_PROFILE.md`) is a TRACKED methodology file. Editing it to match YOUR geography, role archetypes, or seniority writes your real job-search targets into files that become public if this repo is public. Do methodology personalization only in a **private** clone (see **Privacy** above), or leave the tracked methodology generic and keep your specifics in the git-ignored `YOUR_PROFILE.md`, which the skills always read first.

- **Different geography:** edit currency formatting + phone format in `skills/resume-customizer/SKILL.md` ATS rules; set your actual target in `references/YOUR_PROFILE.md` (git-ignored), and re-theme the company-type calibration buckets in `skills/resume-customizer/references/career-tools.md` if needed
- **Different role family:** rewrite the company-type strategies in `SKILL.md` (`AI`, `Consumer Scale`, `Enterprise/B2B`, `Fintech`, `Telco`) to match the role archetypes you target
- **Different seniority:** adjust bullet length norms (40-55 words is calibrated for senior PM)

The 7-block evaluation framework, narrative-arc cover letter, humanizer skill, and STAR weaving rules generalize across roles.

</details>

<details>
<summary><b>📦 Plugin structure</b></summary>

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

</details>

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

## Origin

This template was extracted from a real director-PM job search workflow. All personal data has been replaced with skeletons; the underlying methodology is preserved.

If you find this useful, share the result, or fork it and make it better.
