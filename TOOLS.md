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

