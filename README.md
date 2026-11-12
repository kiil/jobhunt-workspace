---
type: guide
title: Job search workspace
description: Getting started with the job search workspace.
---

# Job search workspace

A job search as a graph of notes: one master CV, tailored CV variants, one cover letter per application that also carries the application's state and contact log, the organizations you applied to, and a daily list of new postings. Start at [the job map](MOC-job.md).

## Worked example

The workspace ships with a fictional applicant, Robin Vale, and three applications in three different states:

- [Northwind Wholesale](letters/northwind-wholesale.md) — sent, followed up once by phone and once by email, rejected among 100 applicants.
- [Harbour Museum of Modern Art](letters/harbour-museum.md) — unsolicited, sent, waiting by design.
- [Clearpath Consulting](letters/clearpath-consulting.md) — a draft that was archived when the deadline passed.

Every person, company, address and number in them is invented. Replace them with your own before you start, beginning with [the master CV](cv/master.md).

## Daily use

``` bash
iwe new -t cover-letter "Company name"     # → letters/company-name.md
iwe new -t cv "Company name"               # → cv/company-name.md, then copy from the master and cut
iwe new -t organization "Company name"     # → organizations/company-name.md
iwe update -k letters/company-name --set status=sent --set sent=2026-11-12
iwe find --filter 'type: cover-letter' --project 'company,status,deadline,sent' --sort 'deadline:1'
iwe schema validate
```

The agent instructions are in [AGENTS.md](AGENTS.md). The skills in `.claude/skills/` describe how to draft an application and how to log a contact.
