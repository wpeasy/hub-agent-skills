# WP Easy Hub tools

Generated from the Hub's tool registry. A tool is only offered to a person who may use it.

## skills.load

Load a playbook: step-by-step guidance for a kind of job done well with the Hub's tools (for example triage-a-website or fill-in-a-discovery-interview). Load the matching one before starting such a job, and follow it. Leave the name out to see the list.

- Kind: looks only
- `name` (string): The playbook's name (leave out to list them)

## websites.search

Find websites the Hub watches. Search by name, address or client, and filter by status (up, down, maintenance, unknown) or by group name. Returns each website's id, address, status, group, client and what is waiting. Use websites.get for everything about one.

- Kind: looks only
- `query` (string): Part of a name, address or client name
- `status` (string): up, down, maintenance or unknown
- `group` (string): A group name, or Default for websites in no group
- `limit` (integer): How many to return (1 to 25, default 10)

## websites.get

Everything the Hub knows about one website: status and uptime, what it is built with and where it is hosted, domain, DNS and certificate details, the connector plugin's report (WordPress and PHP versions, updates waiting), health of each check, its group and client, and its notes list. Needs the website's id (from websites.search).

- Kind: looks only
- `id` (integer, required): The website's id

## clients.search

Find clients by business name, contact name or contact email. Returns each client's id, business, contact details, type, and how many websites and projects they have.

- Kind: looks only
- `query` (string): Part of a business name, contact name or email
- `limit` (integer): How many to return (1 to 25, default 10)

## projects.search

Find projects by name or client, optionally by status (active, on_hold, completed). Returns each project's id, name, plan, status and client.

- Kind: looks only
- `query` (string): Part of a project or client name
- `status` (string): active, on_hold or completed
- `limit` (integer): How many to return (1 to 25, default 10)

## projects.get

One project in full: its client, plan, status, timeline (start, due date and whether it is on track), and its meetings with their dates and outcomes. Needs the project's id (from projects.search).

- Kind: looks only
- `id` (integer, required): The project's id

## projects.interview

The discovery interview of a project: each question or field (its key, what it asks) with the answer so far, and which are still empty. Use it before proposing answers, so you only propose what is missing or clearly better. Secrets, files and lists are not included.

- Kind: looks only
- `id` (integer, required): The project's id

## projects.propose_answers

Propose answers for a project's discovery interview, from what you found (the client's website, notes, the person's own words). Each answer needs the field key from projects.interview, the text, and where it came from. The person sees each proposed answer next to the current one and must approve; nothing is saved until they do. Never propose answers you are guessing at: say what is missing instead.

- Kind: proposes; a person must approve
- `id` (integer, required): The project's id
- `answers` (array, required): The answers to propose (1 to 20)

## clients.get

One client in full: contact details, business type, their projects, and their websites. Needs the client's id (from clients.search).

- Kind: looks only
- `id` (integer, required): The client's id

## hub.attention

What needs attention across all websites right now: totals (live, down, on hold), websites down, open vulnerabilities, updates waiting, broken links, certificates and domains running out, and the last day of backups. Start here for "what is wrong?" or "how are things?". Use websites.problems for one website.

- Kind: looks only

## websites.problems

Everything wrong, or about to be, on one website: whether it is up and since when and why not, open vulnerabilities and abandoned-plugin warnings, updates waiting, broken links, the last backups, and domain and certificate expiry. The first thing to use when troubleshooting one website. Needs the website's id.

- Kind: looks only
- `id` (integer, required): The website's id (from websites.search)

## websites.history

A website's recent stretches of up, down and maintenance, with when each began and ended and the reason it was down. Use it to find out when and why a website went down.

- Kind: looks only
- `id` (integer, required): The website's id
- `limit` (integer): How many stretches (1 to 40, default 15)

## websites.backups

A website's recent backups: when, how it ended (ok, partial, failed, stopped), how long it took, how big, why it failed, and whether it was scheduled or started by hand.

- Kind: looks only
- `id` (integer, required): The website's id
- `limit` (integer): How many (1 to 20, default 8)

## websites.links

The broken links confirmed on a website (a link has to fail on two checks), with the address, what went wrong, the status code and the pages it is on, plus when the site was last checked.

- Kind: looks only
- `id` (integer, required): The website's id
- `limit` (integer): How many (1 to 30, default 15)

