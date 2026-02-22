---
name: learning
description: Use when you encounter a failure, dead end, or wrong approach and discover the fix, or before attempting something you've struggled with before
---

# Recording Learnings

## Overview

Capture what went wrong and what fixed it so you never repeat the same mistake. This skill is **rigid** -- follow it exactly.

## When to Use

- You tried something that didn't work and found the fix
- A debugging session concluded with a root cause identified
- You're about to attempt something in an area where past failures occurred
- The user points out you made a mistake you should remember

## The Schema

Every learning follows this format:

```
[LEARNING] <category>: <one-line summary>
TRIED: <what was attempted and why it didn't work>
SOLUTION: <what actually worked>
CONTEXT: <project/tool/language>
```

**Categories:** `debugging`, `implementation`, `infra/config`, `api-usage`, `tooling`

## Storage Backend Detection

**Check once per session:**

1. If `mcp__memories__memory_add` tool is available → use **Memories MCP**
2. Otherwise → use **Auto-memory files**

Do NOT mix backends in a single session.

## Recording a Learning

### With Memories MCP

1. **Check novelty first:**
   ```
   mcp__memories__memory_is_novel(text="<one-line summary of the learning>")
   ```
   If not novel, skip recording.

2. **Record:**
   ```
   mcp__memories__memory_add(
     text="[LEARNING] <category>: <summary>\nTRIED: <what failed>\nSOLUTION: <what worked>\nCONTEXT: <project/tool>",
     source="learning/<project-name>"
   )
   ```

### With Auto-memory Files

1. **Read existing learnings:**
   Read `~/.claude/projects/<project-path>/memory/learnings.md`
   If a similar learning already exists, skip.

2. **Append:**
   Edit the file to append:
   ```
   ## <category>: <one-line summary>
   - **Tried:** <what failed>
   - **Solution:** <what worked>
   - **Context:** <project/tool>
   ```

## Retrieving Learnings

Before attempting work in a problem area, search for relevant past learnings:

### With Memories MCP
```
mcp__memories__memory_search(query="<description of what you're about to do>", k=5)
```

### With Auto-memory Files
Read `learnings.md` and scan for relevant entries.

## When to Record (Checklist)

After resolving any of these, STOP and record before moving on:

- [ ] Tried an approach that failed, then found the right one
- [ ] Discovered a tool/API behaves differently than expected
- [ ] A config or setup issue took multiple attempts to resolve
- [ ] Found a non-obvious root cause for a bug
- [ ] User corrected your approach

## Red Flags -- You're Skipping This

| Thought | Reality |
|---------|---------|
| "This was too simple to record" | Simple mistakes are the ones you repeat |
| "I'll remember this" | You won't. Context windows reset |
| "This is project-specific" | Patterns transfer across projects |
| "Let me finish first" | Record NOW while context is fresh |

## Quick Reference

| Step | Action |
|------|--------|
| 1 | Recognize: you failed and found the fix |
| 2 | Check: is this already recorded? |
| 3 | Record: use the [LEARNING] schema |
| 4 | Before similar work: search past learnings |
