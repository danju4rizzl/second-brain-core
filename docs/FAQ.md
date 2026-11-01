# FAQ & Troubleshooting

## Getting started

**Which install should I use?**
Claude Code → the plugin (two `/plugin` commands). Claude desktop app → the `.plugin` file. Any other AI tool → `git clone` this repo and say "Read prompts/install.md and follow it." All three produce the same kind of vault. See the [README](../README.md#install-pick-your-tool).

**Do I need to know how to code?**
No, but you need an AI tool that can read and write files on your computer (Claude Code, Claude desktop with folder access, Cursor, Codex, Antigravity…), plus Node.js 18+ for the health-check script. A chat-only AI in the browser can't build the vault, but it can answer questions from it via `node scripts/kb.mjs bundle`.

**What should I feed it first?**
A 20–30 minute voice brain dump (transcribed), plus anything you already have: CV, website copy, price list, Notion or Google Docs exports. It doesn't need to be organised; that's the AI's job.

**Can I see a finished example first?**
Yes: the fictional [`example/`](../example/) vault. Open it in Obsidian, or run `node scripts/kb.mjs lint --root example`.

## Using it

**How do I add new information?**
Drop the file into `raw/` (never edit existing raw files), then ask your AI to "compile the new raw files".

**How do I ask it something?**
Say "Answer from the wiki: …". Answers cite wiki pages and end with a **File back?** list. Say "file that back" to save the useful parts. That's how the brain improves itself.

**What do `[CONFIRM]` and `[SET]` mean?**
`[CONFIRM]` marks a fact the AI couldn't verify. `[SET]` marks a decision only you can make (e.g. a price). They're collected in `wiki/gaps.md`. Answer them and the AI updates the pages.

**Why does it say "Conflicts"?**
When two sources disagree, the wiki records both sides with links instead of silently picking one. You decide which is right.

**How big can it get before it stops fitting in the AI's memory?**
Run `node scripts/kb.mjs stats`. Most personal and small-business wikis stay well under 128K tokens. Above ~200K, `kb lint` suggests splitting into separate brains.

## Privacy

**Will my notes end up on GitHub?**
Not from this repo. `.gitignore` is an *allowlist*: git ignores everything except the engine files, so `raw/`, `wiki/`, `agents.md` and anything new you create stay local. The GitHub check on this repo also fails if a private file is ever tracked.

**I want version history for my notes. How?**
Use a **separate private** repo or an encrypted backup, never a public fork. With the Claude plugin, add `{"privateRepo": true}` to `.kavara-brain.json` in that private repo so the git guard allows it. Secrets are still blocked.

**My Notion export contains passwords. Is that a problem?**
The raw export stays on your computer and is git-ignored. The install and import steps tell the AI to **report** credentials to you and never copy them into the wiki. Move them to a password manager and rotate anything sensitive (API keys especially).

**Does the AI provider see my notes?**
Whatever you send to a cloud model is processed by that provider under their terms. For sensitive material, use a local model for questions, or strip details before sending.

## Troubleshooting

**`node` is not recognized / command not found**
Install Node.js LTS from nodejs.org, then restart your terminal or AI tool. On Windows, reopen the app after installing so the new PATH is picked up. Bun works too: `bun scripts/kb.mjs lint`.

**`kb lint` shows "broken link"**
Links must use full vault paths: `[[wiki/00-core/strategy|strategy]]`. Inside Markdown tables, escape the pipe: `[[wiki/00-core/strategy\|strategy]]`. Ask your AI to "fix the lint errors".

**"orphan: no inbound links"**
No other page links to this one. Add it to a related page's `## Related` list (and link back).

**"uncompiled: raw file not cited by any wiki page"**
A source in `raw/` hasn't been compiled yet. Ask "compile the new raw files", or list it under "Unplaced raw files" in `wiki/gaps.md` if it's noise.

**"stale: updated … (> 30 days)"**
A gentle nudge to review the page. If it's still correct, bump `updated:` to today.

**Obsidian links don't work**
Open the **repo root** as the vault (not the `wiki/` folder). In Settings → Files & links, set New link format to *Absolute path in vault* and turn on *Use [[Wikilinks]]*.

**Windows: "Destination path too long" when unzipping Notion**
Use `python scripts/notion_extract.py "<export.zip>" "raw/notion-<date>"`. It shortens Notion's long IDs and fixes the links.

**`git` errors with "File exists" / `.lock`**
Another git process crashed or is still running. Close other git tools; if nothing is running, delete the named `.lock` file inside `.git/`.

## Other

**Can I use it for a team?**
Yes, for small teams: share the vault through a private repo, with each person adding to `raw/` and one compile pass merging. Very large organisations should look at retrieval (RAG) instead.

**Is it free?**
Yes, MIT licensed. If you'd like it set up for your business, Kavara Digital Global offers a done-for-you setup: see [kavaradigital.com](https://kavaradigital.com).

**Found a bug or a privacy issue?**
Bugs: open a GitHub issue. Privacy or security problems: see [SECURITY.md](../SECURITY.md).
