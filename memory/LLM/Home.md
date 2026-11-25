---
type: moc
status: active
created: 2026-11-04
tags: [moc, home]
---

# Home

Entry point for the AI vault. Pin this note in Obsidian (Bookmarks).

## Navigate
- [[Instructions]]: step-by-step how to use the vault and templates
- [[Vault-Guide]]: how the vault is organised and how to work in it
- [[Obsidian-Formats]]: note formats, properties, links, tags, callouts
- [[Tagging-and-Naming]]: tag taxonomy and file naming rules
- [[Claude-Workflow]]: how to use Claude Code with this vault

## Areas
- [[Sales-Research-Hub]]: sales research notes and leads
- [[AI-Workflows-Hub]]: prompts, agents, automations

## Templates
[[Daily]] · [[Project]] · [[Note]] · [[Meeting]] · [[Sales-Lead]] · [[Prompt]] · [[Decision]] · [[Area-Hub]]

## Working set
- Capture new thoughts in `00_Inbox/`, triage weekly
- Today's note: use the *Daily notes* command (`01_Daily/`)
- Active projects live in `02_Projects/`

## Active projects
- [[Project - Airtronic Pricing Tool]]
- [[Project - Airtronic Market Pricing Review]] (waiting)

```dataview
TABLE status, due
FROM "02_Projects"
WHERE status = "active"
SORT due ASC
```
> The block above needs the optional **Dataview** community plugin. Without it, browse `02_Projects/` instead.
