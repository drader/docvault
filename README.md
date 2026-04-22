# docvault

**Agentic developer documentation knowledge base — built on [memex](https://github.com/drader/memex)**

Drop library docs, changelogs, and RFCs in. Agents extract APIs, breaking changes, and patterns — linking libraries and concepts into a searchable reference that grows with your stack.

→ [View presentation](https://drader.github.io/docvault/)

---

## How it works

1. **Drop a doc** — Place a changelog, API reference, RFC, or tutorial into `wiki/raw/docs/`. The agent identifies its type automatically.
2. **Agent routes and extracts** — The researcher agent reads the doc, identifies the library, version, and content type, then extracts APIs, breaking changes, patterns, and gotchas.
3. **Breaking changes are never buried** — Every breaking change gets its own explicit flag in the changelog page — never hidden in prose. The library page's version history table is updated automatically.
4. **Orchestrator tracks staleness** — When the queue is empty, the agent scans for libraries with outdated version entries and flags them in the journal.

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
