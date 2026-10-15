# NOTICE

This repository contains **verbatim excerpts extracted from third-party proprietary software**
for the purpose of security analysis and criticism.

## What this repository is not

It is **not** a distribution of Anthropic's, OpenAI's, Block's, Hugging Face's, or any other
vendor's source code. It is an **analysis** of that code, and the excerpts exist because a
security finding without a quotable artifact is not checkable.

## What it does contain

| Directory | Nature of the material |
|---|---|
| `claude/evidence/` | Byte strings, IPC channel names, error messages, settings schemas, and code excerpts extracted from **Anthropic Claude Desktop 2.31226.1.0**. Anthropic's code is proprietary. |
| `codex/evidence/` | String literals, protocol event names, native string tables, and an ASAR index extracted from **OpenAI Codex 26.1007.2314.0**. OpenAI's code is proprietary. |
| `harness/evidence/` | Grep output and code snippets from **open-source** projects (jan, atomic-agents, smolagents, OpenHands, goose, open-interpreter, Coven), each used under its own licence. |

The largest individual artifacts are `codex/evidence/asar-index.json` (3.2 MB) and
`codex/evidence/manifest.tsv` (596 KB), which are **indexes and hashes** of the ASAR archive —
a directory listing, not the source itself.

## Excluded on purpose

- **The extracted source trees are not here.** They lived in scratch (`%TEMP%\codex-src`,
  `%TEMP%\claude-src`, `%TEMP%\coven-audit`, `%TEMP%\harness-sandbox`) and were never committed.
- **No binaries.** No `.exe`, `.dll`, or `.vhdx` from any product appears in this repository.
- **No user data.** The analyst's own `~/.claude/` and `~/.codex/` conversation and memory files
  were explicitly out of scope and were never opened.
- **No credentials.** The workspace was scanned for GitHub PATs, OpenAI/Anthropic API keys, AWS
  access keys, Slack tokens, Google API keys, bearer literals, and private keys. **Zero hits.**

## Vendor attribution

- **Claude / Claude Desktop / Claude Code** — © Anthropic PBC
- **Codex** — © OpenAI
- **Typeless** — © Typeless
- **MiniMax Code** — © MiniMax
- **jan** — AGPLv3 · **smolagents** — Apache 2.0 · **OpenHands** — MIT · **goose** — Apache 2.0 ·
  **open-interpreter** — AGPLv3 · **atomic-agents** — MIT · **Coven** — see its own repository

Each open-source project retains its own licence; the snippets quoted here are attributed in the
per-file evidence and remain under those terms.

## If you are a rights holder

The material here was produced for security research and criticism, which is lawful. If you
consider any excerpt problematic, open an issue or contact the repository owner and it will be
removed or redacted on request.

## No endorsement

Product and company names are used **only** to identify the artifacts analysed. Nothing here
implies endorsement, affiliation, or that any vendor reviewed or approved these findings.