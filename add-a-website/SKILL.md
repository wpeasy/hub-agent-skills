---
name: add-a-website
description: Add a new website for the Hub to watch, safely (no duplicates, right client and group).
---

# Add a website

Use this when someone asks you to add or start watching a website.

1. **Get the full address.** It needs `https://` (or `http://`), for example https://shop.example.com. Services on different subdomains are different websites. If the person gives only a domain, say what you will use and confirm.
2. **Check it is not already there.** `websites.search` with the host. If it exists, say so and show it instead of adding it again.
3. **Find the client.** `clients.search` by business name or email. If there is no match, say so; the website can be added without a client and linked later. Do not make up a client.
4. **Choose a group** only if the person names one. A group can switch checks on or off for the websites in it (a development group usually turns the shield on), so mention which group you are using.
5. **Confirm before adding:** address, label if any, client, group. Then `websites.add`.
6. **Report what happened:** the website's page link and its first status (the Hub looks at it straight away and looks up its domain details in the background). If it is down, say so and offer the triage steps.

If the website runs WordPress and should be managed (updates, backups, one-click login), tell the person the Hub Connector plugin must be installed and paired on it; that is done in the website's panel, not by you.

These steps use the WP Easy Hub's tools (websites.search, clients.search, websites.add), available when the Hub is connected as an MCP server.
