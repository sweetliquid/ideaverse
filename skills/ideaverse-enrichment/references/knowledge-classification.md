# Lite 1.5 Knowledge Classification

Classify material by how it will be reused.

## Concept Or Method

Abstract idea, framework, definition, workflow, or reusable explanation.

Default location: `Atlas/Dots/Things`

Typical frontmatter:

```yaml
---
up:
  - "[[Relevant Map]]"
related: []
created: YYYY-MM-DD
in:
  - "[[Concepts]]"
---
```

Use `[[Concepts]]` only if the vault has that collection and the note belongs there.

## Statement Or Principle

Claim-like evergreen note, heuristic, belief, or proposition.

Default location: `Atlas/Dots/Statements`

Typical frontmatter:

```yaml
---
up:
  - "[[Relevant Map]]"
related: []
created: YYYY-MM-DD
---
```

## Source

Book, article, paper, video, web page, podcast, course, or other external material.

Default location: `Atlas/Dots/Sources`

Typical frontmatter:

```yaml
---
up:
  - "[[Sources]]"
related: []
year:
encountered: YYYY-MM-DD
in:
  - "[[Sources]]"
---
```

Add narrower collections when they exist: `[[Books]]`, `[[Papers]]`, `[[Movies]]`, `[[Songs]]`, `[[Courses]]`.

## Person

Person profile, collaborator, author, or historical figure.

Default location: `Atlas/Dots/People`

Typical frontmatter:

```yaml
---
up:
  - "[[People Map]]"
related: []
created: YYYY-MM-DD
---
```

## Effort Material

Task notes, implementation notes, project context, or decision records useful mainly for a current responsibility.

Default location:

- `Efforts/Notes` for supporting material
- `Efforts/On`, `Efforts/Ongoing`, `Efforts/Simmering`, or `Efforts/Sleeping` for effort notes

Extract reusable concepts from Efforts into Atlas.

## Calendar Material

Daily notes, meetings, logs, dated observations, and time-bound plans.

Default location: `Calendar` or the vault's configured Calendar subfolder.

Do not invent `Calendar/Days` unless the vault already uses it.

## Inbox Material

Unprocessed clips, ambiguous notes, mixed sources, and ideas that need cooling time.

Default location: `+`

When processing, move or rewrite into the proper Atlas, Calendar, or Efforts location.

## Support Material

Templates, images, Excalidraw files, utilities, and vault support notes.

Default location: `x`

Do not put knowledge notes here just because they are miscellaneous.
