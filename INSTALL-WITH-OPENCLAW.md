# Install With OpenClaw

Follow this in order.

## 0. Get GOG working

Complete `SETUP-GOG.md` first.

Do not continue until these all work:

- Gmail message search
- Calendar list / event read
- Sheets metadata read
- Google Docs read if you plan to use meeting-notes ingestion

## 1. Gather install values

Collect these before editing files:

- `{{OWNER_NAME}}`
- `{{ASSISTANT_NAME}}`
- `{{ASSISTANT_EMAIL}}`
- `{{PRIMARY_WORK_EMAIL}}`
- `{{PERSONAL_EMAIL}}`
- `{{BUSINESS_NAME}}`
- `{{BUSINESS_URL}}`
- `{{TIMEZONE}}`
- `{{PRIMARY_UPDATE_CHANNEL}}`
- `{{PRIMARY_UPDATE_TARGET}}`
- `{{GOOGLE_SHEET_ID}}`
- `{{TARGET_MARKET}}`
- `{{TARGET_GEOGRAPHY}}`

Optional additional values if you use more calendars:

- `{{SECONDARY_CALENDAR_EMAIL_1}}`
- `{{SECONDARY_CALENDAR_EMAIL_2}}`
- `{{SECONDARY_CALENDAR_EMAIL_3}}`

## 2. Install the skills

Copy these directories into `~/.openclaw/skills/`:

- `skills/executive-assistant`
- `skills/business-development`
- `skills/daily-task-manager`
- `skills/daily-task-prep`

## 3. Install the workspace files

Copy these into `~/.openclaw/workspace/`:

- `clawchief/`
- `workspace/HEARTBEAT.md`
- `workspace/TOOLS.md`
- `workspace/memory/meeting-notes-state.json`

Note:
- `workspace/tasks/current.md` is included only as a deprecation note for older installs
- the live task source of truth is now `clawchief/tasks.md`

## 4. Add your private workspace files

This public pack does *not* ship personal context files.

Create your own versions of these if your setup depends on them:

- `AGENTS.md`
- `SOUL.md`
- `USER.md`
- `IDENTITY.md`
- `MEMORY.md`
- `memory/`

## 5. Replace placeholders

Replace every placeholder token before testing.

Minimum search list:

- `{{OWNER_NAME}}`
- `{{ASSISTANT_NAME}}`
- `{{ASSISTANT_EMAIL}}`
- `{{PRIMARY_WORK_EMAIL}}`
- `{{PERSONAL_EMAIL}}`
- `{{BUSINESS_NAME}}`
- `{{BUSINESS_URL}}`
- `{{TIMEZONE}}`
- `{{PRIMARY_UPDATE_CHANNEL}}`
- `{{PRIMARY_UPDATE_TARGET}}`
- `{{GOOGLE_SHEET_ID}}`
- `{{TARGET_MARKET}}`
- `{{TARGET_GEOGRAPHY}}`

Then customize these files for your real workflow:

- `workspace/TOOLS.md`
- `clawchief/priority-map.md`
- `clawchief/tasks.md`
- `skills/business-development/resources/partners.md`
- `cron/jobs.template.json`

## 6. Create the cron jobs

Use `cron/jobs.template.json` as the starting pattern.

Recommended starting jobs:

1. executive assistant sweep
2. daily task prep
3. daily business-development sourcing

Optional jobs:

4. nightly backup
5. self-update

Notes:
- keep prompts short and let the skill carry the workflow details
- if your sweep window cannot be expressed cleanly in one cron, split it into a main recurring job plus boundary jobs
- keep backup disabled until the remote repo and allowlist are correct
- keep self-update disabled unless you explicitly want that behavior

## 7. Validate the install

Run `INSTALL-CHECKLIST.md`.

## Optional: local lead enrichment

This starter kit does not require a lead-enrichment tool.

If you already use one, document it in `workspace/TOOLS.md` and keep it as an optional helper during prospecting.

Keep these rules:

- do not block the base install on it
- still check the website first
- verify any candidate email before using it
- treat the outreach tracker as the source of truth
- only use it for leads that already match your configured target market / geography
- do not broaden targeting or increase batch size just because enrichment is available

Example optional setup:

- local CLI: `findymail` via `@paulelliot/findymail-cli` (unofficial)
- install: `npm install -g @paulelliot/findymail-cli`
- repo: `https://github.com/paulelliotco/findymail-cli`
- workflow: website public email -> enrichment lookup -> verification -> continue the normal tracker/outreach flow
