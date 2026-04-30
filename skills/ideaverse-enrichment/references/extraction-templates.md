# Lite 1.5 Extraction Templates

Use these shapes as defaults. Preserve existing local style when editing existing notes.

## Concept Or Method

Location: `Atlas/Dots/Things`

```markdown
---
up:
  - "[[Relevant Map]]"
related: []
created: YYYY-MM-DD
in:
  - "[[Concepts]]"
---

# Title

One or two sentences stating the idea.

## Core Idea

- The useful explanation.

## Use Cases

- Where this applies.

## Connections

- [[Related Note]] - why it matters.
```

## Statement Or Principle

Location: `Atlas/Dots/Statements`

```markdown
---
up:
  - "[[Relevant Map]]"
related: []
created: YYYY-MM-DD
---

# Statement Title

State the claim clearly.

## Why It Matters

- Reasoning or evidence.

## Boundaries

- When this does not apply.
```

## Source

Location: `Atlas/Dots/Sources`

```markdown
---
up:
  - "[[Sources]]"
related: []
year:
encountered: YYYY-MM-DD
in:
  - "[[Sources]]"
---

# Source Title

Author / URL / publication context.

## Summary

- Short summary.

## Extracted Notes

- [[Extracted Idea]]

## Highlights

- Quoted or paraphrased highlights with location.
```

## Person

Location: `Atlas/Dots/People`

```markdown
---
up:
  - "[[People Map]]"
related: []
created: YYYY-MM-DD
---

# Person Name

One-line context.

## Identity

- Role or relationship.

## Connections

- [[Related Note]]
```

## Effort Support Note

Location: `Efforts/Notes` unless the note is itself an effort.

```markdown
---
up:
  - "[[Effort Name]]"
related: []
created: YYYY-MM-DD
---

# Note Title

## Context

- Why this matters for the effort.

## Notes

- Working material.

## Reusable Knowledge To Extract

- [[Potential Atlas Note]]
```

## Inbox Capture

Location: `+`

```markdown
---
created: YYYY-MM-DD
---

# Capture Title

Raw capture.

## Processing Notes

- Possible destination:
- Possible duplicate:
- Source:
```

## Quality Checklist

- [ ] Correct Lite 1.5 folder.
- [ ] Source attribution when relevant.
- [ ] `created` present.
- [ ] `up` present for durable notes.
- [ ] `in` uses existing collection notes.
- [ ] No `+ Extras`, `Calendar/Days`, or generic Archive path.
