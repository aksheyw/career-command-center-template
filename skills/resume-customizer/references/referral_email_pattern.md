# Forwardable Referral Email Pattern

When a referrer (your manager, VP, or senior connection) says "send me a mail I can directly forward."

---

## The principle

The email body must be structured for the END recipient (the recruiter), NOT the referrer. The referrer's role is just to forward. So the email is recruiter-facing from sentence one.

This means: no "Hi {{Referrer first name}}, thanks for offering to forward..." opening. Use a generic "Hi," that reads naturally after the recruiter sees "Fwd:" in their inbox.

---

## The pattern

```
Subject: {{Your Name}}: Application for {{Role}} at {{Company}}
(Use the EXACT wording the referrer specifies, if any.)

Hi,

Attaching my resume and cover letter for {{senior product / specific role}} at {{Company}}.

{{2-3 line journey summary covering ENTIRE career — not just current company.
Highlight B2B/enterprise breadth if relevant. NO outcome metrics in this paragraph.}}

{{ONE optional outcome line — pick 2-3 strongest owned outcomes if and only if
the referrer signals "highlight outcomes." Otherwise drop this entire paragraph.}}

AI work:

Launched {{N}} {{tech}}-powered features at {{current company}} for {{market/segment}}.

Open-source AI products (GitHub: github.com/{{handle}}) built on my own time, including:
- {{repo1}}: description with concrete signal (size, scope)
- {{repo2}}: description with concrete signal
- {{repo3}}: description with concrete signal

Closed-source projects include {{list with sources/tools}}. Open to demo during our conversation.

AI Certifications:
- {{University 1}}: {{cert1}}, {{cert2}}, {{cert3}}
- {{University 2}}: {{cert4}}
- {{Provider 3}}: {{cert5}}

Available to join {{immediately / on date}}.

Open to a call this week or the next; happy to send any further information needed ahead of time.

Regards,
{{Name}}
{{Phone}}
linkedin.com/in/{{handle}} | github.com/{{handle}} | {{portfolio URL if any}}
```

---

## Hard rules

1. **No referrer salutation in body** — start with "Hi," generic. Never "Hi [Referrer Name]" since the body must work post-forward when the recruiter reads it without context.

2. **Subject must work post-forward** — even if the recruiter sees "Fwd: [Subject]" in their inbox.

3. **Bold the section headings in Gmail** (Cmd+B): "AI work:", "AI Certifications:". Makes them visually pop.

4. **Two attachments, both PDF:** resume + cover letter. NEVER paste cover letter content into email body — it's an attachment.

---

## Outcomes-belong-where rule

| Document | Outcomes? |
|---|---|
| Email body | NO outcome metrics by default. Optional ONE line if referrer wants. |
| Cover letter | YES — outcome-rich, 4-paragraph arc |
| Resume | YES — full outcome bullets with method and numbers |

**Rationale:** A senior recruiter skims the email body in 10 seconds. Stacked outcomes here look like padding. They open the cover letter for depth, the resume for numbers. The email body's job is to reduce friction to opening the attachments, not convince on its own.

---

## Ownership-language override (referrer-driven)

When the referrer says "write it as if you did it, not just a part of it" or similar:

- Override the cover-letter collaborative-framing rule for the EMAIL BODY ONLY
- Use action verbs: "Launched", "Drove", "Owned outcomes such as..."
- The cover letter and resume CONTINUE to use collaborative framing for honesty under interview probing

This three-document split:

- **Email body:** ownership-led ("Launched 5+ AI-powered mini-apps", "Owned outcomes at {{company}}...")
- **Cover letter:** balanced ("With the broader product team, 5+ features cleared an A/B gate...")
- **Resume:** explicit collaborative bullet ("Collaborated with the broader product team to ship and A/B test...")

Gives the recruiter a confident first signal (email) backed by detailed honest scope (cover letter + resume).

---

## Iteration discipline

Referrer feedback is iterative. Allocate at least 2 hours and expect 4-7 iterations. Each round is more data about what the recruiter will read.

**Typical iteration arc:**

- v1: Conversational draft thanking the referrer → referrer says "send something I can forward directly"
- v2: Forwardable form, brief credibility paragraph → referrer asks about cover letter, motivation
- v3: Add labeled GitHub + Certifications sections → referrer flags emphasis adjustments
- v4: Drop outcomes from body, tighten journey paragraph → referrer accepts
- v5-v7: Polish based on referrer's specific preferences

**Lesson:** Don't lock the email after v1. The compounding loss is shipping a v1 the recruiter would reject; the cost of iterations with the referrer is small.

---

## Pre-send checklist

- [ ] Subject matches referrer's exact wording (if specified)
- [ ] No referrer name anywhere in body — grep for it, should be 0 hits
- [ ] Subject works post-forward (mentally prefix "Fwd:" — does it still scan?)
- [ ] Para 1 stands alone — recruiter understands the email if they only read the first paragraph
- [ ] Both attachments named clearly (e.g., `{{LastName}}_{{FirstName}}_Resume_{{Company}}.pdf`)
- [ ] Section headings bolded in Gmail
- [ ] All cert names match LinkedIn exactly (provider name + cert title)
- [ ] All repo names match GitHub exactly (capitalization, no spaces)
- [ ] Star-count claims on third-party projects verified via WebFetch before send

---

## Related references

- `github_in_resume_pattern.md` — GitHub introduction pattern + repo selection
- `interview-prep.md` — cover letter arc and proof-point depth
