# Frontmatter Reference: Ideaverse Lite 1.5

Ideaverse Lite 1.5 uses YAML frontmatter for navigation, relationship, and Dataview collection membership. The 1.5 release shifted collection logic toward properties, especially `in`, instead of relying on tags.

## Core Properties

### `up`

Parent map or parent context. Use the note this one belongs under.

```yaml
up:
  - "[[Meta PKM]]"
```

Most notes should have `up`. Root notes such as `Home` may omit it. Draft or unprocessed notes can use `up: []` until processed.

### `related`

Lateral links that are useful but not parent/child relationships.

```yaml
related:
  - "[[Adjacent Idea]]"
  - "[[Contrasting Idea]]"
```

Use an empty array when there are no known lateral links:

```yaml
related: []
```

### `created`

Creation date in `YYYY-MM-DD`.

```yaml
created: 2026-05-01
```

### `in`

Collection membership. In Lite 1.5 this powers many Dataview collection notes.

```yaml
in:
  - "[[Maps]]"
```

Common collection links:

- `[[Maps]]`
- `[[Views]]`
- `[[Sources]]`
- `[[Books]]`
- `[[Movies]]`
- `[[Papers]]`
- `[[Concepts]]`
- `[[Efforts]]`
- `[[Meta PKM]]`

Use the collection notes that actually exist in the vault.

### Other Properties

Use existing vault conventions when present:

- `rank`: priority ordering, especially for Efforts.
- `version`: kit/version notes.
- `modified`: manually maintained modified date when the note already uses it.
- `tags`: keep existing tags such as `x/readme`, but do not use tags as the primary Lite 1.5 collection mechanism.
- source-specific fields such as `year` or `encountered`.

## Examples

### Map or MOC

Maps live in `Atlas/Maps`.

```yaml
---
up:
  - "[[Home]]"
related:
  - "[[Adjacent Map]]"
created: 2026-05-01
in:
  - "[[Maps]]"
---
```

### View

Views are dynamic Dataview/search collection notes and usually live in `Atlas/Maps`.

```yaml
---
up:
  - "[[Home]]"
related:
  - "[[Maps]]"
created: 2026-05-01
in:
  - "[[Views]]"
---
```

### Thing or Concept Note

Durable ideas usually live in `Atlas/Dots/Things`.

```yaml
---
up:
  - "[[Thinking Map]]"
related: []
created: 2026-05-01
in:
  - "[[Concepts]]"
---
```

### Statement Note

Claim-like evergreen notes usually live in `Atlas/Dots/Statements`.

```yaml
---
up:
  - "[[Relevant Map]]"
related:
  - "[[Related Thing]]"
created: 2026-05-01
---
```

### Source Note

Sources live in `Atlas/Dots/Sources` and should link to source collections.

```yaml
---
up:
  - "[[Sources]]"
related: []
year: 2026
encountered: 2026-05-01
in:
  - "[[Sources]]"
---
```

For a book source, also include `[[Books]]` if that collection exists:

```yaml
in:
  - "[[Sources]]"
  - "[[Books]]"
```

### Effort Note

Efforts live under `Efforts/On`, `Efforts/Ongoing`, `Efforts/Simmering`, or `Efforts/Sleeping`.

```yaml
---
up:
  - "[[Efforts]]"
related: []
created: 2026-05-01
rank: 5
---
```

### Daily or Dated Note

Calendar notes should follow the vault's Daily Notes or Periodic Notes configuration.

```yaml
---
created: 2026-05-01
---
```

### Inbox Note in `+`

Use minimal metadata for unprocessed capture. Add richer metadata when processing.

```yaml
---
created: 2026-05-01
---
```

## Rules

1. Quote wikilinks in frontmatter: `"[[Note Name]]"`.
2. Use arrays for relationship properties, even with one item.
3. Prefer `in` over tags for collection membership in Lite 1.5.
4. Do not put inline relationship labels such as `Up: [[Note]]` in the body when frontmatter can express the relationship.
5. Match the existing note's property style when editing existing kit notes.
6. Do not invent absent collection notes unless the user asks or the MOC workflow clearly requires them.
