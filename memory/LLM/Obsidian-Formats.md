---
type: guide
status: active
created: 2026-11-04
tags: [meta, obsidian, reference]
---

# Obsidian Formats

Reference for every format used in this vault. Notes are plain Markdown (`.md`), so they work in any editor and are easy for Claude to read and write.

## 1. Properties (frontmatter)
YAML block at the very top of a note, between `---` lines. Shown as the Properties panel.

```yaml
---
type: project            # note type, see table below
status: active           # draft | active | waiting | done | archived
created: 2026-11-04      # ISO date, always YYYY-MM-DD
due: 2026-12-01          # optional
tags: [sales, q4]        # lowercase, no spaces
aliases: [Q4 outreach]   # alternative names for linking
related: ["[[Other Note]]"]  # links inside properties must be quoted
---
```

| `type` | Used for | Template |
|---|---|---|
| `daily` | daily log | Daily |
| `project` | outcome with an end date | Project |
| `area` / `moc` | hub or map-of-content | Area-Hub |
| `note` | evergreen, one-idea knowledge note | Note |
| `meeting` | meeting record | Meeting |
| `lead` | sales lead or company research | Sales-Lead |
| `prompt` | reusable prompt | Prompt |
| `decision` | recorded decision (ADR style) | Decision |
| `guide` | vault documentation | none |

## 2. Links
| Syntax | Meaning |
|---|---|
| `[[Note]]` | link to note |
| `[[Note\|label]]` | link with display text |
| `[[Note#Heading]]` | link to a heading |
| `[[Note#^block-id]]` | link to a block (add `^block-id` at the end of a paragraph) |
| `![[Note]]` | embed whole note |
| `![[Note#Heading]]` | embed a section |
| `![[image.png]]` / `![[doc.pdf#page=3]]` | embed attachment |
| `[text](https://url)` | external link |

Wikilinks are the default (`useMarkdownLinks: false`), with shortest-path names.

## 3. Tags
Inline `#tag` or in the `tags` property. Nested with `/`: `#sales/lead`. See [[Tagging-and-Naming]].

## 4. Callouts
```markdown
> [!note] Title
> Body text
```
Types used here: `note`, `info`, `tip`, `warning`, `question`, `todo`, `quote`, `example`, `bug`.
Add `-` to collapse by default: `> [!tip]- Click to expand`.

## 5. Tasks
```markdown
- [ ] open task
- [x] done task
- [ ] task with due date 📅 2026-11-10
```
(Dates use the optional Tasks plugin emoji format.)

## 6. Other Markdown in use
- Headings `#` to `######` (one `#` H1 per note: the title)
- Tables with pipes, code fences with a language (` ```python `), `==highlight==`, `~~strike~~`
- Footnotes `[^1]`, comments `%% hidden %%`
- Diagrams: ` ```mermaid ` blocks render flowcharts and sequences
- Math: `$E=mc^2$` inline, `$$ ... $$` block

## 7. Canvas (`.canvas`)
Free-form boards for planning and mind-maps. Name them `Canvas - <topic>`. Store in the relevant project or area folder.

## 8. Dataview queries (optional plugin)
```dataview
TABLE status, due FROM "02_Projects" WHERE status != "done" SORT due ASC
```
Works because every note carries consistent properties.

## 9. Note anatomy
1. Frontmatter
2. `# Title` (matches filename)
3. One-paragraph summary
4. Body with `##` sections
5. `## Related` with `[[links]]`
