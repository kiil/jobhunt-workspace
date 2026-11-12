---
type: map
title: Job
description: Entry point to the job search — material, applications and the watch.
---

# Job

Convince one organization that you solve one problem for it: one reader, one deadline, and a CV instead of a sales pitch.

## Material

[Letter material](letter-material.md) — standing claims with evidence and tried phrasings. Raw material for letters, not text to paste

[Master CV](cv/master.md) — the stock. Every tailored variant is a copy that has been cut down, and every bullet is checked word for word against this one

[Organizations](MOC-organizations.md)

## Active applications

The state lives in the letter's frontmatter and can be queried:

``` bash
iwe find --filter 'type: cover-letter' --project 'company,status,deadline,sent' --sort 'deadline:1'
```

- [Harbour Museum of Modern Art](letters/harbour-museum.md) — unsolicited, as an independent AI advisor, sent 27 July 2026. Strongest opening paragraph: the applicant lives nearby and visits often. CV: [harbour-museum](cv/harbour-museum.md)

## Closed

- [Northwind Wholesale](letters/northwind-wholesale.md) — Experienced AI builder, sent 3 August 2026. Opens on the posting's own sentence about solutions that must still run after the skiing holiday. Rejected 19 August among 100 applicants. CV: [northwind-wholesale](cv/northwind-wholesale.md)
- [Clearpath Consulting](letters/clearpath-consulting.md) — AI solutions consultant. Drafted, never sent; archived when the deadline passed. CV: [clearpath-consulting](cv/clearpath-consulting.md)

## The watch

New postings are collected into one note per day under `watch/`, for example [12 November 2026](watch/2026-11-12.md). Each entry has the title, company, source, date, location and link. Judge the list, then create a letter for the ones worth applying to.

## What works

- **The opening paragraph decides the rest.** If it could be sent to another company unchanged, it is not finished.
- **Reuse claims, not paragraphs.** Letters that share paragraphs word for word read like templates. The best ones say the same thing in new words for the actual reader.
- **Sobriety sells.** Saying when AI is *not* the answer separates an advisor from a vendor.
