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

These steps use the WP Easy Hub's tools (hub.attention, events.recent), available when the Hub is connected as an MCP server.
