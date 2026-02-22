# Learning Skill for Claude Code

A skill that teaches Claude to record learnings (failures + fixes) and retrieve them to avoid repeating mistakes.

## Install

```bash
bash install.sh
```

Then restart Claude Code (`/restart` or new session).

## How It Works

**Two layers:**

1. **Skill (real-time)** -- Claude recognizes failures during a session and records them using a structured schema
2. **Hook (safety net)** -- A Stop hook analyzes the transcript for failure-to-fix patterns that weren't captured in-session

**Two storage backends:**

- **Memories MCP** (if available) -- semantic search, deduplication, cross-project retrieval
- **Auto-memory files** (default fallback) -- appends to `learnings.md` in the project's memory directory

## Schema

```
[LEARNING] <category>: <one-line summary>
TRIED: <what was attempted and why it didn't work>
SOLUTION: <what actually worked>
CONTEXT: <project/tool/language>
```

Categories: `debugging`, `implementation`, `infra/config`, `api-usage`, `tooling`

## Usage

The skill activates automatically when Claude encounters a failure and finds the fix. No manual invocation needed -- it's listed in Claude's available skills and triggers based on context.

To manually invoke: reference "learning" skill or type patterns that match its trigger conditions.
