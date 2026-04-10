# Agent Wiki

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Obsidian Compatible](https://img.shields.io/badge/Obsidian-compatible-7C3AED)
![Cursor](https://img.shields.io/badge/Cursor-supported-111827)
![Claude Code](https://img.shields.io/badge/Claude_Code-supported-111827)
![Codex](https://img.shields.io/badge/Codex-supported-111827)

[English](README.md) | [简体中文](README_zh.md)

A persistent, agent-maintained wiki for raw sources, notes, and research.

Drop source material into `raw/`. Your agent reads it, extracts knowledge, cross-links ideas, and maintains a Markdown wiki that compounds over time.

![Obsidian graph view showing an interlinked wiki grown from ingested sources](assets/obsidian-graph-view.png)

Obsidian is the best viewer for the result, but the knowledge stays in plain Markdown and works with Cursor, Claude Code, and Codex-style agents.

## Why This Exists

Most note systems still make you do the bookkeeping yourself:

- read the source
- summarize it by hand
- create concept pages
- update related notes
- remember what changed

`agent-wiki` turns that maintenance loop into an agent workflow. You keep the raw sources. The agent maintains the derived wiki.

## Quick Start

1. Clone this repo into a new vault or an empty folder:

```bash
git clone https://github.com/xccElephant/agent-wiki.git
cd agent-wiki
```

2. Bootstrap the starter files:

```bash
./install.sh
```

3. Add files to `raw/articles/`, then open the folder in Obsidian and your coding agent.

Ask your agent to ingest a source, update related wiki pages, or answer questions from the compiled wiki.

## What You Get

- `raw/` keeps immutable source snapshots
- `wiki/` stores derived knowledge pages
- `wiki/source-notes/` captures one note per source
- `wiki/entities/`, `wiki/concepts/`, and `wiki/synthesis/` separate durable knowledge types
- `logs/log.md` records ingest and maintenance history
- `AGENTS.md`, `CLAUDE.md`, and `.cursor/rules/` define the workflow for different agents

## Why It Compounds

- Each new source can update multiple downstream notes instead of living as one isolated summary.
- Query answers can be written back into `wiki/synthesis/` as durable knowledge.
- Raw files remain untouched, so the source layer stays auditable.
- Obsidian backlinks and graph view make the compiled structure easy to browse.

## Agent Wiki vs. RAG vs. Notes

| Workflow | Primary unit | What happens on each question | What accumulates |
| --- | --- | --- | --- |
| Chat history | messages | the model reasons from past conversation | fragile context |
| RAG | chunks | the model re-derives an answer from retrieved chunks | retrieval index |
| Manual notes | pages you write yourself | you maintain summaries and links by hand | scattered notes |
| Agent Wiki | maintained Markdown pages | the agent queries already-synthesized knowledge and can file new synthesis back | a persistent interlinked wiki |

## How It Works

```text
raw sources -> source notes -> entities / concepts / syntheses -> index and log
```

- `raw/` is the immutable source layer.
- `wiki/` is the maintained knowledge layer.
- `schemas/` and agent instruction files define ingest, query, and lint behavior.
- `install.sh` bootstraps tracked starter files such as `wiki/index.md` and `logs/log.md`.

## Use With an Existing Vault

If you already have an Obsidian vault, copy these into it:

- `AGENTS.md`
- `CLAUDE.md`
- `.cursor/rules/`
- `raw/`
- `wiki/`
- `logs/`
- `schemas/`
- `install.sh`

Then run:

```bash
./install.sh
```

This repo intentionally tracks starter files, templates, and workflow rules rather than your day-to-day vault contents.

## Agent Compatibility

- **Cursor** reads `.cursor/rules/` and can also benefit from `AGENTS.md`
- **Claude Code** reads `CLAUDE.md`
- **Codex-style agents** read `AGENTS.md`

Keep `AGENTS.md` and `CLAUDE.md` aligned if you change the workflow.

## Example Prompts

- `Read AGENTS.md and ingest raw/articles/article.md into wiki/source-notes/. Update related concept or entity pages and append to logs/log.md.`
- `Read CLAUDE.md and ingest raw/articles/article.md into wiki/source-notes/. Update related concept or entity pages and append to logs/log.md.`
- `Read wiki/index.md and answer: what do we currently know about <topic>? File the answer back into wiki/synthesis/ if it is durable.`
- `Lint this vault for unsupported claims, stale syntheses, missing source-notes, orphan pages, and broken wikilinks.`

## Project Structure

```text
.
├── assets/               # screenshots and promo assets
├── docs/                 # packaging and supporting docs
├── raw/                  # immutable sources
├── wiki/                 # maintained knowledge pages
├── logs/                 # append-only operational history
├── schemas/              # workflow and structure docs
├── AGENTS.md             # Codex-style instructions
├── CLAUDE.md             # Claude Code instructions
├── .cursor/rules/        # Cursor rules
└── install.sh            # bootstrap starter files
```

See `docs/github-metadata.md` for suggested GitHub naming, description, and topics.

## Credit

Inspired by Andrej Karpathy's original **LLM Wiki** idea:

- [Karpathy gist: LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f#file-llm-wiki-md)

This repository is an independent implementation template and workflow starter, not the original concept note or an official Karpathy repository.

## License

MIT.

