---
name: triage-a-website
description: Find out what is wrong with a website (down, slow, broken, out of date) and what to do about it.
---

# Triage a website

Use this when someone says a website is down, broken, "acting up" or asks "what is wrong with X?".

1. **Find it.** `websites.search` with part of the name, address or client. If more than one matches, show the short list (name, address, status) and ask which one. If the person is already looking at one, it is that one.
2. **Look at everything at once.** `websites.problems` with its id. Read the status first: is it up? If down, what does `last_error` say and since when?
3. **Say what you see, plainly,** in this order: is it answering; the likely cause (the error in words, not codes); anything else wrong (vulnerabilities, updates, broken links, backups, expiring domain or certificate). Do not list things that are fine.
4. **Dig only where it helps.**
   - Went down recently, or keeps going down: `websites.history` (when and why, how long).
   - Someone changed something: `events.recent` with `website_id` (who did what and when).
   - Broken links reported: `websites.links`.
   - Backup trouble: `websites.backups`.
5. **Check whether it is still happening** with `websites.check_now` (only if the person wants it, and the website is not on hold).
6. **Finish with next steps** the person can take, in plain words. Offer to add a note (`notes.add`, kind task) so the problem is not forgotten. Offer to install waiting updates (`websites.update`) if that is part of the fix, and remember it needs their approval.

Do not guess at causes you cannot see. If you cannot tell, say what you looked at and what would tell you more.

These steps use the WP Easy Hub's tools (websites.search, websites.problems, websites.history), available when the Hub is connected as an MCP server.
