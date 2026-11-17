# AGENTS.md

Standardized workspace and iteration space for a human user running human-AI-driven market research. Agents read this file before acting.

## Purpose

This repository is the human user's workspace: a place to think, iterate, and refine research with an agent's help. The file tree is fixed so every project is replicable, but the work inside it is expected to evolve continuously — including the deliverables themselves.

## Directory contract

The repository MUST contain exactly these two top-level directories:

```
./
├── input/       # Reference material provided to the project. READ-ONLY for agents.
└── workspace/   # Everything the project produces: human-authored, co-created, and AI-generated files.
```

### `input/`
- Source of truth: briefs, specs, PDFs, exports, prior research, raw data.
- Agents MUST treat it as read-only. Never create, rename, move, or overwrite files here.
- If an input is wrong or missing, ask the human — do not patch it in place.

### `workspace/`
Contains three kinds of files, distinguished by a filename prefix:

1. **`human-`** — human-authored files the human created or edited themselves (notes, briefs, spreadsheets they maintain). Example: `human-brief.md`.
2. **`co-`** — human-AI co-created files produced through back-and-forth with an agent (drafts shaped in dialogue, tables the human directed, analyses worked through together). Example: `co-vendor-shortlist.md`.
3. **`ai-`** — AI-generated deliverables the agent produces autonomously from `input/` and other `workspace/` context (reports, dashboards, benchmarks, decks). Example: `ai-market-dashboard.html`.

Rules by prefix:
- **`human-`**: agents MUST NOT modify without explicit permission.
- **`co-`**: the agent may edit freely within the current conversation's direction; still ask before large rewrites.
- **`ai-`**: the human does not edit these directly — feedback flows through conversation, and the agent regenerates or updates the file. Agents may create and iterate across sessions; deliverables are living artifacts, not frozen on first write. **Default format: standalone visual HTML** (self-contained, no external assets, with layout, typography, and charts/tables incorporated inline — designed for reading, not a wall of text). Use another format only when the content genuinely can't be expressed as HTML — see File conventions for the two allowed exceptions. Before a large overwrite, offer a quick "replace or keep a new version alongside?" check.

Cross-cutting conventions:
- **Unprefixed files are treated as `human-` by default.** Nothing breaks if a file slips through without a prefix — the agent errs on the side of not touching it.
- **Promotion is allowed.** A `co-` file the agent later regenerates end-to-end can be renamed to `ai-`; an `ai-` file the human starts editing becomes `co-`. The prefix reflects current authorship, not origin.
- Expected to be messy but legible: use descriptive filenames so the human can scan the folder.
- `human-` and `co-` content is not intended for anyone outside the project. Do not link to it from `ai-` deliverables.

## Workflow loop

1. **Ingest** — read everything in `input/`, plus any existing `human-` and `co-` files in `workspace/`. Summarize what the human has provided before proposing work.
2. **Work in `workspace/`** — either co-create (`co-` files) when the human wants to steer the artifact directly, or generate autonomously (`ai-` files) when the human asks for a deliverable. Both modes are interleaved, not sequential — the human drives the pace and decides which mode fits each ask.

## File conventions

Formats depend on the authorship prefix.

**`ai-` files** default to **standalone visual HTML** — self-contained, no external assets, with dashboards, charts, tables, layout, and typography incorporated inline. Only two exceptions are allowed:
- **`.xlsx` / CSV** — when the human needs to pivot, sort, filter, or paste the data elsewhere. HTML is read-only; a spreadsheet is a working tool.
- **Original filename from `input/`** — when the `ai-` file is just citing or passing through a source reference, keep the source's filename rather than wrapping it in HTML.

**`human-` and `co-` files** keep flexibility — pick whatever fits the conversation (markdown for notes/reports/analyses, spreadsheet for structured data, HTML when useful).

**Filenames**: lowercase, hyphen-separated, human-readable, with the authorship prefix first (`ai-vendor-comparison.html`, not `vc1.html`).

## Operating rules for agents

- Cite every claim drawn from `input/` with the source filename next to the claim.
- Do not upload artifacts to external services; keep all generated files local.
- Never modify a `human-` file (or an unprefixed file) in `workspace/` without explicit permission. When unsure of a file's authorship, ask.
- When creating a new file in `workspace/`, choose the prefix that reflects how the file will be worked on: `co-` if the human will steer it, `ai-` if you will regenerate it autonomously.
- Before any destructive action (bulk delete, rename sweep, large overwrite of an `ai-` file), confirm with the human.
- Do not create additional top-level directories. Nested subfolders inside `workspace/` are allowed if the human agrees.

## Bootstrap

To recreate an empty instance of this workspace:

```bash
mkdir -p input workspace
```

Then drop reference material into `input/` and begin at step 1 of the workflow loop.
