---
name: build-a-flow
description: Read the Hub's automation flows and propose a new flow or an edit, which a person approves and then switches on at the canvas.
---

# Reading and building automation flows

Flows run when something happens in the Hub (an event) and do steps: conditions, emails, outside calls, changes to websites. There is one canvas per area (projects, clients, websites, WHMCS, agency settings, agency actions).

## Reading
1. `automation.canvases` lists the canvases and the event nodes on each (on or off, how many steps).
2. `automation.get_flow` with the canvas, and `event_node` to read just one chain. Steps show what they do and whether they reach outside the Hub (an email, an outside address). Secret values are hidden.
3. `automation.runs` shows recent runs of a canvas, or one run in full. Use it to answer "why did this not send?".

## Proposing a flow
1. Understand the goal in one sentence. Look at what exists first (`automation.get_flow`) so you do not duplicate a flow.
2. `automation.reference` with `what: events` (find the event and its `change_types`), then `what: steps` for each kind of step you need, so the setting keys are right.
3. Build the proposal with `automation.propose_flow`: the canvas the event belongs on, a plain one-line `summary`, new `nodes` (each with a short `ref`, a `type`, `name` and `config`; an event node is type `trigger` with `config.event`), and `edges` (from and to are refs or existing ids; a condition connects with `handle` true or false). Typical shape: event, then a condition on `change.type`, then the action.
4. Emails: write to the agency's own notification address (`{{agency.notification_email}}`) unless the person named a recipient. Never send to customers unless the person said exactly who and why. Use `{{agency.brand.*}}` colours, not typed hex values.
5. A person approves it on a card. After approval, say plainly: **the flow is created but it is switched OFF, and they must go to Settings > Automation > Canvas and switch the new event on.** Never say it is running.

## Limits
You cannot switch an event on, delete steps or flows, or fill in secrets (API keys, headers): say that a person must. Nothing is removed by a proposal; it only adds steps and edits settings.

These steps use the WP Easy Hub's tools (automation.canvases, automation.get_flow, automation.reference, automation.runs, automation.propose_flow), available when the Hub is connected as an MCP server.
