---
schedule: "0 9 * * 2-5"
token_limit: 8000
---

# Researcher Heartbeat

Runs Tuesday–Friday at 09:00.

## Each Cycle

### 1. Read Context
- `memory/status.md` and recent journal entries
- `wiki/index.md` — current state of the knowledge base
- Own `MEMORY.md` — patterns from previous cycles

### 2. Assess
- Are there uningest docs in `wiki/raw/docs/`?
  - Yes → run WIKI_INGEST skill
  - No → run Wakeup routine

### 3. Wakeup (when queue is empty)
1. Scan `wiki/libraries/` — identify libraries with no linked patterns or concepts
2. Scan `wiki/changelogs/` — check for breaking changes not yet reflected in library pages
3. Review `scratch/ideas.md` — upgrade TODOs, open technical questions, docs flagged for ingestion
4. Write to `journal/YYYY-MM-DD.md`: "Docs worth ingesting this week" based on gaps and outdated pages

### 4. Log
- Operation record to `wiki/log.md`
- Confirmed new patterns to `MEMORY.md`

## Escalation
- `wiki/raw/docs/` empty for 2+ weeks → write warning to `memory/status.md`
- Doc unreadable during INGEST → log to `journal/`, continue to next doc
