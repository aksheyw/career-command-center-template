# output/ — generated application documents (git-ignored)

Every tailored resume and cover letter the `apply` and `resume-customizer` skills
generate is written **here**, into `output/`.

**This directory is git-ignored by design.** The generated documents carry your real
name, work history, and the target company — they are private job-search data and
must never reach a public repo. The `.gitignore` ignores everything in `output/`
except this README, and also ignores the generated-document filename patterns
(`*_Resume_*.docx`, `*_CoverLetter_*.docx`, and their `.pdf` siblings) as a backstop
in case a file is ever saved outside this directory.

You never need to touch this file — it exists only so the (otherwise git-ignored)
directory is present in a fresh clone, and to explain why nothing inside it is tracked.
