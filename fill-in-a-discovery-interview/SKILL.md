---
name: fill-in-a-discovery-interview
description: Work out answers for a project's discovery interview from what is known about the client, and propose them for approval.
---

# Fill in a discovery interview

Use this when someone wants help completing the discovery interview (business profile, goals, website preferences) for a project.

1. **Find the project.** `projects.search` by name or client, then `projects.get` for its client, status and meetings.
2. **See what is missing.** `projects.interview` with the project id. Note which fields are empty and which already have answers. Never overwrite a good answer with a guess.
3. **Gather what is already known.** Search notes for the project and its client (`notes.search` with `on` and `on_id`), and look at the client (`clients.get`) and their websites (`websites.search`, `websites.get`). Use only what the Hub actually holds, or what the person tells you.
4. **Propose, with sources.** Call `projects.propose_answers` once with every answer you are confident in. For each: the field key from `projects.interview`, the proposed text in the client's own plain words, and where it came from ("their About page", "note from 12 March", "you told me"). The person sees each next to the current answer and approves.
5. **New things, not answers.** Locations, products, pages, social channels, websites they like, customer groups and their questions, list entries and business details are new content: use `projects.propose_changes` (one card for the whole set, each with its source). Only what you found; no guesses.
6. **Say what you could not fill in** and what would settle it (a question to ask the client in the meeting). Do not invent answers to look complete.
7. Tell the person a card is waiting for their approval; nothing is saved until they press Apply. Never say the answers are saved.

Keep answers short and factual. Colour preferences and theme are the client's choice: propose only if the client has said so.

These steps use the WP Easy Hub's tools (projects.search, projects.get, projects.interview, projects.propose_answers, projects.propose_changes), available when the Hub is connected as an MCP server.
