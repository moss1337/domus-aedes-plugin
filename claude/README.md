# Domus Aedes — Claude Code plugin

Adds Domus Aedes property search to Claude Code: one remote MCP server (no auth) and one skill.

## Install

```
/plugin marketplace add moss1337/domus-aedes-plugin
/plugin install domus-aedes@domus-aedes
```

CLI equivalent:

```
claude plugin marketplace add moss1337/domus-aedes-plugin
claude plugin install domus-aedes@domus-aedes
```

Restart Claude Code or run `/reload-plugins`. Update later with `/plugin marketplace update domus-aedes` then `/plugin update domus-aedes@domus-aedes`.

## What is inside

```
.claude-plugin/plugin.json                 manifest (name domus-aedes, version 0.1.0)
.mcp.json                                  domus-aedes → https://ai.domusaedes.com/mcp (streamable HTTP)
skills/domus-property-search/SKILL.md      the three-options workflow
```

- **MCP server `domus-aedes`** exposes `search_properties`, `get_property` and `request_property_details`. The first two are read-only; the third sends your contact details to a Domus Aedes advisor and only runs when you ask for it.
- **Skill `domus-property-search`** loads automatically when you talk about buying, renting or staying in Spain or Morocco. Invoke it directly with `/domus-aedes:domus-property-search`.

## Try it

- "Find me a villa to buy in Marbella under €3M with a pool and sea views."
- "I need a place to stay in Marrakech for 4 guests, 12–19 October."
- "What can I rent long-term in Nueva Andalucía for up to €8,000 a month?"

You always get three options. Say "more" and Claude offers ways to narrow the search instead of listing more.

## Validate

```
claude plugin validate .
```

## Privacy

https://ai.domusaedes.com/privacy — nothing is stored beyond the tool parameters; contact details are forwarded only via `request_property_details`.

Support: contact@domusaedes.com · +34 930 34 46 10
