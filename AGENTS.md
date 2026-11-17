# AGENTS.md

Standardized workspace and iteration space for a human user running human-AI-driven market research. Agents read this file before acting.

## Purpose

This repository is the human user's workspace: a place to think, iterate, and refine research with an agent's help. The file tree is fixed so every project is replicable, but the work inside it is expected to evolve continuously — including the deliverables themselves.

## Directory contract

The repository MUST contain exactly these three top-level directories:

```
./
├── input/           # Reference material provided to the project. READ-ONLY for agents.
├── working-space/   # Human-authored + human-AI co-created files.
└── output/          # AI-generated deliverables only.
```

### `input/`
- Source of truth: briefs, specs, PDFs, exports, prior research, raw data.
- Agents MUST treat it as read-only. Never create, rename, move, or overwrite files here.
- If an input is wrong or missing, ask the human — do not patch it in place.

### `working-space/`
- Contains two kinds of files only:
  1. **Human-authored** files the human created or edited themselves (notes, briefs, spreadsheets they maintain).
  2. **Human-AI co-created** files produced through back-and-forth with an agent (drafts shaped in dialogue, tables the human directed, analyses worked through together).
- Agents MUST NOT modify a human-authored file without explicit permission. Treat unfamiliar files as human-authored by default.
- For co-created files, the agent may edit freely within the current conversation's direction; still ask before large rewrites.
- Expected to be messy but legible: use descriptive filenames so the human can scan the folder.
- Content here is not intended for anyone outside the project. Do not link to it from deliverables.

### `output/`
- Contains AI-generated deliverables only — artifacts the agent produces autonomously from `input/` and `working-space/` context (reports, dashboards, benchmarks, decks).
- The human does not edit files here directly; feedback flows through conversation or `working-space/`, and the agent regenerates or updates the `output/` file.
- Agents may create and iterate on `output/` files freely across sessions. Deliverables are living artifacts, not frozen on first write.
- Prefer self-contained formats (standalone HTML, single markdown, single spreadsheet). No references to `working-space/` paths.
- Before a large overwrite, offer a quick "replace or keep a new version alongside?" check.

## Workflow loop

1. **Ingest** — read everything in `input/`, plus any existing human-authored files in `working-space/`. Summarize what the human has provided before proposing work.
2. **Co-create in working-space** — when work is exploratory or the human wants to steer the artifact directly, build and refine it together in `working-space/`.
3. **Generate in output** — when the human asks for a deliverable, produce it autonomously in `output/` using `input/` + `working-space/` as source material. Iterate on the same file across sessions as the human requests changes.

Steps 2 and 3 are interleaved, not strictly sequential — the human drives the pace and decides which mode (co-creation vs. AI-generation) fits each ask.

## File conventions

- **Notes, reports, analyses** → Markdown (`.md`).
- **Structured data, comparisons, benchmarks** → Spreadsheet (`.xlsx`) or CSV.
- **Dashboards, visual deliverables** → Standalone HTML (self-contained, no external assets).
- **Source references** → keep original filename from `input/` when citing.
- Filenames: lowercase, hyphen-separated, human-readable (`vendor-comparison.md`, not `vc1.md`).

## Operating rules for agents

- Cite every claim drawn from `input/` with the source filename next to the claim.
- Do not upload artifacts to external services; keep all generated files local.
- Never modify a human-authored file in `working-space/` without explicit permission. When unsure of a file's authorship, ask.
- When uncertain which folder a file belongs in: if it needs human input or editing, use `working-space/`; if it's a deliverable you generate autonomously, use `output/`.
- Before any destructive action (bulk delete, rename sweep, large overwrite in `output/`), confirm with the human.
- Do not create additional top-level directories. Nested subfolders inside `working-space/` or `output/` are allowed if the human agrees.

## Bootstrap

To recreate an empty instance of this workspace:

```bash
mkdir -p input working-space output
```

Then drop reference material into `input/` and begin at step 1 of the workflow loop.
