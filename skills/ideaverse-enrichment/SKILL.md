---
name: ideaverse-enrichment
description: Add new knowledge to an Ideaverse Lite 1.5 Obsidian vault without breaking the Lite 1.5 folder contract. Use when processing articles, books, videos, research, copied text, meeting takeaways, links, or user-provided ideas into notes; when checking for duplicates; or when deciding whether material belongs in +, Calendar, Atlas/Dots, Atlas/Maps, Sources, People, or Efforts.
---

# Ideaverse Lite 1.5 Enrichment

Use this skill to absorb new material into an Ideaverse Lite 1.5 vault. It assumes the core `ideaverse` skill's Lite 1.5 mapping:

- `+` is the Add inbox/cooling pad.
- `x` is the extras/toolbox support layer.
- `Atlas/Maps` holds maps, MOCs, and views.
- `Atlas/Dots/Things` holds reusable concepts, methods, definitions, and explanations.
- `Atlas/Dots/Statements` holds claim-like evergreen statements.
- `Atlas/Dots/Sources` holds source notes.
- `Atlas/Dots/People` holds people notes.
- `Calendar` holds dated notes and logs.
- `Efforts` holds active or paused work.

Before modifying an Obsidian vault, read the vault root `AGENTS.md` if it exists. Vault-local instructions override this skill.

## Enrichment Contract

When adding knowledge:

1. Search first.
2. Preserve source attribution.
3. Use `+` for ambiguous raw capture.
4. Extract durable knowledge into `Atlas/Dots`, not `x`.
5. Update maps in `Atlas/Maps` only when navigation improves.
6. Use Lite 1.5 frontmatter with `up`, `related`, `created`, and usually `in`.
7. Do not create `+ Extras`, `Calendar/Days`, generic Archive folders, or new taxonomy folders unless the user asks.

## ARC Enrichment Workflow

### 1. Add

Capture the raw material with the least destructive placement:

- Time-bound context, meeting notes, and today-specific observations go to `Calendar`.
- Unprocessed clips, mixed ideas, and uncertain material go to `+`.
- Clearly reusable concepts can go directly to `Atlas/Dots/Things`.
- External sources can go to `Atlas/Dots/Sources`.
- Active-work material can go to the relevant `Efforts` note or `Efforts/Notes`.

Always record where the material came from: URL, title, author, date encountered, page, timestamp, or the user's prompt context.

### 2. Relate

Before creating durable notes:

1. Search exact title and likely aliases.
2. Search `Atlas/Maps` for likely parent maps.
3. Check `Atlas/Dots/Sources` for an existing source note.
4. Decide the extraction type:
   - concept or method -> `Atlas/Dots/Things`
   - claim or principle -> `Atlas/Dots/Statements`
   - source -> `Atlas/Dots/Sources`
   - person -> `Atlas/Dots/People`
   - effort-specific support -> `Efforts/Notes`
5. Update an existing note if it already covers the same idea.
6. Create a new note only when the idea is distinct enough to reuse.

### 3. Communicate

After enrichment:

- Link extracted notes from their source note or dated context.
- Add a map entry only when the note improves that map.
- Mention the enrichment in today's Calendar note only when that note exists or the user wants an activity log.

## Knowledge Types

Use these placement defaults:

| Type | What It Is | Default Folder | Typical `in` |
| --- | --- | --- | --- |
| Concept | reusable idea, framework, definition, method | `Atlas/Dots/Things` | `[[Concepts]]` when appropriate |
| Statement | claim, principle, evergreen assertion | `Atlas/Dots/Statements` | usually parent-map driven |
| Process | repeatable workflow or how-to | `Atlas/Dots/Things` | `[[Concepts]]` or a domain map |
| Entity | tool, organization, product, place | `Atlas/Dots/Things` or a specific existing folder | existing collection if present |
| Person | person profile or relationship note | `Atlas/Dots/People` | `[[People Map]]` if appropriate |
| Source | book, article, paper, video, site | `Atlas/Dots/Sources` | `[[Sources]]`, plus `[[Books]]`, `[[Papers]]`, etc. |
| Effort material | notes useful mainly for a current responsibility | `Efforts/Notes` | effort-specific |

For templates and examples, read:

- [references/knowledge-classification.md](references/knowledge-classification.md)
- [references/extraction-templates.md](references/extraction-templates.md)

## Duplicate Detection

Use search in this order:

1. Obsidian CLI, if available: `obsidian search query="term"` and `obsidian backlinks file="Note Name"`.
2. Filesystem fallback: `rg -n "term" Atlas Calendar Efforts +`.
3. Manual map review: inspect likely maps in `Atlas/Maps`.

Do not assume QMD exists. Use it only if the user has explicitly configured it or asks for it.

When a duplicate is found:

- If new material is smaller than the existing note, update or link the existing note.
- If it supplements the existing note, merge the new insight into the existing note.
- If it is a neighboring but distinct idea, create a separate note and link through `related`.
- If uncertain, capture in `+` with a short dedup note.

Read [references/duplicate-detection.md](references/duplicate-detection.md) for the detailed merge process.

## Common Enrichment Workflows

### Article, Book, Video, or Web Page

1. Create or update a source note in `Atlas/Dots/Sources`.
2. Add source metadata and a short summary.
3. Extract 1-5 durable ideas.
4. Create or update notes in `Atlas/Dots/Things` or `Atlas/Dots/Statements`.
5. Link extracted notes from the source note.
6. Add source collection membership through `in`, such as `[[Sources]]`, `[[Books]]`, or `[[Papers]]`.

### User Idea or Conversation

1. If raw and ambiguous, capture in `+`.
2. If stable and reusable, create/update `Atlas/Dots/Things`.
3. If it is about how the vault works, prefer `Atlas/Dots/Things` with `up: [[Meta PKM]]`.
4. If it is action-oriented, create/update an Effort instead of forcing it into Atlas.

### Research Batch

1. Keep a temporary synthesis in `+` or `Efforts/Notes`.
2. Create source notes for durable references.
3. Extract atomic reusable notes.
4. Update or create a MOC in `Atlas/Maps` only when structure is earned.
5. Leave the synthesis note in place only if it remains useful as a map or work note.

## Validation Checklist

Before enrichment is complete:

- [ ] Existing notes were searched first.
- [ ] Source attribution is present.
- [ ] Durable knowledge is in `Atlas/Dots`, not `x`.
- [ ] Ambiguous capture is in `+`.
- [ ] Maps were updated only when useful.
- [ ] Frontmatter follows Lite 1.5 conventions.
- [ ] No `+ Extras` or `Calendar/Days` path was introduced.

## References

- [references/enrichment-workflow.md](references/enrichment-workflow.md)
- [references/knowledge-classification.md](references/knowledge-classification.md)
- [references/extraction-templates.md](references/extraction-templates.md)
- [references/duplicate-detection.md](references/duplicate-detection.md)
