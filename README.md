# Harness Case Study

Static security analysis of AI agent runtimes — three shipping desktop products and seven
open-source harnesses — conducted by reading their code, never running them.

**Start here if you are new:** **[primer/01-agent-security-explained.md](primer/01-agent-security-explained.md)**

---

## What this is

Every conclusion here comes from **reading source or binary artifacts**. No product in this study
was launched, installed, or allowed to phone home. Where a claim is inference rather than
observation, the report says so, and §6 of every report lists what was *not* established.

## The one-paragraph summary

Every agent tool arranges its defences in the same three layers — authority rules in the system
prompt, structural validation in code, and OS-level containment — and they differ almost entirely
in **where the boundary sits and what the default is**. The reusable question is not *"does it have
a sandbox"* but:

> **Is the sandbox on by default, and does anything report when it's off?**

Defaults beat features. Claude has the most elaborate sandbox configuration of anything examined
and a worse out-of-the-box posture than Codex, which has a plainer one.

## Index

### Primer
| | |
|---|---|
| [01 — Agent security explained](primer/01-agent-security-explained.md) | Vocabulary decoder, the three layers, a 7-question evaluation procedure, worked examples |

### Claude Desktop 2.31226.1.0
`C:\Program Files\WindowsApps\Claude_2.31226.1.0_x64__pzs8sxrjxfjjc`

| | Report |
|---|---|
| 01 | [Artifact manifest](claude/reports/01-artifact-manifest.md) |
| 02 | [IPC surface](claude/reports/02-ipc-surface.md) |
| 03 | [Sandbox boundary](claude/reports/03-sandbox-boundary.md) |
| 04 | [Native binaries & elevation](claude/reports/04-native-and-elevation.md) |
| 05 | [Update & signing](claude/reports/05-update-and-signing.md) |
| 06 | [Findings F1–F21](claude/reports/06-findings.md) |
| 07 | [Consent gate & 3p bypass](claude/reports/07-consent-gate-and-3p-bypass.md) |
| 09 | [Prompt injection & the execution sandbox](claude/reports/09-prompt-injection-and-sandbox.md) |

### Codex 26.1007.2314.0
`C:\Program Files\WindowsApps\OpenAI.Codex_26.1007.2314.0_x64__2p2nqsd0c76g0`

| | Report |
|---|---|
| 01 | [Artifact manifest](codex/reports/01-artifact-manifest.md) |
| 02 | [IPC surface](codex/reports/02-ipc-surface.md) |
| 03 | [Sandbox & elevation boundary](codex/reports/03-sandbox-elevation-boundary.md) |
| 04 | [Native inventory](codex/reports/04-native-inventory.md) |
| 05 | [Update & signing](codex/reports/05-update-and-signing.md) |
| 06 | [Findings F1–F20, corrections C-A…C-Q](codex/reports/06-findings.md) |
| 07 | [Typeless comparison](codex/reports/07-typeless-comparison.md) |
| 08 | [Adversarial pass](codex/reports/08-adversarial-pass.md) |
| 09 | [Permission modes & workspace confinement](codex/reports/09-permission-modes-and-workspace-confinement.md) |
| 10 | [Orchestration, queueing & memory](codex/reports/10-orchestration-queue-and-memory.md) |
| 11 | [Voice pipeline](codex/reports/11-voice-pipeline.md) |

### Cross-project harness comparison
| | Report |
|---|---|
| 01 | [MiniMax Code agent orchestration](harness/01-agent-orchestration-explained.md) |
| 02 | [Sandbox census — jan, atomic-agents, smolagents, OpenHands, goose, open-interpreter](harness/02-sandbox-census-across-harnesses.md) |
| 03 | [Coven v0.0.54 vs the Claude baseline](harness/03-coven-sandbox-vs-claude.md) |

### Baselines & method
| | |
|---|---|
| [Typeless 2.8.1 verification review](verify/VERIFICATION-REVIEW.md) | |
| [Study queue](queue.md) | Running log of targets, findings, and corrections |

---

## How the evidence is recorded

Each product has an `evidence/` directory holding the scripts that produced its numbers and their
raw output, so any claim can be re-derived rather than trusted.

**Conventions used throughout:**

- **Occurrences, not lines.** The bundles are minified; line counts are meaningless.
- **A count always names its corpus.** Bytes *and* chars, and code separated from locale files.
  Coven's renderer census was 82% translation text until it was split — that correction is C-P.
- **"0 hits" is never evidence of absence.** Every negative is paired with a positive control run
  over the same corpus in the same pass.
- **CODE / DOC / VENDOR are separated.** A README sentence is not a sandbox; a vendored upstream
  repo is not your sandbox. Scoring `open-interpreter` at face value would have credited it with
  8,079 files of someone else's implementation.
- **Corrections stay visible.** Numbers are not quietly fixed after the fact — the corrections are
  where the interesting information lives. Currently: **C-A…C-Q** (Codex), **C-A…C-K** (Claude).

## Known limitations

- **Static only.** Nothing was executed. Reading code shows what is *written*, not what *happens*.
- **Versions move.** Findings are pinned to specific builds on specific dates. Coven's `main` was
  ~3 months ahead of the tag audited.
- **Scratch paths in evidence indexes are machine-local** (`%TEMP%\codex-src`, `%TEMP%\claude-src`,
  `%TEMP%\coven-audit`). The scripts that consume them are included; the extracted trees are not.
- **Open items carried forward** are listed in `queue.md` rather than quietly dropped.

## Conflict of interest

The analysis was performed **by an AI agent**. That creates a bias toward concluding agent tooling
needs hardening. Reports therefore credit the genuinely good findings — Codex's fail-closed
fallbacks, `jan`'s `enforces: bool` liveness signal, Coven's real code-enforced redaction and
candid `SECURITY.md`, goose documenting its own sandbox *removal* rather than erasing the trail —
but weigh the conclusions accordingly.

See [NOTICE.md](NOTICE.md) for third-party material.