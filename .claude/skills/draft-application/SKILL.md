---
name: draft-application
description: Draft a cover letter and a tailored CV for one job posting from the master CV and the letter material. Use when the user asks to apply for a role, draft an application, write a cover letter or tailor the CV for a posting.
---

# Draft an application

Writes two notes in the workspace and nothing else. It never submits an application, sends an email or fills in an applicant portal.

## Steps

1. Get the posting from the user: pasted text, or a URL the user asks you to read. Note company, position, deadline, contact people with role, phone and email, and any interview dates the posting announces.
2. Pick a slug from the company name, lowercase kebab-case. Create the notes if they do not exist: `iwe new -t cover-letter "<Company>"`, `iwe new -t cv "<Company>"` and, for a new organization, `iwe new -t organization "<Company>"`. Rename keys to the slug if the template produced another.
3. Fill the letter's frontmatter with `iwe update --set`: `company`, `position`, `language`, `url`, `deadline`, `contact`, `contact_phone`, `contact_email`, `contacts`, `interview_dates`, `tags` from the closed vocabulary in the schema, `cv: <slug>`, and `solicited: false` when no posting exists. Leave a field null rather than guess. Write phone numbers with country code and plus.
4. Tailor the CV: copy `cv/master.md` into `cv/<slug>.md` and cut. Choose the bullets that answer the posting; drop the rest. Every remaining bullet must match a master bullet word for word. Only `## Summary` may be rewritten for the role. If a line the posting needs is not in the master, stop and ask the user; if it is true, it goes into the master first.
5. Write the letter in `## Letter`, in the posting's language, prose only, at least three paragraphs, under 900 tokens:
   - Open with the recipient, not the applicant, using something that could only be written about them. If the opening would work with another company's name, rewrite it.
   - Draw claims from `letter-material.md` and rewrite each sentence for this reader. Never paste a tried phrasing unchanged, and never reuse a paragraph from another letter.
   - Say plainly what the applicant has not done if the posting asks for it.
   - End with an invitation to talk.
6. Put working notes in `## Notes`: which claims the letter draws on and why the opening was chosen.
7. Add the application link to `organizations/<slug>.md` and the application to `MOC-job.md` under Active applications.
8. Run `iwe schema validate` and fix what it reports. Tell the user the draft needs reading before anything is sent.
