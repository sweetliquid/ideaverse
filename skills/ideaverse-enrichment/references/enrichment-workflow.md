# Lite 1.5 Enrichment Workflow

Use this when turning raw material into Ideaverse Lite 1.5 notes.

## 1. Intake

Ask what the material is:

- dated context or meeting note -> `Calendar`
- unclear mixed capture -> `+`
- durable idea -> `Atlas/Dots/Things`
- claim or principle -> `Atlas/Dots/Statements`
- external source -> `Atlas/Dots/Sources`
- person -> `Atlas/Dots/People`
- work support -> `Efforts/Notes`

Do not use `x` for captured knowledge. `x` is for templates, images, Excalidraw, and support files.

## 2. Search

Before creating notes:

1. Search exact titles and aliases.
2. Search likely terms in `Atlas`, `Calendar`, `Efforts`, and `+`.
3. Review relevant maps in `Atlas/Maps`.
4. Check existing source notes in `Atlas/Dots/Sources`.

Use Obsidian CLI when available:

```bash
obsidian search query="term"
obsidian backlinks file="Note Name"
```

Fallback:

```bash
rg -n "term" Atlas Calendar Efforts +
```

Do not assume QMD exists.

## 3. Classify

Choose the most useful durable note type:

| Material | Destination |
| --- | --- |
| rough clip | `+` |
| reusable concept/method/process | `Atlas/Dots/Things` |
| evergreen claim/principle | `Atlas/Dots/Statements` |
| article/book/video/paper/site | `Atlas/Dots/Sources` |
| person | `Atlas/Dots/People` |
| current project context | `Efforts/Notes` or an Effort note |
| dated record | `Calendar` |

## 4. Extract

For each durable idea:

1. Use one clear title.
2. Keep one main idea per note.
3. Add frontmatter:

```yaml
---
up:
  - "[[Relevant Map]]"
related: []
created: YYYY-MM-DD
in:
  - "[[Relevant Collection]]"
---
```

4. Use `in` only with collection notes that exist.
5. Link back to the source note or Calendar context.

## 5. Update Navigation

Update a map only when it improves navigation:

- maps and MOCs live in `Atlas/Maps`
- map notes use `in: ["[[Maps]]"]`
- dynamic views use `in: ["[[Views]]"]`
- raw extracted knowledge stays in `Atlas/Dots`

If there are only a few notes and no navigation pain, link from an existing broader map instead of creating a new map.

## 6. Finish

Before finishing:

- Source attribution is present.
- No duplicate was created.
- Ambiguous material remains in `+` with a short processing note.
- Durable notes are linked from a relevant map or source.
- No `+ Extras`, `Calendar/Days`, or generic Archive path was introduced.

## Batch Processing

For a group of clips or sources:

1. Put the raw batch in `+` or an Effort note.
2. Process the highest-value items first.
3. Create source notes only for sources worth re-finding.
4. Extract durable ideas into Atlas.
5. Leave low-value clips in `+` until deleted or clarified.
