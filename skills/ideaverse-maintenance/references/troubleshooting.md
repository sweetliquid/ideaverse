# Lite 1.5 Troubleshooting

## Note Feels Lost

Check:

1. Does it belong in `+`, Calendar, Atlas, or Efforts?
2. Does it have `up`?
3. Is it linked from a relevant map?
4. Is it actually a source, person, statement, or effort note?

Fix:

- durable knowledge -> `Atlas/Dots`
- navigation -> `Atlas/Maps`
- ambiguous capture -> `+`
- dated context -> `Calendar`
- work context -> `Efforts`

## Missing Frontmatter

Durable notes usually need `created` and `up`. Maps and views should usually have `in`.

Example map:

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

Example concept:

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

## Orphan Notes

An orphan is not automatically bad.

Options:

- add it to a map
- add `up`
- leave it in `+` for processing
- delete it if disposable

Do not create a map solely to hide orphan warnings.

## Map Is Too Large

If a map in `Atlas/Maps` is hard to scan:

1. Identify the largest cluster.
2. Create a child map only if it will be reused.
3. Move grouped links under the child map.
4. Keep the parent map as navigation.

## Squeeze Point

A squeeze point means many notes reference one concept without a useful map.

Create a map when:

- the concept has enough durable notes
- navigation is painful
- the map will be used again

Do not create empty taxonomy maps.

## Stale Effort

If an Effort is stale:

- move `Efforts/On` -> `Efforts/Simmering` when it is background
- move to `Efforts/Sleeping` when paused
- keep `Efforts/Ongoing` for continuing responsibilities

Extract durable lessons into `Atlas/Dots` before moving or deleting effort material.

## Search Problems

Start from `Home`, `Home Basic`, `Ideaverse Map`, `Meta PKM`, `Maps`, and `Views`.

Use:

```bash
obsidian search query="term"
rg -n "term" Atlas Calendar Efforts +
```

Do not assume tags are the primary collection mechanism in Lite 1.5. Prefer `in` properties and map links.
