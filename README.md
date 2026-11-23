# WP Easy Hub: agent playbooks

Playbooks (Claude skills) and a tool reference for AI agents that work with a WP Easy Hub through its MCP server.

- `TOOLS.md`: every tool the Hub offers an agent (an agent is only offered the tools its signed-in person may use).
- One folder per playbook, each with a `SKILL.md`.

## Connecting

Your Hub is an MCP server at `https://<your hub>/api/mcp`. Create a personal access token in Settings > AI access (needs Level 3), or let a hosted agent connect through the Hub's OAuth sign-in. The agent can never do more than the person it acts for, and the agency decides which areas it may read or change.

Claude Code example:

    claude mcp add wpeasy-hub -s local --transport http https://<your hub>/api/mcp --header "Authorization: Bearer <token>"

These files are generated from the Hub itself (`php artisan agent:skills-export`), so do not edit them by hand.
