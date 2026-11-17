# human-ai-research-sandbox

With this project, create repeatable workspaces for running market research with an AI agent as your co-worker. The folder layout is fixed so every research project looks the same; the work inside evolves freely.

## Layout

```
./
├── input/              # Reference material you give the project (read-only for agents)
└── workspace/          # Your notes + things you shape with the agent together (reports, dashboards, decks)
```

- **input/** — briefs, PDFs, exports, prior research. The agent reads these but never changes them.
- **workspace/** — messy-but-legible drafts, tables, and analyses. Some you write yourself, some you build with the agent. You give feedback through chat, the agent reworks based on `/input/` and `/workspace`.

## How to use it

1. Clone this project
2. Drop source materials into `input/`.
3. Chat with the agent to work on your research.
