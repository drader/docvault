# Skill: WIKI_INGEST

New doc → structured wiki page.

## Trigger
A file exists in `wiki/raw/docs/` with no corresponding page in `wiki/libraries/` or `wiki/changelogs/`.

## Steps

1. Find the most recently modified uningest file in `wiki/raw/docs/`
2. Read the doc. Identify its type, then extract accordingly:

   **Changelog / Release notes:**
   - Library name and version
   - Breaking changes (flag prominently — these are the most critical)
   - New APIs or features added
   - Deprecated APIs
   - Migration steps if provided
   - Gotchas or known issues

   **API reference / Guide / Tutorial:**
   - Library name and version this applies to
   - Key APIs, functions, or hooks documented
   - Patterns demonstrated (how to use X correctly)
   - Common mistakes or anti-patterns mentioned
   - Dependencies or peer requirements
   - Concepts explained

   **RFC / Proposal:**
   - Library or ecosystem it targets
   - Problem being solved
   - Proposed solution and trade-offs
   - Status (proposed / accepted / rejected)
   - Open questions

3. **For changelogs:** write `wiki/changelogs/library-name-vX.Y.Z.md`
   - Frontmatter: library, version, date, has_breaking_changes, tags, source, status: active
   - Sections: Breaking Changes, New Features, Deprecations, Migration Steps, Gotchas
   - Update `wiki/libraries/library-name.md` — add version entry, flag breaking changes

   **For guides/APIs/RFCs:** write or update `wiki/libraries/library-name.md`
   - Frontmatter: library, version, doc_type, tags, source, date, status: active
   - Sections: Overview, Key APIs, Patterns, Anti-Patterns, Gotchas, Related

4. For each design pattern demonstrated: create or update `wiki/patterns/pattern-name.md`
5. For each programming concept explained: create or update `wiki/concepts/concept-name.md`
6. Update `wiki/index.md` — add new pages to the relevant categories
7. Write to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD] ingest | library-name vX.Y.Z (type)
   Pages touched: libraries/X, changelogs/Y, patterns/Z
   Breaking changes: yes/no
   ```

## Rules
- Never modify files in `wiki/raw/` — read only
- Breaking changes must always be explicitly flagged in the changelog page and reflected in the library page
- If a doc for this library version already exists: update it, do not create a new one
- If a doc is unreadable: log to `journal/`, skip, continue to next doc
- All wiki writes go through the locker
