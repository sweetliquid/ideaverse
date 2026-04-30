---
name: ideaverse-maintenance
description: Audit and maintain an Ideaverse Lite 1.5 Obsidian vault. Use when checking broken links, orphan notes, dead ends, frontmatter, MOC bloat, squeeze points, stale Efforts, unprocessed + inbox notes, or overall vault health while preserving the Lite 1.5 folder contract.
---

# Ideaverse Lite 1.5 Maintenance

Use this skill to keep an Ideaverse Lite 1.5 vault healthy without reshaping it into a generic Ideaverse layout.

The Lite 1.5 folder contract:

- `+` is the inbox/cooling pad and should be processed, not treated as extras.
- `x` is the support/toolbox layer and should be excluded from knowledge health audits unless the user asks.
- `Atlas/Maps` contains maps, MOCs, and views.
- `Atlas/Dots` contains durable knowledge, sources, people, and statements.
- `Calendar` contains dated records.
- `Efforts` contains active, ongoing, simmering, or sleeping work.

Before modifying an Obsidian vault, read the vault root `AGENTS.md` if it exists. Vault-local instructions override this skill.

## Requirements

- Python 3.8 or later.
- No external Python dependencies.
- Obsidian CLI is useful but optional.

## Quick Health Check

Prefer Obsidian CLI when Obsidian is open:

```bash
obsidian orphans
obsidian deadends
obsidian unresolved
obsidian backlinks file="Note Name"
```

If Obsidian CLI is unavailable, run the bundled scripts from this skill directory:

```bash
python3 scripts/find_broken_links.py /path/to/vault
python3 scripts/find_orphans.py /path/to/vault
python3 scripts/check_frontmatter.py /path/to/vault --strict
python3 scripts/detect_moc_bloat.py /path/to/vault
python3 scripts/validate_squeeze_points.py /path/to/vault
python3 scripts/suggest_archival.py /path/to/vault
```

Do not assume QMD is installed. Use semantic search tools only when the user has explicitly configured them.

## Script Behavior

The scripts are Lite 1.5 aware:

- Hidden agent/tool folders such as `.agents` are excluded.
- `x/Templates`, `x/Images`, `x/Excalidraw`, and other support paths are excluded from frontmatter expectations.
- `+` is included because inbox notes should eventually be processed.
- `Atlas/Maps` and `in: [[Maps]]` are treated as map indicators.
- Calendar date notes are allowed to have minimal frontmatter.
- No script should recommend creating `+ Extras` or `Calendar/Days`.

## Cadence

### Lightweight Weekly Sweep

1. Check broken links.
2. Check `+` for stale unprocessed captures.
3. Spot-check new notes for `created`, `up`, and `in` where appropriate.
4. Review orphan notes and decide whether to link, keep in `+`, or delete.

### Monthly Sweep

1. Run all bundled scripts.
2. Review map bloat in `Atlas/Maps`.
3. Review squeeze points and create maps only when structure is earned.
4. Review `Efforts/On` and `Efforts/Simmering` for items that should move to `Efforts/Sleeping`.
5. Extract reusable knowledge from Efforts and Calendar into Atlas.

## What To Do With Findings

- Broken links: fix target names, create missing notes only when the note should exist, or remove stale links.
- Orphans: link to a relevant map, keep in `+` for processing, or delete if disposable.
- Frontmatter issues: add `created`, `up`, and `in` according to Lite 1.5 conventions.
- MOC bloat: split only when the map is genuinely hard to navigate.
- Squeeze points: consider a new map in `Atlas/Maps`, but do not create empty taxonomy.
- Stale work: move Efforts between `On`, `Ongoing`, `Simmering`, and `Sleeping`; do not invent an Archive folder by default.

## Deep Dives

- [references/vault-hygiene.md](references/vault-hygiene.md)
- [references/troubleshooting.md](references/troubleshooting.md)