## events.recent

The most recent things that happened in the Hub (the events log): who did what and when. Filter by a website, or by an event name or the start of one (for example websites.website.changed, agency.backup, clients). Use it to find out what changed, who changed it, and when.

- Kind: looks only
- `website_id` (integer): Only events about this website
- `event` (string): An event name, or the start of one
- `limit` (integer): How many (1 to 40, default 15)

## notes.search

Search notes, tasks, decisions and feedback across projects, websites, clients and the agency (only those you may read). Filter by words, by kind (note, task, decision, feedback), by status (open, in_progress, done) or by the record they are on. Credential notes are never included.

- Kind: looks only
- `query` (string): Words to look for in the note
- `kind` (string): note, task, decision or feedback
- `status` (string): open, in_progress or done (tasks and feedback)
- `on` (string): The kind of record: project, website, client or agency
- `on_id` (integer): The record's id (with `on`)
- `limit` (integer): How many (1 to 25, default 10)

## notes.add

Add a note, task or decision to a project, website, client or the agency. Say what you are about to write before you add it. It is shown under the person's name like any other note, and can be edited or deleted by them.

- Kind: changes something
- `on` (string, required): project, website, client or agency
- `on_id` (integer): The record's id (not for agency notes)
- `kind` (string): note (default), task or decision
- `text` (string, required): What to write

## websites.check_now

Check one website is answering right now (the same as the Check now button) and report what it found. Use it to confirm whether a problem is still there.

- Kind: changes something
- `id` (integer, required): The website's id

## websites.set_group

File a website under a group (a new name makes the group), or take it out of its group with "Default". If the group switches checks on or off for its websites, those apply to this one too. Tell the person which group before you do it.

- Kind: changes something
- `id` (integer, required): The website's id
- `group` (string, required): The group name, or Default for no group

## websites.add

Add a website for the Hub to watch. It needs the FULL address with https:// (services on different subdomains are different websites), and may have a label, a client and a group. Check with websites.search first that it is not already there, and confirm the details with the person before adding. The Hub looks at it straight away and looks up its domain details.

- Kind: changes something
- `url` (string, required): The full address, for example https://example.com
- `name` (string): An optional label
- `client_id` (integer): The client it belongs to (from clients.search)
- `group` (string): A group name to file it under

## websites.update

Propose installing the updates a connected WordPress website is waiting for (WordPress core, plugins and themes), either everything waiting or only the names you give. The person must approve a card before anything is installed; each update is backed up first and put back if the website breaks. Look at websites.problems first to see what is waiting.

- Kind: proposes; a person must approve
- `id` (integer, required): The website's id
- `names` (array): Only these (plugin or theme names, or WordPress for core). Leave out for everything waiting.

## notes.update

