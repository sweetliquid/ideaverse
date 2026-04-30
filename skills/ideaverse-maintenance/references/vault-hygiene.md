# Lite 1.5 Vault Hygiene

Maintenance should preserve the Lite 1.5 shape:

- `+` is an inbox.
- `x` is support.
- `Atlas/Maps` is navigation.
- `Atlas/Dots` is durable knowledge.
- `Calendar` is time.
- `Efforts` is action.

## Weekly

- Process old notes in `+`.
- Run broken-link checks.
- Review orphans.
- Spot-check new frontmatter.
- Move stale active work from `Efforts/On` to `Efforts/Simmering` or `Efforts/Sleeping` when appropriate.

## Monthly

- Run the full script suite.
- Review `Atlas/Maps` for bloat.
- Review squeeze points.
- Extract durable learnings from `Calendar` and `Efforts` into `Atlas/Dots`.
- Review support clutter in `x`.

## Handling Findings

### Broken Links

Fix the link, create the missing note only when it should exist, or remove the stale link.

### Orphans

For each orphan:

- link it from a relevant map
- move/process it through `+`
- delete if it is disposable
- leave it only if intentionally private or standalone

### Frontmatter

Durable notes should usually have:

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

Calendar and `+` notes may be lighter. Support files under `x` may be exempt.

### MOC Bloat

Maps are considered bloated when the direct link list is hard to scan. Split only when a child map improves navigation.

### Squeeze Points

Create a map when many notes point to the same concept and navigation is painful. Put the map in `Atlas/Maps` with `in: [[Maps]]`.

### Stale Work

Do not invent a generic Archive folder by default.

Use existing Effort states:

- current -> `Efforts/On`
- ongoing -> `Efforts/Ongoing`
- background -> `Efforts/Simmering`
- paused -> `Efforts/Sleeping`

Before moving work out of focus, extract reusable knowledge into Atlas.

## Health Report Shape

```markdown
# Vault Health Report - YYYY-MM-DD

## Summary

- Broken links:
- Orphans:
- Frontmatter issues:
- Map bloat:
- Squeeze points:
- Stale work:
- `+` inbox items:

## Recommended Actions

- [ ] Action
```
