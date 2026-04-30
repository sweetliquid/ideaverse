# Ideaverse Lite 1.5 Workflows

These workflows adapt ARC (Add -> Relate -> Communicate) to the Lite 1.5 folder layout.

## Table of Contents

1. [Capture](#capture)
2. [Process the + Inbox](#process-the--inbox)
3. [Create Durable Atlas Notes](#create-durable-atlas-notes)
4. [Create and Evolve MOCs](#create-and-evolve-mocs)
5. [Maintain Calendar Notes](#maintain-calendar-notes)
6. [Manage Efforts](#manage-efforts)
7. [Cross-Reference Discovery](#cross-reference-discovery)

## Capture

Goal: get information into the vault without forcing a permanent structure too early.

Use this placement order:

1. If the note is about today, a meeting, a log, or a timestamped event, use `Calendar`.
2. If the placement is unclear, use `+`.
3. If it is clearly durable knowledge with an obvious parent map, create it in `Atlas/Dots`.
4. If it is clearly active work, create or update an `Efforts` note.

Do not use `x` for captured knowledge. `x` is for support files such as templates and images.

## Process the `+` Inbox

The `+` folder is the Add cooling pad. Process it periodically.

For each item:

1. Read the note and identify what it really is.
2. Search the vault for existing notes with the same idea.
3. Choose one outcome:
   - move to `Calendar` if it is time-bound
   - move to `Atlas/Dots/Things` if it is a reusable concept or method
   - move to `Atlas/Dots/Statements` if it is a claim or proposition
   - move to `Atlas/Dots/Sources` if it is a source
   - move to `Efforts/Notes` or an effort status folder if tied to active work
   - delete if it no longer has value
4. Add or update frontmatter after moving.
5. Link it from a relevant map if it has durable value.

If still unsure, leave it in `+` and add a short note explaining what decision remains.

## Create Durable Atlas Notes

Use this flow for stable knowledge:

1. Search before creating.
2. Read likely parent maps in `Atlas/Maps`.
3. Decide the Atlas subfolder:
   - `Atlas/Maps` for MOCs, views, navigation hubs
   - `Atlas/Dots/Things` for reusable concepts, methods, definitions
   - `Atlas/Dots/Statements` for claim-like evergreen notes
   - `Atlas/Dots/Sources` for external sources
   - `Atlas/Dots/People` for people
4. Create a clear title.
5. Add Lite 1.5 frontmatter.
6. Add the note to the relevant MOC or collection when appropriate.
7. Add meaningful links to related notes.

### Atomic Note Shape

```markdown
# [Clear Note Title]

One or two sentences that state the core idea.

## Notes

- Supporting detail.
- Important context.

## Connections

- [[Related Note]] - why it matters.
```

Keep the shape flexible. Match existing local style when editing existing notes.

## Create and Evolve MOCs

MOCs and Views live in `Atlas/Maps`.

Create a MOC when:

- the user explicitly asks for one
- a topic has about 10 related notes and no useful navigation
- repeated search/navigation friction shows a real squeeze point
- an existing map is too broad and needs a child map

Do not create empty taxonomy maps just because a category could exist.

### MOC Creation Procedure

1. Search for related notes.
2. Read neighboring maps.
3. Create the map in `Atlas/Maps`.
4. Use `in: ["[[Maps]]"]`.
5. Group links under simple headings.
6. Add short context after links when useful.
7. Update child notes' `up` property only when this map is their parent context.

### MOC Template

```yaml
---
up:
  - "[[Home]]"
related: []
created: YYYY-MM-DD
in:
  - "[[Maps]]"
---
```

```markdown
# [Topic] Map

Briefly describe what this map helps navigate.

## Core Notes

- [[Note A]] - short context.
- [[Note B]]

## Related Areas

- [[Related Map]]
```

### View Template

Use a View when the main value is a dynamic Dataview/search result.

```yaml
---
up:
  - "[[Home]]"
related:
  - "[[Maps]]"
created: YYYY-MM-DD
in:
  - "[[Views]]"
---
```

## Maintain Calendar Notes

Calendar holds timestamped notes. Preserve the vault's current Daily Notes or Periodic Notes configuration instead of inventing a new folder such as `Calendar/Days`.

Good Calendar content:

- daily notes
- meeting notes
- workout or tracking notes
- logs
- dated planning and review
- decisions made on a specific day
- links to notes created or updated that day

Extract durable knowledge out of Calendar into Atlas when it becomes reusable.

### Daily Note Shape

Use the vault's template if configured. The Lite 1.5 kit template is simple:

```yaml
---
created: YYYY-MM-DD
---
```

```markdown
## Freewrite

## Big Things Today

## Log
```

## Manage Efforts

Use Efforts for work that has action, priority, or responsibility.

Placement:

- `Efforts/On`: active focused work
- `Efforts/Ongoing`: ongoing responsibilities
- `Efforts/Simmering`: background work
- `Efforts/Sleeping`: paused work
- `Efforts/Notes`: supporting material for efforts

When creating an effort:

1. Choose the intensity folder.
2. Use `up: ["[[Efforts]]"]`.
3. Add `rank` if the Efforts view should sort it.
4. Link supporting notes.
5. Keep reusable ideas in Atlas and link them from the effort.

When completing or pausing an effort:

1. Add a short summary.
2. Extract reusable knowledge into Atlas.
3. Move the effort to the appropriate folder.
4. Update the `[[Efforts]]` map only if needed.

## Cross-Reference Discovery

After creating or updating a note:

1. Identify key concepts, people, sources, and efforts mentioned.
2. Search for existing notes by exact title and likely aliases.
3. Add useful links from the new note.
4. Add a backlink or MOC entry only when it improves navigation.
5. If a term appears repeatedly without a map, consider a future MOC.

Avoid link spam. A link should help a future reader move through the vault.

## Safety Checklist

Before making structural changes:

- Search first.
- Do not rename, delete, or reorganize kit/example notes unless explicitly asked.
- Do not create `+ Extras`.
- Do not put support files in `+`.
- Do not put raw atomic notes in `Atlas/Maps`.
- Preserve existing frontmatter style when editing existing notes.
- If unsure, capture in `+` and explain what remains ambiguous.
