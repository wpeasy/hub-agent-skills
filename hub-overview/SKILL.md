---
name: hub-overview
description: Give a short, useful picture of how everything is going across the websites.
---

# Overview of the Hub

Use this for "how are things?", "anything I need to know?" or at the start of someone's day.

1. `hub.attention`. Lead with what needs action now, most serious first: websites down, serious vulnerabilities, failed backups, domains or certificates about to run out. Then the quieter items (updates waiting, broken links).
2. Give counts, name the websites that matter (with their page links), and skip anything that is fine.
3. If something changed recently that explains a problem, `events.recent` (for example `websites.website.changed` or `agency.backup`) shows who did what and when.
4. Offer the next step for the most important item (the triage skill for a website, or adding a note so it is not lost).

Keep it to a few lines. If everything is fine, say so in one sentence.

## Questions about many websites
Never open websites one by one to answer a question about many. `websites.search` filters by any job (`feature` + `feature_on`), any status dot (`health` + `health_state`), hosting, DNS, email provider, registrar, platform, WordPress version, expiry dates, missing backups, vulnerabilities, broken links, client and on hold, and pages with `offset`. `websites.count_by` answers "how many per ..." in one call. `websites.plugins` finds which websites have a plugin or theme and at what version. `clients.search` and `projects.search` filter the same way (projects by state, plan and whether the client still has answers to give). One call, then summarise.

These steps use the WP Easy Hub's tools (websites.search, websites.count_by, websites.plugins, hub.attention, events.recent), available when the Hub is connected as an MCP server.
