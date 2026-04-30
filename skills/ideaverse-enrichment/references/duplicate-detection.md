# Lite 1.5 Duplicate Detection

Search before creating durable notes.

## Search Order

1. Exact title and likely aliases.
2. Existing source notes in `Atlas/Dots/Sources`.
3. Relevant maps in `Atlas/Maps`.
4. Full-text search across `Atlas`, `Calendar`, `Efforts`, and `+`.

Use Obsidian CLI when available:

```bash
obsidian search query="concept name"
obsidian backlinks file="Related Note"
```

Fallback:

```bash
rg -n "concept name" Atlas Calendar Efforts +
```

Do not assume QMD exists.

## Near-Duplicate Signals

Potential duplicate:

- same title or alias
- same source being summarized again
- same claim with different wording
- same process with a slightly different name
- new note would use the same parent map and same key links

Probably distinct:

- one is a source, the other is an extracted idea
- one is a general concept, the other is a specific example
- one is a person/entity, the other is a process or principle
- the notes should be linked through `related` instead of merged

## Resolution

When duplicate coverage exists:

1. Prefer updating the existing note.
2. Add the new source/context as a section or bullet.
3. Preserve the better title.
4. Keep source attribution.
5. Update maps in `Atlas/Maps` to point to the primary note.
6. Delete the secondary note only when it is clearly redundant and the user is comfortable with deletion.

If uncertain, capture the new material in `+` and add a short note:

```markdown
Possible duplicate of [[Existing Note]]. Needs review before extraction.
```

## Merge Checklist

- [ ] Existing and new notes really cover the same idea.
- [ ] Unique content was moved to the primary note.
- [ ] Links and map entries point to the primary note.
- [ ] Source attribution survived the merge.
- [ ] No unsupported Archive folder was created.
