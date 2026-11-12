---
type: guide
title: Agent workspace instructions
description: How an agent works in this job search workspace.
---

# Agent workspace instructions

Reply in the user's language. Write field names, filenames and documentation in English; write letters and CVs in the language of the posting.

This workspace runs a job search: one master CV, tailored CV variants, one cover letter per application, the organizations applied to, and a daily watch of new postings. Start at [the job map](MOC-job.md). Use `iwe` for every structural operation (`iwe find`, `iwe retrieve`, `iwe new -t <template>`, `iwe update --set`) and run `iwe schema validate` after changes.

The records under `cv/`, `letters/`, `organizations/` and `watch/` ship with the template as a worked example. The applicant Robin Vale, every company, contact, address and number in them is fictional. Replace them before recording a real search, and never contact anyone named in them.

## Who owns which fact

- `cv/master.md` is the stock of everything that is true about the applicant, plus the applicant's contact details in its frontmatter. A tailored variant in `cv/<slug>.md` starts as a copy of the master and is cut down. Every bullet in a variant must match a master bullet word for word; only `## Summary` may be rewritten. If a new line is true, add it to the master first.
- `letters/<slug>.md` owns the application's state. `status`, `sent`, `deadline`, `interviewed`, `solicited`, `archived` and the contact fields live in its frontmatter, and only there. Change them with `iwe update -k letters/<slug> --set field=value`, never by editing text.
- `organizations/<slug>.md` lists the applications to one organization.
- [Letter material](letter-material.md) holds standing claims with evidence and tried phrasings. It is material, not text to paste: reuse the claim and rewrite the sentence for the reader.

## Letters

- The opening paragraph is the one paragraph never reused. If it would still work with another company's name in it, it is not finished.
- `## Letter` is prose only, at least three paragraphs and at most 900 tokens. The schema rejects bullet lists there.
- `## Contact log`, `## Case notes` and `## Notes` never go to the employer. When exporting a letter, take only `## Recipient`, `## Letter` and `## Closing`.

## Contact log and case notes

A touch is something that went between you and the employer. It goes in `## Contact log`, newest first, headed `### <ISO 8601 timestamp with offset> <IN|OUT> <CHANNEL>`, where the channel is one of `EMAIL`, `CALL`, `MEETING`, `LINKEDIN`, `PORTAL` or `OTHER`. When only the date is known, write the date alone. Your own observations, decisions and call preparation go in `## Case notes`, headed by the timestamp alone, so they never count as a follow-up. The `log-contact` skill describes the procedure.

Two outgoing touches after an application is sent, and the case is parked: a third does not move an answer, only what they think of you. Unsolicited applications (`solicited: false`) are never chased.

## Actions that reach other people

Never send an email, submit an application, create an account on an applicant portal or type a password. Draft the text, show it, and let the user send it. Log the touch afterwards, when the user confirms it went out.

## Queries

``` bash
iwe find --filter 'type: cover-letter' --project 'company,status,deadline,sent' --sort 'deadline:1'
iwe find --filter 'type: cover-letter, status: sent, solicited: {$ne: false}' --project 'company,sent'
iwe find --filter 'type: cover-letter, interviewed: {$exists: true}' --project 'company,sent,interviewed'
iwe find --filter 'type: cover-letter, status: rejected' --project 'company,applicants,rejection_reasons'
```

`{$ne: null}` matches everything, including empty fields; use `{$exists: true}`. A field written as `null` also exists, so filter null values out of the result when it matters.
