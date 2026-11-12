---
name: log-contact
description: Record a touch with an employer (call, email, meeting, portal submission, rejection) in an application's contact log, or a private observation in its case notes, and update the application state. Use when the user reports that they called, wrote, heard back, had an interview, were rejected, or wants to note something about an application.
---

# Log a contact or a case note

Edits one letter note in `letters/`. It records what happened; it never sends anything.

## Decide which section

- **A touch** — something went between the user and the employer, in either direction. It goes in `## Contact log`.
- **A case note** — the user observed, prepared or decided something without touching the employer: call preparation, «gave up, too far away», «the role was re-posted». It goes in `## Case notes`.

A case note must never go in the contact log: follow-up rules count outgoing entries there, and a private note would count as a follow-up.

## Write the entry

1. Find the letter: `iwe find --filter 'type: cover-letter' --project 'company,status'`.
2. Create the section if it is missing, placed after `## Closing` in the order Contact log, Case notes, Notes.
3. Add a `###` entry at the top of the section, newest first.
   - Contact log heading: `### <timestamp> <IN|OUT> <CHANNEL>`, channel one of `EMAIL`, `CALL`, `MEETING`, `LINKEDIN`, `PORTAL`, `OTHER`.
   - Case note heading: `### <timestamp>` alone.
   - The timestamp is ISO 8601 with offset, `2026-08-13T11:41:00+01:00`. When only the date is known, write the date alone; do not invent a time.
4. In the body, say what happened in a sentence or two. For an email, put the subject line first as `**Subject:** «…»`.

## Update the state

Set the fields that changed with `iwe update -k letters/<slug> --set …`:

- sent: `status=sent`, `sent=<date>`
- first interview: `status=interview`, `interviewed=<date>`
- rejection: `status=rejected`, `rejected=<date>`, and `applicants`, `rejection_reasons` or `hired_profile` if the employer said so, in their words
- withdrawn: `status=withdrawn`
- put away: `archived=<date>`, `archived_reason=<why>` — status unchanged

## Follow-up rules to mention

- Two outgoing touches after sending, and the case is parked. Tell the user when a third would break the rule.
- A reply moves the case from «waiting» to «in dialogue»: do not chase someone you are already talking to.
- Never chase an unsolicited application (`solicited: false`).

Run `iwe schema validate` afterwards.
