# docvault — Master Schema

This file is the system constitution. Read every session.

## Purpose

A self-growing developer documentation knowledge base. Drop library docs, changelogs, RFCs, or tutorials into `wiki/raw/docs/`. The researcher agent ingests them into structured wiki pages — extracting APIs, breaking changes, patterns, and gotchas, linking libraries and concepts into a searchable reference that grows with your stack.

## System Architecture

```
TypeScript Motor (src/)     →  scheduler, runner, locker, validator, budget, consolidator
Markdown Content            →  wiki/, agents/, memory/, commands/
MCP Server                  →  obsidian-hybrid-search (semantic search over wiki/)
```

## Two Memory Layers

| Layer | Location | Content | Written by |
|---|---|---|---|
| Process memory | `agents/*/MEMORY.md` | Recurring gotchas, upgrade patterns, hypotheses | Each agent |
| Domain knowledge | `wiki/` | Libraries, patterns, concepts, changelogs | Agents via locker |

The weekly consolidator bridges process memory → domain knowledge automatically.

## Tier System

- **Tier 1** — Every session: `memory/`, `scratch/ideas.md`, `journal/` (last 3 days)
- **Tier 2** — When agent/domain is active: `wiki/index.md`, `agents/[active]/AGENT.md + MEMORY.md`
- **Tier 3** — Only when explicitly requested: `wiki/archive/`, `outputs/`, old `journal/`

## Operations

- **INGEST** — New doc → structured wiki page (`/ingest`)
- **QUERY**  — Ask a technical question, get a wiki-backed answer (`/query`)
- **LINT**   — Wiki health check: orphan pages, outdated versions, broken links (`/lint`)
- **CONSOLIDATE** — MEMORY.md → wiki bridge (orchestrator, weekly)

## Hard Rules

1. `wiki/raw/` is never modified — read only
2. Every claim cites a source doc — unsourced claims are forbidden
3. Contradictions are flagged with `## CONFLICT`, never deleted
4. Pages are never deleted — moved to `wiki/archive/`, status: archived
5. Every operation is logged with a timestamp to `wiki/log.md`
6. Wiki writes go through the locker — no direct writes
7. Never modify another agent's files

## Directory Guide

```
CLAUDE.md          this file — master schema
MANIFEST.md        tier routing map
CONVENTIONS.md     naming rules
AGENT_REGISTRY.md  active agents index

src/               TypeScript motor
wiki/              developer knowledge base
  raw/docs/        drop docs, changelogs, RFCs, tutorials here
  libraries/       one page per library or framework
  patterns/        design patterns and architectural approaches
  concepts/        programming concepts (memoization, SSR, etc.)
  changelogs/      version-specific change summaries
  syntheses/       cross-library comparisons, migration guides
agents/            agent definitions and process memories
memory/            system-wide Tier 1 state
scratch/           docs to read, open questions, upgrade TODOs
journal/           cross-agent signal channel
commands/          slash command prompt templates
scripts/           setup and management scripts
outputs/           upgrade checklists, weekly reports
```
