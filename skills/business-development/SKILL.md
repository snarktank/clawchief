---
name: business-development
description: "Manage {{BUSINESS_NAME}} business-development and outreach-tracking work using Google Workspace via gog. Use when handling prospecting replies, referral-partner outreach, updating the outreach tracker, logging lead status changes, booking or confirming outreach meetings tied to a lead / prospect, or maintaining the operational record of sales / outreach conversations. Prefer this skill over executive-assistant whenever the task touches the outreach tracker, lead status, prospect pipeline, or referral-partner outreach, even if scheduling is involved."
---

# Business Development

Use this skill for outreach and prospect tracking work. Keep it separate from generic executive-assistant inbox clearing.

## Read these first at the start of every run

- `clawchief/priority-map.md`
- `clawchief/auto-resolver.md`
- `workspace/TOOLS.md`
- `skills/business-development/resources/partners.md`

## Core rules

- the outreach sheet / tracker / CRM is the live source of truth; do not treat local prospect files as current state
- do not silently broaden default prospecting beyond the configured target market / geography without explicit direction
- verify a working website before adding a new lead unless the user explicitly waives that requirement
- prefer a real public email when one exists
- if no trustworthy public email is visible and a local lead-enrichment CLI is configured in `workspace/TOOLS.md`, use it only to produce a candidate work email, then verify that candidate before using it
- ignore placeholder or junk addresses from site code
- sweep sent mail so unanswered outreach does not disappear
- if the work touches lead status, pipeline state, or the outreach tracker, this skill owns it even when scheduling is part of the job

## Source of truth

Google Sheet / tracker id: `{{GOOGLE_SHEET_ID}}`

Treat this as the live source of truth for outreach status.
Do not rely on local `.md` or `.csv` prospect files as the current record.

## Current focus

Customize the business-development playbook in `workspace/TOOLS.md`.

At minimum define:
- target geography
- target market or target segments
- default daily batch size
- verification requirements
- any follow-up cadence overrides

If no more specific override exists, default to:
- prospecting inside `{{TARGET_MARKET}}` in `{{TARGET_GEOGRAPHY}}`
- adding only verified leads
- using the default follow-up cadence in this skill

## Optional lead enrichment

If `workspace/TOOLS.md` defines a local lead-enrichment CLI, you may use it only as a helper for already-qualified leads during sourcing.

Rules:
- this is optional and not required for the base workflow
- check the website first and prefer a real public email when one exists
- only use enrichment for leads that already match the configured target market / geography
- verify any candidate email before adding the lead or sending outreach
- do not treat enrichment output as the source of truth
- do not increase batch size or broaden targeting just because enrichment is available

## When to update the tracker

Update the tracker every time outreach state changes.

That includes when you:
- send the initial outreach email
- get any meaningful reply
- ask for a meeting
- book, confirm, reschedule, or cancel a meeting
- record a decline / not-a-fit outcome
- learn a follow-up or next-step detail worth preserving

Do this before you mark the thread handled.

## Inbound reply operating procedure

When partner / referral emails start coming back, process the inbox and the tracker as one workflow.

1. use *message-level* Gmail search to find inbound replies
2. review each inbound thread and identify the current state:
   - positive interest
   - meeting requested / meeting booked
   - decline / not a fit
   - question that needs a response
   - auto-reply / invalid contact / left organization
3. check whether the person already exists in the tracker
4. update the row with what changed
5. only after the tracker is current should the email be considered handled
6. if a meeting is booked through a scheduler, update the row immediately after the booking succeeds

Useful search patterns:

```bash
gog gmail messages search 'newer_than:30d' -a {{ASSISTANT_EMAIL}} --all --json --results-only
```

## Tracker update guidance

Read the current header row before writing.
Do not assume an old example schema is still correct.

Useful pattern:

```bash
gog sheets get {{GOOGLE_SHEET_ID}} 'Leads!A:Z' -a {{ASSISTANT_EMAIL}} --json --results-only
```

Use `--values-json` for reliable writes.
Prefer updating by the actual current column names rather than assuming a frozen fixed layout.

## Follow-up cadence

For unanswered outreach where the lead should stay active, use this default cadence unless the user overrides it:

- first follow-up: about 2 days after the last unanswered outbound
- second follow-up: about 5 days after the previous follow-up
- third follow-up: about 7 days after the previous follow-up

Rules:
- reset the clock after each new outbound follow-up
- record each follow-up in the tracker notes
- after the third unanswered follow-up, stop the automatic sequence and surface the lead if it still matters
- do not auto-follow up when the thread is sensitive, clearly closed, or the user told you to stop

## Default outbound workflow

1. verify the lead is not already in the tracker
2. verify the lead matches the configured target market / geography
3. verify a working website unless explicitly waived
4. inspect the website for a real public email address before leaving email blank
5. if no trustworthy public email is visible and a local lead-enrichment CLI is configured, use it to produce a candidate work email and verify that candidate before use
6. send the initial outreach email using `resources/partners.md`
7. update the tracker immediately after each action
8. sweep sent mail for unanswered outreach and follow up on cadence

## Operating standard

- keep outreach state current as part of doing the work, not as an afterthought
- preserve thread context and recipient context before replying
- process inbound partner replies and tracker updates as one combined workflow
- when an outreach conversation turns into scheduling, coordinate the meeting and then update the tracker immediately after the scheduling action succeeds
- use the priority map to decide what should interrupt the principal and what can be batched
- use the auto-resolver to decide when to act directly versus draft or escalate
