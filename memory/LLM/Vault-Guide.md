---
type: guide
status: active
created: 2026-11-04
tags: [meta, guide]
---

# Vault Guide

This folder is the Obsidian vault **LLM**, located at `C:\Users\New User\Desktop\AI\memory\LLM`. Open it with **Obsidian > Open folder as vault**.

## Folder map
| Folder | Purpose | Note type |
|---|---|---|
| `00_Inbox/` | Default location for every new note. Triage weekly. | any |
| `01_Daily/` | One note per day, named `YYYY-MM-DD`. | `daily` |
| `02_Projects/` | Things with an outcome and an end date. One note (or folder) each. | `project` |
| `03_Areas/` | Ongoing responsibilities: `Sales/`, `AI-Workflows/`. | `area`, `note` |
| `04_Resources/` | Reusable knowledge: `Prompts/`, `Reference/`, `Snippets/`. | `prompt`, `reference` |
| `05_Archive/` | Finished or dormant material. Move, never delete. | any |
| `06_Attachments/` | Images, PDFs, audio pasted into notes. | n/a |
| `_Meta/` | Templates and vault rules. | n/a |
| `AI\sales research\` (outside vault) | Raw sales research files. Notes about it go in `03_Areas/Sales/`. | n/a |

## Workflow (capture, process, use)
1. **Capture**: everything lands in `00_Inbox/` as a note from a template.
2. **Process** (weekly, 15 min): give each note a `type`, tags and at least one `[[link]]`, then move it to its folder.
3. **Use**: pull notes into projects with links and embeds. Review `Home` and active projects daily.
4. **Archive**: when a project is done set `status: done` and move it to `05_Archive/`.

## Rules
- One idea per note. Link rather than copy.
- Every note has frontmatter properties (see [[Obsidian-Formats]]).
- Prefer links to folders for navigation; use folders only for broad grouping.
- Names and tags follow [[Tagging-and-Naming]].

## Graph view colours
Set in Graph view > Groups. A node takes the colour of the **first** group it matches, top to bottom.

| Colour | Group | Query |
|---|---|---|
| Gold | Hubs and Home | `tag:#moc` |
| Light grey | Vault guides and templates | `tag:#meta OR path:"_Meta"` |
| Orange | Decisions | `tag:#decision` |
| Red | Security | `tag:#security` |
| Blue | Projects | `path:"02_Projects"` |
| Green | Sales | `path:"03_Areas/Sales"` |
| Purple | AI workflows | `path:"03_Areas/AI-Workflows"` |
| Teal | Resources | `path:"04_Resources"` |
| Slate | Daily notes | `path:"01_Daily"` |
| Pink | Inbox (to triage) | `path:"00_Inbox"` |
| Dark grey | Archive | `path:"05_Archive"` |

So a decision inside a project shows orange, and the security audit and demo show red, not blue.

## See also
[[Home]] · [[Instructions]] · [[Obsidian-Formats]] · [[Tagging-and-Naming]] · [[Claude-Workflow]] · [[CLAUDE]]

## Setup checklist
- [ ] Restart Obsidian once so it picks up the new settings (inbox for new notes, templates, ignore rules)
- [ ] Settings > Core plugins: confirm *Daily notes*, *Templates*, *Properties*, *Bookmarks* are on (preconfigured)
- [ ] Optional community plugins: Dataview (queries), Templater (smarter templates), Tasks, Calendar
- [ ] Bookmark [[Home]]
