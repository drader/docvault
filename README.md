# docvault

An agentic developer documentation knowledge base. Drop library docs, changelogs, and RFCs in. Agents extract APIs, breaking changes, and patterns — linking libraries and concepts into a searchable reference that grows with your stack.

Built on [memex](https://github.com/drader/memex).

---

## What it does

You drop a doc into `wiki/raw/docs/`. The researcher agent — running on a schedule in the background — reads it, identifies its type, and produces:

- A **library page** (`wiki/libraries/`) with key APIs, patterns, anti-patterns, gotchas, and a version history table
- A **changelog page** (`wiki/changelogs/`) for each release — breaking changes are always flagged explicitly, never buried in prose
- **Pattern pages** (`wiki/patterns/`) for any design pattern demonstrated in the doc
- **Concept pages** (`wiki/concepts/`) for any programming concept explained in depth

Breaking changes in a new changelog are automatically reflected back into the library page's version history. When the queue is empty, the agent scans for libraries with outdated version entries and flags them in the journal.

---

## Wiki structure

```
wiki/
  raw/docs/       drop changelogs, API refs, RFCs, tutorials here
  libraries/      one page per library or framework
  changelogs/     one page per version (library-vX.Y.Z.md)
  patterns/       design patterns and architectural approaches
  concepts/       programming concepts (memoization, SSR, etc.)
  syntheses/      cross-library comparisons, migration guides
  archive/        retired pages (never deleted)
```

---

## Quick Start

### Prerequisites

- Node.js ≥ 20
- [Claude CLI](https://github.com/anthropics/claude-code) (`npm install -g @anthropic-ai/claude-code`)
- `obsidian-hybrid-search` (`npm install -g obsidian-hybrid-search`)

### Install

```bash
git clone https://github.com/drader/docvault my-docvault
cd my-docvault
npm install
```

### First run

```bash
npm run setup
```

Runs a 7-question intake interview. You list your stack, doc types you track, and the "I always have to look this up" questions in your codebase. The agent seeds stub pages for every library you name and Bootstrap Hypotheses based on your recurring questions.

### Start the daemon

```bash
npm start                # foreground
npm run dev              # watch mode
npm run install-daemon   # background daemon (launchd on macOS, systemd on Linux)
```

### Ingest a doc

```
/ingest
```

Or drop any file into `wiki/raw/docs/` — changelogs, API pages, tutorials, RFC text files. The daemon picks it up on the next cycle (Tue–Fri 09:00 by default) and routes it to the right wiki folder automatically based on content type.

---

## Slash Commands

| Command | What it does |
|---|---|
| `/ingest` | Process the next uningest doc in `wiki/raw/docs/` |
| `/query` | Ask a technical question, get a wiki-backed answer with source citations |
| `/lint` | Check wiki health: outdated versions, missing changelogs, orphan pages |
| `/setup` | First-time intake interview |
| `/session-start` | Load context, log session open |
| `/session-end` | Flush scratch notes, log session close |

---

## License

MIT
