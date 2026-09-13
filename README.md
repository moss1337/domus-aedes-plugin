# Domus Aedes — property search in ChatGPT and Claude

Domus Aedes is a property agency in Spain and Morocco (Marbella, Benahavís, the Golden Mile, Sotogrande, Marrakech, Casablanca). This repository is the public plugin bundle that connects ChatGPT, Claude, Claude Code and Codex to the Domus Aedes property search server at **https://ai.domusaedes.com/mcp** — a remote MCP server with an interactive property view (photos, price, key facts, map, refinement chips, detail view and a request-details form).

No account, no API key, no OAuth. The server only ever reads Domus Aedes' own portfolio and, when you ask for it, forwards your contact details to a Domus Aedes advisor.

## The one rule: three options, never a list

Every search returns the **three best matches** for your brief plus a few ways to narrow it down (budget, area, bedrooms, features). Ask for more and the assistant refines the search with you instead of scrolling through pages. There is no pagination anywhere in the API — the server caps results at three.

## What you can ask

- *Domus Aedes: find me a villa to buy in Marbella under €3M with a pool and sea views.*
- *Domus Aedes: I need a place to stay in Marrakech for 4 guests, 12–19 October.*
- *Domus Aedes: what can I rent long-term in Nueva Andalucía for up to €8,000 a month with 3+ bedrooms?*

Then: "tell me more about the second one", "narrow it down to Benahavís", "send my details to an advisor".

## Install

### ChatGPT
1. Open ChatGPT → **Plugins** (or **Settings → Apps & connectors** / the tools menu) → search **Domus Aedes** → **Connect**.
2. Start your prompt with "Domus Aedes" the first time so the assistant picks the plugin.

Not listed yet? Turn on **Settings → Security and login → Developer mode**, go to https://chatgpt.com/plugins, press **+**, name it "Domus Aedes" and enter the public endpoint `https://ai.domusaedes.com/mcp`.

### Claude (claude.ai, Claude Desktop, mobile)
1. https://claude.ai/customize/connectors → **+** → **Add custom connector**.
2. Name **Domus Aedes**, URL `https://ai.domusaedes.com/mcp`, leave OAuth blank → **Add**.
3. In a chat press **+** → **Connectors** → enable Domus Aedes.

On Team and Enterprise plans an Owner adds it under **Organization settings → Connectors** and members enable it from **Customize → Connectors**.

### Claude Code
```
/plugin marketplace add moss1337/domus-aedes-plugin
/plugin install domus-aedes@domus-aedes
```
The plugin registers the `domus-aedes` MCP server and the `domus-property-search` skill. Restart Claude Code (or run `/reload-plugins`) and ask for a property.

### Codex / ChatGPT Work (local marketplace)
```
codex plugin marketplace add moss1337/domus-aedes-plugin
```
Then install **Domus Aedes** from the Plugins Directory under that marketplace source. The bundle lives in `chatgpt/`.

## Repository layout

```
.claude-plugin/marketplace.json   Claude Code marketplace (plugin "domus-aedes" → ./claude)
claude/                           Claude Code plugin: .claude-plugin/plugin.json, .mcp.json, skills/
chatgpt/                          OpenAI plugin bundle: plugin.json, mcp.json, skills/, .codex-plugin/ (compat)
LICENSE                           MIT
```

Both bundles ship the same skill, `skills/domus-property-search/SKILL.md`, which teaches the assistant the three-options workflow.

## Tools exposed by the server

| Tool | What it does |
|---|---|
| `search_properties` | Three best matches for a brief (buy / rent / stay), total matches, refinement suggestions. Read-only. |
| `get_property` | Full details for one reference: description, key facts, up to 12 photos, approximate location, listing page, live availability for stays with dates. Read-only. |
| `request_property_details` | Sends name, email, optional phone and a message to a Domus Aedes advisor. Not destructive, not idempotent. |

## Privacy

The server stores nothing about your conversation beyond the parameters of the tool call. Contact details are forwarded only when you ask for an advisor. Full policy: https://ai.domusaedes.com/privacy

## Contact

Domus Aedes · +34 930 34 46 10 · WhatsApp https://wa.me/34930344610 · contact@domusaedes.com · https://domusaedes.com

Server docs: https://ai.domusaedes.com/docs
