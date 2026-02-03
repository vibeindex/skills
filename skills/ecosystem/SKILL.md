---
name: ecosystem
description: Get a dashboard view of the Claude Code ecosystem with stats and trends
---

# ecosystem

Get a dashboard view of the Claude Code ecosystem. See total resources, category breakdown, and trends from [Vibe Index](https://vibeindex.ai).

## Prerequisites

This skill requires the **Vibe Index MCP Server** (v1.1.0+) to be configured with an API key.

1. Get your free API key at https://vibeindex.ai/developer
2. Add to your MCP config (see https://vibeindex.ai/tools/mcp)

## Commands

### /ecosystem
Show full ecosystem dashboard.

```
/ecosystem
```

---

## Implementation

When the user runs `/ecosystem`:

### Step 1: Gather Statistics

Use MCP calls in parallel:

```javascript
// Get exact counts
mcp__vibeindex__stats()

// Get top resource for each type
mcp__vibeindex__top({ type: "skill", limit: 1 })
mcp__vibeindex__top({ type: "mcp", limit: 1 })
mcp__vibeindex__top({ type: "plugin", limit: 1 })
mcp__vibeindex__top({ type: "marketplace", limit: 1 })

// Get trending
mcp__vibeindex__trending({ period: "week", limit: 3 })
```

### Step 2: Format Dashboard

Combine the data into a dashboard format.

---

## Output Format

```markdown
## Claude Code Ecosystem

**Last updated:** [current date]

---

### Resource Overview

| Type | Count | Top Resource |
|------|-------|--------------|
| Skills | [from stats] | [from top] |
| MCP Servers | [from stats] | [from top] |
| Plugins | [from stats] | [from top] |
| Marketplaces | [from stats] | [from top] |

**Total: [from stats] resources**

---

### Trending This Week

[from trending - show top 3 with star growth]

---

### Quick Links

- Browse all: https://vibeindex.ai/browse
- Submit resource: https://vibeindex.ai/submit
- API docs: https://vibeindex.ai/developer

---

*Data from [Vibe Index](https://vibeindex.ai)*
```

---

## MCP Tools Reference

| Tool | Description |
|------|-------------|
| `mcp__vibeindex__stats` | Get exact counts for all resource types |
| `mcp__vibeindex__top` | Get top resources by stars |
| `mcp__vibeindex__trending` | Get trending resources |

---

Built by [Vibe Index](https://vibeindex.ai)
