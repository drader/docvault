# Wiki Schema — Constitution

This file is the wiki's constitution. The LLM follows these rules on every wiki write.

## Purpose

A permanent knowledge base for developer documentation. Domain: defined in CLAUDE.md.

## Folder Structure

| Folder | Content | Does NOT contain |
|---|---|---|
| `raw/docs/` | Raw docs, changelogs, RFCs, tutorials | Anything processed |
| `libraries/` | One page per library or framework | Individual version diffs |
| `patterns/` | Design patterns and architectural approaches | Library-specific APIs |
| `concepts/` | Programming concepts (memoization, SSR, etc.) | Specific library APIs |
| `changelogs/` | Version-specific change summaries (one file per version) | Full library overview |
| `syntheses/` | Cross-library comparisons, migration guides | Raw doc summaries |
| `archive/` | Retired pages — never deleted | Active content |
| `_seed/` | Starter template pages — can be deleted after setup | Real knowledge |

## Library Page Format

```markdown
---
library: react
latest_version: "18.3.0"
tags: [frontend, ui, javascript]
source: raw/docs/react-18-docs.md
date: YYYY-MM-DD
status: active
---

# React

One-paragraph overview of the library's purpose and ecosystem position.

## Key APIs
- `useState` — local state in function components
- `useEffect` — side effects and cleanup

## Patterns
- [[patterns/compound-components]]
- [[patterns/render-props]]

## Anti-Patterns
- Patterns the docs explicitly warn against

## Gotchas
- Non-obvious behavior to be aware of

## Version History
| Version | Breaking Changes | Notes |
|---|---|---|
| 18.3.0 | No | [[changelogs/react-v18.3.0]] |
| 18.0.0 | Yes | [[changelogs/react-v18.0.0]] — concurrent mode default |

## CONFLICT (if any)
[[changelogs/react-v18.0.0]] says X while [[changelogs/react-v17.0.0]] implies Y. Unresolved — YYYY-MM-DD.

## Sources
- [[raw/docs/filename]]

## Related
- [[libraries/react-router]]
- [[concepts/virtual-dom]]
- [[patterns/compound-components]]
```

## Changelog Page Format

```markdown
---
library: react
version: "18.0.0"
date: YYYY-MM-DD
has_breaking_changes: true
tags: [react, major-release]
source: raw/docs/react-18-changelog.md
status: active
---

# React v18.0.0

## ⚠ Breaking Changes
- List every breaking change explicitly

## New Features
- Feature 1

## Deprecations
- Deprecated API → replacement

## Migration Steps
Step-by-step migration from the previous version.

## Gotchas
Non-obvious issues discovered during migration.

## Sources
- [[raw/docs/filename]]

## Related
- [[libraries/react]]
```

## Naming Conventions

- File names: kebab-case
- Library pages: canonical library name (`react.md`, `prisma.md`, `fastapi.md`)
- Pattern pages: canonical pattern name (`compound-components.md`)
- Concept pages: canonical concept name (`server-side-rendering.md`)
- Changelog pages: `library-name-vX.Y.Z.md` (e.g., `react-v18.0.0.md`)

## Hard Rules

1. `raw/` is never modified — read only
2. Every claim cites a source doc — unsourced claims are forbidden
3. Breaking changes are always explicitly flagged — never buried in prose
4. Conflicts are flagged with `## CONFLICT`, never deleted
5. Pages are never deleted — moved to `archive/`, status: archived
6. Bidirectional links are required: if A links to B, B must list A in `## Related`
7. Every operation is logged to `log.md`
