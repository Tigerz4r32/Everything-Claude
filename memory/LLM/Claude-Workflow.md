---
type: guide
status: active
created: 2026-11-04
tags: [meta, ai]
---

# Claude Workflow

How Claude Code works with this vault. The same rules are in [[CLAUDE]] (loaded automatically).

## Good requests
- "Triage `00_Inbox/`: add properties, tags, links, and move each note."
- "Create a lead note for <company> from `sales research/`."
- "Summarise this week's daily notes into a weekly review."

## Conventions Claude follows
- Use templates from `_Meta/Templates/`; keep all frontmatter fields.
- Use `[[wikilinks]]`, ISO dates, lowercase tags.
- Never delete: move to `05_Archive/`.
- Do not touch `.obsidian/workspace*.json`.

## Memory
Claude's own persistent memory is separate from this vault. Durable preferences go there; project knowledge goes in the vault.