Change a task or feedback item: its status (open, in_progress, done), who it is given to (a team member's id, or 0 to take it off them), or pin or unpin any note. Find the note id with notes.search.

- Kind: changes something
- `id` (integer, required): The note's id
- `status` (string): open, in_progress or done (tasks and feedback)
- `assignee_id` (integer): A team member's user id, or 0 for no one
- `text` (string): New wording for the note (plain text)
- `pinned` (boolean): Pin (true) or unpin (false)

## websites.set_monitoring

Put a website on hold (nothing checks it, no alerts) or resume it (it is checked straight away). Say which one you are doing and why.

- Kind: changes something
- `id` (integer, required): The website's id
- `paused` (boolean, required): true = put on hold, false = resume

## websites.set_renewal

Set (or clear) the date a website's domain registration runs out. Needed for .au domains, whose registry does not publish it. The Hub warns when it is within 30 days.

- Kind: changes something
- `id` (integer, required): The website's id
- `renews_on` (string): The date as YYYY-MM-DD; leave out to clear it

## websites.refresh

Ask the Hub to look again at one thing about a website: "domain" (DNS, email, hosting, certificate, what it is built with), "connection" (ask the WordPress connector plugin to send its report now) or "links" (start a broken-link check; it takes a while and runs in the background).

- Kind: changes something
- `id` (integer, required): The website's id
- `what` (string, required): domain, connection or links

## backups.run

Start a backup of one website now. A reason is required (it is kept with the backup). It runs in the background; read websites.backups later to see how it ended.

- Kind: changes something
- `id` (integer, required): The website's id
- `comment` (string, required): Why the backup is wanted (3 to 500 characters)

## clients.add

Add a client (a business and its contact). It does not start a project or send anything. Search first so you do not add one twice.

- Kind: changes something
- `business_name` (string, required): The business name
- `contact_name` (string, required): The contact person
- `contact_email` (string, required): Their email address
- `contact_phone` (string): Their phone

## clients.update

Change a client's details (business name, contact name, email, phone). Only the fields you give change. If the client is linked to WHMCS the change is sent there too.

- Kind: changes something
- `id` (integer, required): The client's id
- `business_name` (string): New business name
- `contact_name` (string): New contact name
- `contact_email` (string): New email
- `contact_phone` (string): New phone

## clients.assign_website

Make a website belong to a client. A website that belonged to another client moves, so check websites.get first and tell the person.

- Kind: changes something
- `client_id` (integer, required): The client's id
- `website_id` (integer, required): The website's id

## projects.propose_changes

Propose NEW discovery content for a project: a location (name, address_line, suburb, state, postcode, phone, email), an item (kind product, page, social or inspiration; name; details), a customer group (name, with a list of questions), a question for an existing group (audience_id, question), a list entry (part, data) or business details (fields such as legal_name, abn, phone, email). Give each change a source. The person sees the whole list on a card and must press Apply; nothing is saved until then. For answers to existing fields use projects.propose_answers. Never invent details: only propose what you found.

- Kind: proposes; a person must approve
- `id` (integer, required): The project's id
- `changes` (array, required): The changes to propose (1 to 25)

## projects.add

Propose starting a project for a client, on a named plan (use the plan name or key exactly as the person said; never choose one yourself). The person approves on a card; it makes the project and its meetings from the plan and sends nothing to the client.

- Kind: proposes; a person must approve
- `client_id` (integer, required): The client's id
- `plan` (string, required): The plan's key or name
- `name` (string): Project name (optional)

## projects.rename

Rename a project. (Plan, status, on hold, start date and deadline changes are not available to agents, except projects.change_plan.)

- Kind: changes something
- `id` (integer, required): The project's id
- `name` (string, required): The new name

## projects.change_plan

Propose moving a project to a different plan (by the plan's key or name). The person approves on a card. Existing meetings are not changed.

- Kind: proposes; a person must approve
- `id` (integer, required): The project's id
- `plan` (string, required): The plan's key or name

## projects.client_access

Propose changing what the client is asked to fill in on a project: whether they may add customer groups or questions (and until when), and which interview sections they are asked (section key => true or false; keys come from projects.interview). The person approves on a card. Nothing is emailed to the client.

- Kind: proposes; a person must approve
- `id` (integer, required): The project's id
- `client_can_add_groups` (boolean): May the client add customer groups
- `client_can_add_questions` (boolean): May the client add questions
- `client_additions_until` (string): Last day they may add (YYYY-MM-DD), or empty for no limit
- `sections` (object): Section key => true (ask the client) or false

## projects.add_starter_questions

Add the agency's standard customer questions to a project that has no customer groups yet.

- Kind: changes something
- `id` (integer, required): The project's id

## projects.rename_document

Rename a project's document group (every version keeps its place). Give the group's key from projects.get.

- Kind: changes something
- `id` (integer, required): The project's id
- `type` (string, required): The document group key
- `label` (string, required): The new name

## automation.canvases

List the agency's automation canvases (one per area: projects, clients, websites, WHMCS, agency settings and actions) with the event nodes on each, whether each is switched on, and how many steps hang off it. Start here to find a flow, then use automation.get_flow.

- Kind: looks only

## automation.get_flow

Read the steps and connections of one canvas, or just the chain that hangs off one event node (give event_node). Each step shows its type, name, on or off, its settings and anything it reaches outside the Hub (an email, an outside address). Secret values such as API keys are always hidden.

- Kind: looks only
- `canvas` (string, required): The canvas key from automation.canvases
- `event_node` (string): Only the chain from this event node id

## automation.reference

What can be built: "steps" lists the kinds of step (type, what it does, its settings with their keys and kinds, what it saves) and "events" lists every event a flow can start from (key, area, what it means). Give type or query to narrow it. Use it before proposing a flow so the settings are right.

- Kind: looks only
- `what` (string, required): steps or events
- `query` (string): Part of a name, type or key to search for

## automation.runs

The most recent runs of a canvas (which event, did it finish or fail, how long, any error), or one run with what each step did (give run_id). Use it to find out why a flow did not do what was expected. Data in a run is shown with sign-in links already hidden.

- Kind: looks only
- `canvas` (string): The canvas key
- `run_id` (integer): One run, in full

## automation.propose_flow

Propose a flow: new steps and how they connect, and/or changes to the name or settings of existing steps. Read automation.reference first so step types and setting keys are right, and automation.get_flow to see what is there. Each new step needs a ref (a short letters-and-digits name you choose, used in connections), a type and its settings; an event node is type "trigger" with setting event. Connect with edges from/to using refs or existing node ids; a condition connects with handle true or false. The person sees the whole proposal on a card and must press Apply. A new event is always saved switched OFF, so after approval tell the person the flow is created but they must go to the canvas and switch it on. Secrets (API keys, headers) cannot be set by an agent. Nothing is ever removed.

- Kind: proposes; a person must approve
- `canvas` (string, required): The canvas key from automation.canvases (an event must sit on its own area's canvas)
- `summary` (string, required): One plain sentence: what this flow is for
- `nodes` (array): New steps (up to 30)
- `edges` (array): New connections (from and to are refs or existing node ids; handle true or false for a condition)
- `changes` (array): Edits to existing steps: new name and/or settings (only the keys given change)

## websites.edit

Change a website's label, address (full, with https://) or client. Only what you give changes. A new address is checked straight away.

- Kind: changes something
- `id` (integer, required): The website's id
- `label` (string): New label (empty text clears it)
- `url` (string): New full address, with https://
- `client_id` (integer): Client id, or 0 for no client

## websites.set_type

Tell the Hub what a website is built with when it got it wrong (a key such as wordpress, shopify, static), or give an empty type to go back to what the Hub detects.

- Kind: changes something
- `id` (integer, required): The website's id
- `type` (string): The platform key, or empty for automatic

## websites.set_checks

Switch the Hub's jobs for one website on or off: uptime, domain, vulnerabilities, links, updates, backups, backup_core. Give only the ones to change, each true or false. The visitor shield is never changed by an agent.

- Kind: changes something
- `id` (integer, required): The website's id
- `checks` (object, required): Job name => true or false

## websites.links_action

Ignore a broken link (for good or until a date), stop ignoring it, or look at it again. Give the link ids from websites.links. 'recheck' looks at up to 10 now.

- Kind: changes something
- `id` (integer, required): The website's id
- `action` (string, required): ignore, unignore or recheck
- `ids` (array, required): Link ids
- `until` (string): Ignore until this date (YYYY-MM-DD); empty = for good

## websites.ignore_update

Set a waiting update aside (so it stops counting) or count it again. Give the website, whether it is a core, plugin or theme update, and its name as shown.

- Kind: changes something
- `id` (integer, required): The website's id
- `action` (string, required): ignore or unignore
- `kind` (string, required): core, plugin or theme
- `name` (string, required): The update as named in websites.problems
- `until` (string): Ignore until YYYY-MM-DD; empty = for good

## websites.acknowledge_notice

Acknowledge a 'possibly abandoned' or 'closed' plugin or theme warning (so it stops counting), with a note. Give website_id to cover one website, or leave it out for every website.

- Kind: changes something
- `type` (string, required): plugin or theme
- `slug` (string, required): Its folder name
- `kind` (string, required): closed or abandoned
- `website_id` (integer): One website, or leave out for all
- `note` (string): Why (up to 300 characters)

## websites.group_update

Rename a website group or pin or unpin it (pinned groups list first).

- Kind: changes something
- `id` (integer, required): The group's id
- `name` (string): New name
- `pinned` (boolean): Pin or unpin

## websites.trace

Step through how the Hub's server reaches a website (name lookup, connection, certificate, the page and redirects) and where it breaks. Changes nothing; sends real traffic, so use it when a website seems down.

- Kind: changes something
- `id` (integer, required): The website's id

## backups.stop

Stop a website backup that is running (it ends as 'stopped', not a failure). Needs the backup's id from websites.backups.

- Kind: changes something
- `id` (integer, required): The website's id
- `backup_id` (integer, required): The running backup id

