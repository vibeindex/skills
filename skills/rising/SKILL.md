# rising

Discover trending Claude Code resources that are rising on GitHub right now. Shows resources from [Vibe Index](https://vibeindex.ai) that are currently trending on GitHub.

## Prerequisites

This skill requires the **Vibe Index MCP Server** to be configured with an API key.

1. Get your free API key at https://vibeindex.ai/developer
2. Add to your MCP config (see https://vibeindex.ai/tools/mcp)

## Commands

### /rising
Show resources trending on GitHub today.

```
/rising
```

### /rising week
Show resources trending this week.

```
/rising week
```

### /rising month
Show resources trending this month.

```
/rising month
```

### /rising [type]
Filter by resource type (skill, mcp, plugin).

```
/rising mcp
/rising skill week
```

---

## How It Works

This skill combines **GitHub Trending** data with **Vibe Index** database:

1. Fetch GitHub Trending repositories
2. Match with resources in Vibe Index
3. Show matched resources with trending stats

This means you see resources that are:
- Rising in popularity on GitHub
- Already curated in Vibe Index

---

## Implementation

When the user runs `/rising`, use the `mcp__vibeindex__trending` tool:

```
mcp__vibeindex__trending
├── period: "day" | "week" | "month"
└── limit: 10 (default)
```

### Output Format

```markdown
## 🔥 Rising on GitHub

Resources from Vibe Index currently trending on GitHub:

### #1 claude-code-toolkit (skill)
**+523 stars today** | Total: 4,521 ⭐
Comprehensive toolkit for Claude Code development
→ `claude skill add owner/repo/claude-code-toolkit`

---

### #2 supabase-mcp (mcp)
**+312 stars today** | Total: 6,616 ⭐
Supabase MCP server with RLS support
→ See MCP config at vibeindex.ai

---

### #3 cursor-rules (skill) 🆕
**+289 stars today** | Total: 1,234 ⭐
New entry this week!
→ `claude skill add owner/repo/cursor-rules`

---

See full rankings: https://vibeindex.ai
```

### Badge Display

- 🆕 **New entry** - First time trending
- 🔥 **Hot** - Unusual spike in stars
- 📈 **Rising** - Consistent growth

---

## Why This Matters

GitHub Trending shows what the developer community cares about right now. By filtering to Vibe Index resources, you get:

- **Quality filter** - Already curated resources
- **Relevance** - Claude Code ecosystem only
- **Install ready** - Immediate install commands

---

Built by [Vibe Index](https://vibeindex.ai)
