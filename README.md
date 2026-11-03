# Kavara Brain: a privacy-focused, self-improving LLM second brain 🧠

**One repo, every AI tool.** Use it with Claude (plugin with guard hooks), or clone it for Cursor, Codex, Antigravity, Grok Build, Aider or any agent that can read and write files.

A personal (or small-business) second brain that **an AI writes and you read**. It follows Andrej Karpathy's LLM knowledge-base workflow ([method](docs/method.md)): dump raw material in a folder, let an LLM *compile* it into a linked Markdown wiki, browse it in Obsidian, ask it questions, and file every useful answer back in. The wiki gets denser and better linked with every loop.

- **No RAG, no vector database.** The compiled wiki is small enough to fit in a modern model's context window.
- **Plain Markdown + git.** You own every file, and it works with Claude Code, Cursor, Codex, Aider or any agent that can read and write files.
- **Self-checking.** A zero-dependency script catches broken links, missing sources, orphan pages, stale notes and raw files nobody has compiled yet.
- **Private by default.** The `.gitignore` is an allowlist: only engine files can ever be committed. Your notes stay on your machine.

> This repository is the **Kavara Brain Engine**: prompts, scripts, templates and a fictional demo. It contains no one's personal data.

---

## Install: pick your tool

| You use… | Do this |
|---|---|
| **Claude Code** | `/plugin marketplace add danju4rizzl/second-brain-core` then `/plugin install kv-brain@kavara`. Open a folder and run `/kv-brain:install`. You get slash commands, an auditor agent and guard hooks. |
| **Claude desktop app** | Download `kavara-brain.plugin` from the [plugin releases](https://github.com/danju4rizzl/kavara-brain-claude/releases) and install it, then say "set up a second brain in this folder". |
| **Cursor, Codex, Antigravity, Grok Build, Aider, other agents** | `git clone https://github.com/danju4rizzl/second-brain-core.git my-second-brain`, open the folder in your agent and say **"Read prompts/install.md and follow it."** |

Stuck? See the [FAQ & troubleshooting](docs/FAQ.md).

## The Kavara Brain suite

| Product | What it is | Status |
|---|---|---|
| **Kavara Brain Engine** (this repo) | Tool-agnostic core: prompts, `kb.mjs` lint/index script, templates, demo vault | ✅ v1.1.0 |
| [**Kavara Brain for Claude**](https://github.com/danju4rizzl/kavara-brain-claude) | The engine plus a Claude skill (9 modes), `/brain-*` slash commands, an independent auditor agent and guard hooks (raw/ protection, secret scan, git privacy guard, auto-lint) | ✅ v0.1.0 |
| **Kavara Brain Guard** | MCP server + git hooks: the same hard guards for Cursor, Antigravity, Codex, Grok Build | 🛠 planned |
| **Kavara Brain Sync** | Encrypted private sync of your notes across computers | 🛠 planned |

Built by [Kavara Digital Global](https://kavaradigital.com).

## Quick start (any tool)

```bash
git clone https://github.com/danju4rizzl/second-brain-core.git my-second-brain
cd my-second-brain
```

1. **Gather raw material.** The best start is a **20–30 minute voice brain dump** (transcribed) about your goals, work, customers, offers, team, tools, projects and writing style. Add a conversation, CV, website copy, a price list, Notion/Google Docs exports, anything. It doesn't need to be organised.
2. **Open the folder in your AI agent** and say:

   > **Read prompts/install.md and follow it.**

   It interviews you, saves your sources in `raw/`, compiles your first wiki, writes your personal `agents.md`, runs the health check, and confirms nothing private is staged in git.
3. **Open the folder in [Obsidian](https://obsidian.md)** as a vault (*Open folder as vault*).

Want to see the result first? Browse the fictional [`example/`](example/) vault (Ada's Oven, a home bakery).

## How it works

```
   ┌──────────── 1. INGEST ────────────┐
   │ raw/  ← dump anything, never edit │
   └───────────────┬───────────────────┘
                   ▼
   2. COMPILE  (prompts/compile.md)    →  wiki/  topic pages with sources, open questions, conflicts
                   ▼
   3. VIEW     (you, in Obsidian: graph · backlinks · tags)
                   ▼
   4. QUERY    (prompts/query.md, whole wiki in context, answers cite pages)
                   ▼
   5. FILE BACK (prompts/file-output.md)  →  wiki/07-outputs/ + updated pages + wiki/gaps.md
                   ▼
   6. LINT     (scripts/kb.mjs lint + prompts/lint.md)
                   │
                   └──→ gaps drive new research (prompts/research.md) → back to raw/
```

### What's in the box

```
second-brain/
├── README.md · LICENSE · CHANGELOG.md · SECURITY.md · package.json · .gitignore (allowlist)
├── .claude-plugin/       ← pointer so Claude Code can install the plugin from this repo
├── docs/
│   ├── method.md         ← the method, and why there's no RAG
│   └── FAQ.md            ← FAQ & troubleshooting
├── prompts/
│   ├── install.md        ← one-time setup interview
│   ├── compile.md        ← raw/ → wiki/ (incremental)
│   ├── query.md          ← full-context Q&A with citations
│   ├── file-output.md    ← save answers back (the self-improving loop)
│   ├── lint.md           ← LLM health check
│   └── research.md       ← close gaps with web research
├── scripts/
│   ├── kb.mjs            ← index · lint · bundle · stats (Bun or Node, zero deps)
│   └── notion_extract.py ← unzip Notion exports on Windows without path-too-long errors
├── templates/            ← agents.md, CLAUDE.md, topic page, synthesis, folder map, gaps, log
└── example/              ← fictional demo vault
```

### What install creates for you (private, never committed)

```
├── agents.md · CLAUDE.md ← your operating manual for every AI tool
├── raw/                  ← your sources
└── wiki/
    ├── index.md          ← generated topic hierarchy
    ├── gaps.md · log.md
    ├── 00-core/ …        ← topic folders, each with a generated agent.md map
    └── 07-outputs/       ← dated syntheses
```

## Requirements

| Need | Why |
|---|---|
| An AI agent that reads/writes local files ([Claude Code](https://claude.com/claude-code), Cursor, Codex, Aider) | Compiles, answers and files |
| [Bun](https://bun.sh) or Node.js 18+ | Runs `scripts/kb.mjs` |
| git | Pull engine updates; optional private history for your notes |
| [Obsidian](https://obsidian.md) (free) | Reading and browsing the graph |
| Python 3.8+ (optional) | Only for `scripts/notion_extract.py` |

## Daily use

| You want to… | Tell your agent |
|---|---|
| Add something | Drop it in `raw/` → *"compile the new raw files"* |
| Ask a question | *"Answer from the wiki: …"*. It cites pages and ends with **File back?** |
| Keep an answer | *"File that back"* → saved in `wiki/07-outputs/`, pages updated |
| Weekly check-up | `bun run lint`, then *"run prompts/lint.md"* |
| Fill gaps from the web | *"Run prompts/research.md on the top 3 research gaps"* |
| Use a chat-only AI | `bun run bundle` → attach `.kb/wiki-bundle.md` |

### Script

```bash
bun run index     # rebuild wiki/index.md, every folder's agent.md map, the gaps auto-list
bun run lint      # health check, logged to wiki/log.md (exit code 1 on errors)
bun run bundle    # one file with the whole wiki, for full-context Q&A
bun run stats     # raw vs wiki size, context-window fit
# or directly: node scripts/kb.mjs <cmd> [--json] [--log] [--root <vault-dir>]
```

Lint checks for broken `[[links]]`, missing frontmatter or sections, missing sources, orphan pages, one-way relations, pages older than 30 days, oversized pages, uncompiled raw files, raw files newer than their pages, folders without a map, and total size vs context.

## Privacy

- `.gitignore` ignores **everything** except the engine files. `raw/`, `wiki/`, `agents.md`, `CLAUDE.md`, `.obsidian/` and `.kb/` are blocked explicitly as well. Anything new you create stays private unless you deliberately allow it.
- Keep version history of your notes in a **separate private** repo or backup, never in a public fork.
- Never store passwords or API keys in notes. The install and compile prompts tell the AI to flag and skip them.
- For sensitive material, run queries on a local model (e.g. Ollama) and strip details before sending anything to a cloud model.

## Updating the engine

```bash
git pull   # updates prompts/, scripts/, templates/, docs/; your private files are untouched
```

## More

- [FAQ & troubleshooting](docs/FAQ.md) · [Method](docs/method.md) · [Changelog](CHANGELOG.md) · [Security & privacy reports](SECURITY.md)

## Credits

- Built by Danjuma Ashiwaju-Garba ([Kavara Digital Global](https://kavaradigital.com)).

- Method: Andrej Karpathy's LLM knowledge-base workflow (April 2026).

## License

[MIT](LICENSE)
