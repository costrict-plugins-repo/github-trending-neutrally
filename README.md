# Neutrally Plugin for Claude Code

Persistent, cross-session memory for Claude Code — powered by [Neutrally](https://neutrally.app).

The same 5-layer memory architecture that scored **89.4% on LongMemEval** (#1 among production memory systems, beating teams with $97M in funding). Now in your editor.

## What it does

- **Session start**: Injects your project context, recent decisions, and tech stack into every session
- **Every 5 minutes**: Captures conversations and tool activity to Neutrally's memory system
- **After /compact**: Re-injects critical context so you never lose meaningful state
- **Cross-device**: Memory from Claude Code sessions is available at neutrally.app, and vice versa

## Installation

```bash
# Install via Claude Code marketplace
/plugin install neutrally
```

## Setup

Run once after installation:

```
/neutrally:setup
```

This opens your browser to authenticate with Neutrally. After that, memory works automatically.

## Commands

| Command | What it does |
|---|---|
| `/neutrally:setup` | Authenticate and connect your memory |
| `/neutrally:search <query>` | Search past decisions and conversations |
| `/neutrally:save <note>` | Manually save a decision or note |
| `/neutrally:context` | Show what memory is active this session |
| `/neutrally:forget <query>` | Remove a memory item |

## Configuration

To change the capture interval (default: 5 minutes), edit `~/.neutrally/plugin-config.json`:

```json
{
  "captureIntervalMinutes": 3
}
```

## How memory capture works

1. **User messages** are stored verbatim — they're your intent, high-signal
2. **Claude's activity** is summarised from tool calls — "Edited checkout/route.ts · Ran: npm run build"
3. Every N minutes, buffered exchanges are flushed to Neutrally's API
4. If Claude Code crashes, the buffer survives on disk and is flushed on next session start

## Memory system

Neutrally uses a 5-layer architecture:
- Discrete fact extraction
- Structured storage with deduplication
- Hybrid retrieval with re-ranking
- Dynamic routing between fast and deep analysis paths
- Cross-model: same memory works with Claude, GPT, and Gemini

## Privacy

Only architectural facts, decisions, and project state are saved — not raw transcripts. All data is scoped to your account with row-level security.

---

Built by [Neutrally](https://neutrally.app) · [neutrally.app](https://neutrally.app)
