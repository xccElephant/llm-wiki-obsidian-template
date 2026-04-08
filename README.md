# llm-wiki-obsidian-template

A Cursor + Obsidian template for building a persistent, LLM-maintained personal wiki.

## Credit

This repository is inspired by Andrej Karpathy's original **LLM Wiki** idea:

- Karpathy gist: [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f#file-llm-wiki-md)

This repo is an independent implementation template. It is **not** the original concept note and is **not** an official Karpathy repository.

## What This Repo Is

This template turns the high-level LLM Wiki pattern into a practical Cursor + Obsidian workspace:

- a `raw/` layer for source snapshots
- a `wiki/` layer for derived knowledge
- `AGENTS.md` instructions for the coding agent
- `.cursor/rules/` files for persistent guardrails
- starter docs for `ingest`, `query`, and `lint`

## Requirements

- [Cursor](https://www.cursor.com/)
- [Obsidian](https://obsidian.md/)
- optional but recommended: `git`

There is no package installation step for this template. You mainly copy or clone the folder structure and use it as an Obsidian vault plus a Cursor workspace.

## Install

### Option 1: Start a New Vault From This Template

1. Click **Use this template** on GitHub, or clone the repository:

```bash
git clone https://github.com/xccElephant/llm-wiki-obsidian-template.git
```

2. Open the folder in Obsidian as a vault.
3. Open the same folder in Cursor.
4. Start dropping source files into `raw/articles/`.

### Option 2: Add It To An Existing Vault

Copy these files and folders into your existing Obsidian vault:

- `AGENTS.md`
- `.cursor/rules/`
- `raw/`
- `wiki/`
- `logs/`
- `schemas/`

If your existing vault already has a different structure, adapt the folders and update `AGENTS.md` plus `.cursor/rules/` to match your naming.

## First Use

1. Put one source document into `raw/articles/`.
2. Open the vault in Cursor.
3. Ask the agent to read `AGENTS.md` and ingest the source into `wiki/source-notes/`.
4. Review the generated note in Obsidian.
5. Ask the agent to update related concept, entity, or synthesis pages.
6. Ask the agent to append an operation note to `logs/log.md`.

## Example Prompts

Use prompts like these in Cursor:

- `Read AGENTS.md and ingest raw/articles/my-article.md into wiki/source-notes/. Update any related concept or entity pages and append to logs/log.md.`
- `Read wiki/index.md and answer: what do we currently know about <topic>? File the answer back into wiki/synthesis/ if it is durable.`
- `Lint this vault for unsupported claims, stale syntheses, missing source-notes, orphan pages, and broken wikilinks.`

## How This Differs From The Original LLM Wiki

Karpathy's gist describes the pattern at a high level.

This template adds a concrete implementation for day-to-day use:

- a ready-to-copy Obsidian folder structure
- explicit separation between `raw/` and `wiki/source-notes/`
- Cursor-specific agent instructions and rule files
- starter schema files and workflow docs
- a bias toward traceability, explicit disputes, and durable markdown artifacts

## Repository Layout

```text
raw/
  articles/
  assets/
wiki/
  source-notes/
  entities/
  concepts/
  synthesis/
logs/
schemas/
.cursor/rules/
AGENTS.md
```

## Core Idea

- `raw/` holds original sources and should be treated as immutable snapshots.
- `wiki/source-notes/` holds one structured derived note per source.
- `wiki/entities/`, `wiki/concepts/`, and `wiki/synthesis/` hold the evolving knowledge graph.
- `logs/log.md` records what the agent did and when.

## Recommended Workflow

1. Drop a new source into `raw/articles/`.
2. Ask Cursor to ingest it into `wiki/source-notes/`.
3. Let the agent update related entity, concept, and synthesis pages.
4. Keep durable answers in the wiki instead of losing them in chat.
5. Periodically ask the agent to lint the wiki for contradictions, stale claims, and orphan pages.

## Good Fit

- research reading
- technical topic tracking
- course notes
- deep-dive study projects
- long-running personal knowledge bases

## Notes

- The template is intentionally minimal.
- You should adapt naming, page types, and rules to your own domain.
- If you publish your own derivative, keep the attribution to the original LLM Wiki idea.
