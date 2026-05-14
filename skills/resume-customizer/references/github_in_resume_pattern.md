# GitHub Repo Pattern — Resume, Email, Cover Letter

When and how to surface your public GitHub work in application materials. Most relevant for AI / engineering-flavored PM roles, where a public repo is concrete proof of "I ship."

---

## Where the GitHub link goes

### Resume — always (if you have any public repos worth surfacing)

- Contact line, alongside email + LinkedIn + phone + portfolio
- Format: `github.com/{{handle}}` (no `https://`, ATS-readable, saves space)
- Side projects / AI Product Building section bullets — call out specific repos by name with concrete proof points

### Cover letter — conditional

- Mention in para 3 (the role-specific fit paragraph) when the role values AI / builder skills
- Lead with the **most role-relevant repo by name**, not a generic "see my GitHub"
- Tie GitHub work to other building proof (certifications, side projects) so the repos read as evidence of consistent practice

### Email body — conditional + section-headed for AI roles

- For AI / builder-flavored referrals, use a dedicated **GitHub:** subsection with 2-3 bullets naming specific repos
- Bold the section heading in Gmail (Cmd+B)
- Pair with a **Certifications:** subsection grouping certs by university / provider

---

## The introduction pattern

```
Open-source AI products (GitHub: github.com/{{handle}}) built on my own time, including:
- {{repo1}}: {{one-line description with concrete signal — scope, scale, technical detail}}
- {{repo2}}: {{one-line description}}
- {{repo3}}: {{one-line description}}

Closed-source projects include {{list with sources / tools — e.g., "a personal AI
assistant using {{framework}}, {{another project}}, and {{another}}"}}. Open to
demo during our conversation.
```

Why this works:

- **Opens with action ("I ship AI products"), not "I have a GitHub"** — shipping is the differentiator
- **Names 2-3 specific repos with one-line proof points** — each repo earns its mention with a concrete fact
- **Closed-source projects with offer to demo** — flags work that isn't on GitHub but happened, hedges the depth without overcommitting

---

## Picking which repos to feature for a given role

| Role flavor | Lead repo | Second repo |
|---|---|---|
| AI / agentic PM | {{your strongest AI repo}} | {{methodology / framework repo}} |
| Generic senior PM (non-AI) | {{case-study / portfolio repo}} | {{personal site if it's a meaningful build}} |
| Fintech / consumer apps | {{your shipped fintech-flavored repo}} | {{portfolio}} |
| Content / video / brand | {{your content-flavored repo}} | {{portfolio}} |

Fill in your own repo names above. Re-rank as you ship new repos.

---

## Defensibility rules for repo claims

- **Numbers in repo descriptions must match the GitHub README verbatim.** If your repo says "14 production bugs during initial use," use that phrase — not "14 bugs across my side projects" (drift).
- **Counts must match the actual code.** If a toolkit has 7 agents, don't say "8" or "several." Recruiters will check.
- **Don't claim "open source" unless the repo is actually public.** Verify via `gh repo view` or browsing github.com/{{handle}} before each application.
- **Re-verify visibility before each send.** Repos that were public when written may have been turned private since.
- **Repo name capitalization matters** — match the actual GitHub repo name exactly. If a recruiter searches GitHub, only the exact form will match.

---

## What to avoid

- ❌ "GitHub portfolio" (vague — name what's there)
- ❌ "Active GitHub presence" (AI-cliche)
- ❌ Listing 5+ repos — pick 1-2 most relevant per role, mention "more at github.com/{{handle}}" if needed
- ❌ Coupling repos with vague claims like "showcasing my engineering skills" — name the specific capability
- ❌ Mentioning private repos by name (only public is forwardable to a recruiter)

---

## Star-count claims

If you cite star counts on third-party projects (e.g., "{{ProjectName}} 360K stars"):

- Verify the actual star count via WebFetch on the repo URL **before sending**
- Use a slightly conservative round-down ("360K" when actual is 369K)
- A recruiter will GitHub-search any star count claim within 10 seconds of reading

---

## Related references

- `referral_email_pattern.md` — full forwardable email pattern with GitHub section
- `star-stories.md` — the underlying career stories that GitHub work supplements
