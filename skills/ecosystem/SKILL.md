# ecosystem

Get a dashboard view of the Claude Code ecosystem. See total resources, category breakdown, recent additions, and trends from [Vibe Index](https://vibeindex.ai).

## Prerequisites

This skill requires the **Vibe Index MCP Server** to be configured with an API key.

1. Get your free API key at https://vibeindex.ai/developer
2. Add to your MCP config (see https://vibeindex.ai/tools/mcp)

## Commands

### /ecosystem
Show full ecosystem dashboard.

```
/ecosystem
```

---

## How It Works

Aggregates data from Vibe Index to show:
- Total resource counts by type
- Category distribution
- Recent additions
- Trending summary

---

## Implementation

When the user runs `/ecosystem`:

### Step 1: Gather Statistics

Use multiple MCP calls in parallel:

```javascript
// Get top resources for counts
mcp__vibeindex__top({ type: "skill", limit: 1 })
mcp__vibeindex__top({ type: "mcp", limit: 1 })
mcp__vibeindex__top({ type: "plugin", limit: 1 })
mcp__vibeindex__top({ type: "marketplace", limit: 1 })

// Get categories
mcp__vibeindex__categories()

// Get trending
mcp__vibeindex__trending({ period: "week", limit: 3 })
```

### Step 2: Format Dashboard

---

## Output Format

```markdown
## 📊 Claude Code Ecosystem

**Last updated:** February 2, 2025

---

### Resource Overview

| Type | Count | Top Resource |
|------|-------|--------------|
| Skills | 500+ | github (118k ⭐) |
| MCP Servers | 400+ | filesystem (77k ⭐) |
| Plugins | 250+ | commit-commands (61k ⭐) |
| Marketplaces | 20+ | claude-code (61k ⭐) |

**Total: 1,200+ resources**

---

### 🔥 Trending This Week

1. **claude-code-toolkit** (+523 ⭐)
2. **supabase-mcp** (+312 ⭐)
3. **cursor-rules** (+289 ⭐)

---

### 📂 Popular Categories

| Category | Resources |
|----------|-----------|
| AI / LLM | 234 |
| Database | 156 |
| DevOps | 89 |
| Frontend | 145 |
| Git / GitHub | 78 |

---

### 🆕 Recently Added

- **new-skill-name** (skill) - 2 hours ago
- **another-mcp** (mcp) - 5 hours ago
- **cool-plugin** (plugin) - 1 day ago

---

### Quick Links

- Browse all: https://vibeindex.ai/browse
- Submit resource: https://vibeindex.ai/submit
- API docs: https://vibeindex.ai/developer

---

*Data from [Vibe Index](https://vibeindex.ai)*
```

---

## Use Cases

- **New users**: Understand the ecosystem size and scope
- **Developers**: Find popular categories to contribute to
- **Decision makers**: Gauge ecosystem maturity

---

Built by [Vibe Index](https://vibeindex.ai)
