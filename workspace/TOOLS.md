# TOOLS.md - Local Notes

Use this file for environment-specific details that should *not* live in public skills.

Examples:
- real inboxes and calendars to check
- tracker / CRM notes
- browser profile preferences
- business-development target segments
- voice, device, or camera names
- local SSH aliases

## Communication defaults

- Principal name: `{{OWNER_NAME}}`
- Assistant name: `{{ASSISTANT_NAME}}`
- Primary assistant email: `{{ASSISTANT_EMAIL}}`
- Primary work email / calendar: `{{PRIMARY_WORK_EMAIL}}`
- Personal email: `{{PERSONAL_EMAIL}}`
- Time zone: `{{TIMEZONE}}`
- Primary proactive update route: `{{PRIMARY_UPDATE_CHANNEL}} -> {{PRIMARY_UPDATE_TARGET}}`

## Calendars to check

List the calendars that should be treated as real availability constraints.

Example:
- `{{PRIMARY_WORK_EMAIL}}`
- `{{PERSONAL_EMAIL}}`
- `{{SECONDARY_CALENDAR_EMAIL_1}}`
- Family calendar (conflict source only unless explicitly desired)

## Outreach tracker

- Live tracker / sheet id: `{{GOOGLE_SHEET_ID}}`
- Treat this as the source of truth for outreach state.
- Document the current expected columns here if your sheet is customized.

## Business-development playbook

Document your default sourcing motion here.

Example knobs to define:
- target geography
- primary target segment
- optional secondary target segment
- default daily batch size
- verification requirements
- optional local lead-enrichment CLI
- default outreach tone
- follow-up cadence overrides

Example:
- Geography: `{{TARGET_GEOGRAPHY}}`
- Primary segment: `{{TARGET_MARKET}}`
- Secondary segment: optional custom segment
- Daily new leads: 10
- Lead-enrichment CLI: none by default
- If configured, document the exact command name and lookup order here
- Preferred order: website public email -> enrichment lookup -> verification -> tracker update
- Verify working website + real email before adding
