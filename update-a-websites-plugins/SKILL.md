---
name: update-a-websites-plugins
description: See what a website is waiting to update and propose installing it, with the person's approval.
---

# Update a website's plugins, themes and WordPress

Use this when someone wants a website brought up to date.

1. **Find the website** (`websites.search`) and look (`websites.problems`). The `updates_waiting` section lists WordPress, plugin and theme updates with their versions. If update checking is switched off for the website, say it is only reported and cannot be managed from the Hub.
2. **Check it is safe to proceed.** The website should be up. Look at `websites.backups`: a recent good backup is reassuring but not required, because each update is backed up and put back if the website breaks.
3. **Mention anything risky:** a major version jump, a premium plugin whose licence may have lapsed, or a vulnerability that an update fixes (say so: that makes it more urgent).
4. **Propose with `websites.update`.** Everything waiting, or only the names the person chose. A card appears in their panel listing each update; nothing is installed until they press Apply. Tell them that.
5. After they approve, the updates run in the background. Offer to check again later with `websites.problems` and report what installed, what was put back, and what failed.

Never claim updates are installed until the website's own report shows it.

These steps use the WP Easy Hub's tools (websites.search, websites.problems, websites.backups, websites.update), available when the Hub is connected as an MCP server.
