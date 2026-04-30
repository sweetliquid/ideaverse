---
name: ideaverse
description: Work with Ideaverse Lite 1.5 Obsidian vaults using ACE, ARC, MOCs, and the current Lite 1.5 folder contract. Use whenever creating notes, organizing knowledge, deciding where a note belongs, updating Home/Home Basic, building Maps of Content, processing the + inbox, maintaining Calendar notes, managing Efforts, or adding source/knowledge notes in an Ideaverse Lite 1.5 vault.
---

# Ideaverse Lite 1.5 Methodology

Use this skill for Ideaverse Lite 1.5 vaults. It adapts the general LYT and ACE methodology to the current Lite 1.5 folder layout:

- `Atlas`
- `Calendar`
- `Efforts`
- `+`
- `x`

The important Lite 1.5 correction: `+` is the Add inbox/cooling pad. It is not the extras folder. The support/extras toolbox is `x`.

Before modifying an Obsidian vault, read the vault root `AGENTS.md` if it exists and let it override this skill for local conventions.

## Core Framework: ACE + Add + x

ACE organizes notes by intention, not by rigid topic hierarchy.

| Folder | Purpose | Question | Orientation |
| --- | --- | --- | --- |
| `Atlas/` | Durable knowledge, maps, concepts, sources, people | "Where would you like to go?" | Space and relatedness |
| `Calendar/` | Dated notes, logs, meetings, time-bound records | "What's on your mind?" | Time and reflection |
| `Efforts/` | Active or paused work, goals, responsibilities | "What can you work on?" | Action and importance |
| `+/` | Add inbox, cooling pad, unprocessed capture | "What came in recently?" | Capture |
| `x/` | Templates, images, Excalidraw, utilities, vault support | "What supports this vault?" | Infrastructure |

Do not create or use a `+ Extras/` folder in Lite 1.5. Use `+` for inbox captures and `x` for support files.

## Folder Placement Rules

### Atlas

Use `Atlas` for durable, reusable knowledge.

- `Atlas/Maps/`: MOCs, maps, views, topic hubs, navigation pages.
- `Atlas/Dots/Things/`: stable concepts, methods, definitions, reusable explanations.
- `Atlas/Dots/Statements/`: claim-like notes or proposition-style evergreen statements.
- `Atlas/Dots/Sources/`: books, articles, videos, papers, websites, and other source notes.
- `Atlas/Dots/People/`: people notes.
- `Atlas/Dots/X/`: kit/example support notes already present in the vault. Do not expand this as the main extras area unless the vault already uses it that way.

When a note is reusable beyond today's context or a single effort, it belongs in Atlas. Put navigation structures in `Atlas/Maps`; put atomic knowledge in `Atlas/Dots`.

### Calendar

Use `Calendar` for timestamped context:

- daily notes
- meeting notes
- logs
- planning/review notes
- time-bound observations

Preserve the vault's existing Daily Notes or Periodic Notes configuration. In Lite 1.5 examples, dated notes may appear in `Calendar`, `Calendar/Notes`, or `Calendar/Notes/Past Years`; do not invent `Calendar/Days` unless the vault already uses it.

### Efforts

Use `Efforts` for work and responsibilities:

- `Efforts/On/`: current focused efforts.
- `Efforts/Ongoing/`: continuing responsibilities.
- `Efforts/Simmering/`: background or lower-priority efforts.
- `Efforts/Sleeping/`: paused efforts.
- `Efforts/Notes/`: supporting notes tied to specific efforts.

Extract reusable learnings from Efforts into Atlas and link back to the effort.

### `+`

Use `+` as the Add inbox/cooling pad. Put new captures here when placement is unclear or when the user wants low-friction capture first. Later, process items from `+` into Atlas, Calendar, or Efforts.

### `x`

Use `x` as the Lite 1.5 support layer:

- `x/Templates/`: note templates.
- `x/Images/`: images and attachments.
- `x/Excalidraw/`: Excalidraw files.
- other vault utilities, archived support material, or meta support files.

Do not put durable knowledge here just because it is "miscellaneous." If it is knowledge, place it in Atlas.

## ARC Workflow

### 1. Add

Capture first:

- Use today's Calendar note for dated context.
- Use `+` for unprocessed ideas and ambiguous placement.
- Use a direct Atlas note only when the note type and parent map are already clear.

Avoid restructuring during capture.

### 2. Relate

Before creating a durable note:

1. Search for an existing note with the same or similar concept.
2. Read likely parent maps in `Atlas/Maps`.
3. Decide the note type: map, view, thing, statement, source, person, calendar note, or effort.
4. Add Lite 1.5 frontmatter with `up`, `related`, `created`, and usually `in`.
5. Add the note to the relevant MOC or collection when appropriate.

Prefer updating an existing note when it clearly represents the same idea.

### 3. Communicate

Use connected notes to produce outputs. Link or transclude existing notes instead of duplicating content. When an output or effort is complete, extract reusable knowledge into Atlas.

## MOCs and Views

In Lite 1.5:

- MOCs and navigation maps live in `Atlas/Maps`.
- Put `in: ["[[Maps]]"]` on maps.
- Put `in: ["[[Views]]"]` on Dataview-powered dynamic views.
- Use existing map names such as `[[Home]]`, `[[Home Basic]]`, `[[Ideaverse Map]]`, `[[Meta PKM]]`, `[[Maps]]`, `[[Views]]`, `[[Sources]]`, `[[Efforts]]`, and domain maps when they exist.

Create a new MOC only when structure is earned: repeated navigation pain, about 10 related notes, or a clear user request.

## Required Conventions

Use YAML frontmatter to express relationships and collection membership. Keep wikilinks quoted in arrays:

```yaml
---
up:
  - "[[Parent Map]]"
related: []
created: YYYY-MM-DD
in:
  - "[[Relevant Collection]]"
---
```

For detailed examples, read [references/frontmatter.md](references/frontmatter.md).

### Linking

- Use Obsidian wikilinks for internal references: `[[Page Name]]` or `[[Page Name|Alias]]`.
- Use markdown links only for external URLs.
- Add links where they help navigation or future reuse.

### Style

- Preserve existing note style when editing existing kit notes.
- Keep new notes focused and reusable.
- Use clear descriptive titles.
- Do not rename, delete, or reorganize kit/example notes unless explicitly asked.

## Key Workflows

For detailed procedures, read [references/workflows.md](references/workflows.md):

- capturing into `+` or Calendar
- processing the `+` inbox
- creating durable Atlas notes
- creating or evolving MOCs
- maintaining daily notes
- completing Efforts and extracting knowledge

## Common Pitfalls

| Pitfall | Symptom | Correction |
| --- | --- | --- |
| Treating `+` as extras | Templates or assets are placed in `+` | Use `x` for support files and `+` for inbox capture |
| Creating `+ Extras` | A non-Lite 1.5 support folder appears | Do not create it; use `x` |
| Dumping raw notes into Maps | `Atlas/Maps` becomes a pile of content | Put raw knowledge in `Atlas/Dots`; maps are navigation |
| Premature MOCs | Empty topic hubs appear before notes exist | Let structure emerge or use `+` first |
| Ignoring `in` | Dataview collections miss notes | Add `in` links such as `[[Maps]]`, `[[Views]]`, `[[Sources]]` |
| Losing effort learnings | Good ideas stay buried in project notes | Extract reusable pieces to Atlas and link back |
