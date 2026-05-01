# LLM Wiki Starter

This project is a generic LLM-maintained markdown wiki starter, not an application runtime. Its job is to turn raw documents into a persistent, linked knowledge base with summaries, entities, concepts, source attribution, and maintenance logs.

The starter gives humans and AI agents a predictable place to put source material, generated wiki pages, operating instructions, and maintenance history. It is intentionally generic. Add domain-specific folders only when the project needs them.

## How It Works

- Put unprocessed source files in `raw/`.
- Ask an AI agent to follow [`_update.md`](_update.md).
- The agent reads each source once, extracts durable knowledge, and creates or updates generated pages.
- Consumed sources move to `ingested/` with dated filenames and should remain immutable.
- Human-facing pages live in `summaries/`, `entities/`, and `concepts/`.
- `index.md` and same-name folder directory pages keep the wiki navigable.
- `log.md` records every maintenance operation, including created and updated files.

## Current Starter State

This repository is currently an empty starter wiki. No summary, entity, or concept pages have been generated yet; the directory pages are placeholders until source files are ingested.

## Quickstart

1. Copy this folder into a new project.
2. Put unprocessed source files in `raw/`.
3. Ask an AI agent to follow [`_update.md`](_update.md).
4. Review generated pages in `summaries/`, `entities/`, and `concepts/`.
5. Keep source files immutable after they move to `ingested/`.
6. Keep `index.md` and each folder directory page current.

## Core Structure

- [`index.md`](index.md) - root navigation entrypoint.
- [`_idea.md`](_idea.md) - operating model and philosophy.
- [`_init.md`](_init.md) - bootstrap instructions for a new wiki.
- [`_update.md`](_update.md) - repeatable ingestion and maintenance workflow.
- [`_template.md`](_template.md) - page templates, metadata, and linking rules.
- [`AGENTS.md`](AGENTS.md) - instructions for AI agents maintaining the wiki.
- [`log.md`](log.md) - append-only maintenance history.
- `raw/` - inbox for unprocessed source files.
- `ingested/` - archive for consumed source files.
- `summaries/` - source summaries and synthesis pages.
- `entities/` - people, products, companies, tools, standards, systems, or other named things.
- `concepts/` - durable ideas, patterns, definitions, and reusable knowledge.

## Folder Directory Rule

Do not create `index.md` inside topic folders. Use a directory page with the same name as the folder:

- `entities/entities.md`
- `concepts/concepts.md`
- `summaries/summaries.md`

Each folder directory page should link every generated markdown page in that folder except itself.

Example:

```markdown
# Entities

- Add generated entity pages here, such as entities/example-company.md.
- Add generated tool pages here, such as entities/example-tool.md.
```

## Ingestion Workflow

1. Add new source files to `raw/`.
2. Read `_template.md`, `index.md`, and `log.md`.
3. Extract durable summaries, entities, and concepts.
4. Update existing pages before creating new ones.
5. Create new pages only for reusable topics.
6. Move processed files to `ingested/YYYY-MM-DD-original-name.md`.
7. Update folder directory pages and `index.md`.
8. Append a concise entry to `log.md`.
9. List every changed file in the log using `create - <file-path>` or `update - <file-path>`.

Example log file list:

```text
create - summaries/example-source.md
update - concepts/example-concept.md
update - index.md
update - log.md
```

## Optional Topic Folders

Create extra folders only when the project domain needs them. Common examples:

- `product/` for requirements, personas, roadmap, and product decisions.
- `market/` for competitors, pricing, positioning, and go-to-market notes.
- `risks/` for risks, mitigations, assumptions, and open questions.
- `comparisons/` for side-by-side evaluations.
- `architecture/` for system design, data models, APIs, security, and infrastructure.

If you add one, also add a same-name directory page such as `architecture/architecture.md`.

## Metadata Rules

Every generated markdown page should include frontmatter:

```yaml
---
type: concept
tags: [example]
source:
  - ingested/YYYY-MM-DD-source-name.md
last_updated: YYYY-MM-DDTHH:mm:ss+05:30
confidence: medium
---
```

Use local ISO timestamps with timezone offsets for `last_updated`, for example `2026-05-01T20:30:00+05:30`.

## Validation Checklist

- Every Obsidian link resolves to an existing markdown file.
- Every `source:` entry is empty or points to an existing file under `ingested/`.
- No folder uses `index.md`; folder directory pages use the folder name.
- `raw/` is empty except placeholders after ingestion.
- `ingested/` contains only consumed, immutable source files.
- Generated pages summarize and synthesize instead of copying large source sections.
