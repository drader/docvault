# /setup

First-time setup — intake interview. Solves the cold start problem.

## Usage

```
/setup
```

Called by `npm run setup`. Can also be run directly inside Claude Code.

## Steps

Ask the user these 7 questions in order (wait for each answer before proceeding):

1. **Stack**: What libraries, frameworks, or tools do you work with regularly?
   _(List everything — e.g. React, Prisma, FastAPI, Rust, Kubernetes, etc.)_

2. **Goal**: What is the purpose of this vault in one sentence?
   _(e.g. "Keep track of breaking changes across my stack" or "Build a reference for how we use these tools at our company")_

3. **Doc types**: What kinds of docs do you expect to ingest most often?
   _(changelogs / API references / tutorials / RFCs / internal guides — pick all that apply)_

4. **Key concepts**: List 5 programming concepts you want the wiki to define from day one.
   _(e.g. server-side rendering, optimistic updates, connection pooling)_

5. **Recurring questions**: What are 3 "I always have to look this up" questions in your current stack?
   _(e.g. "How do I handle Prisma transactions?", "What are the React 18 breaking changes?")_

6. **Update cadence**: How often do you expect to drop new docs into `wiki/raw/docs/`?
   _(on every release / weekly / whenever I hit something new)_

7. **Existing docs**: Do you have any changelogs, guides, or doc files ready to drop in `wiki/raw/docs/` right now?

## Setup Output

After collecting answers:

1. `CLAUDE.md` — update Purpose with the stated goal and stack
2. `memory/status.md` — fill with project context and cadence
3. `memory/glossary.md` — add the 5 key concepts
4. `wiki/libraries/` — write a stub page for each library in the stack
5. `wiki/concepts/` — write a starter page for each concept (from LLM knowledge, clearly marked as unseeded)
6. `wiki/index.md` — updated catalog
7. `agents/researcher/MEMORY.md` — populate Bootstrap Hypotheses based on recurring questions
8. If existing docs are available: immediately start `/ingest`

## Rule
Do not fabricate or speculate in wiki pages.
Unseeded library and concept pages must include the note:
"No docs ingested yet for this entry. This page will be enriched after the first relevant ingest."
