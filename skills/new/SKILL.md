---
name: new
description: Discover the latest Claude Code resources added to Vibe Index
---

# new

Discover the latest Claude Code resources added to [Vibe Index](https://vibeindex.ai). Stay up-to-date with new skills, MCP servers, and plugins.

## Prerequisites

This skill requires the **Vibe Index MCP Server** with an API key.

### Setup

1. Get your free API key at https://vibeindex.ai/developer

2. Add to your Claude Code settings (`~/.claude/settings.json`):

```json
{
  "mcpServers": {
    "vibeindex": {
      "command": "npx",
      "args": ["-y", "vibeindex-mcp"],
      "env": {
        "VIBE_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

3. Restart Claude Code

## Commands

### /new
Show recently added resources (last 7 days).

```
/new
```

### /new [type]
Filter by resource type.

```
/new skill
/new mcp
/new plugin
```

### /new [number]
Show specific number of recent resources.

```
/new 20
/new skill 10
```

---

## How It Works

Fetches resources from Vibe Index sorted by creation date, showing the newest additions to the ecosystem.

---

## Implementation

When the user runs `/new`:

### API Call

Use `mcp__vibeindex__search` with empty query and sort by date:

```javascript
// Search with no query returns recent
mcp__vibeindex__search({
  query: "",
  type: "all",  // or specific type
  limit: 10
})
```

Note: Results are sorted by relevance by default. For newest resources, filter by checking recent dates or use the trending endpoint as a proxy for new popular resources.

---

## Output Format

```markdown
## 🆕 Recently Added to Vibe Index

*Last 7 days*

---

### Skills (5 new)

1. **typescript-patterns** - 2 hours ago
   Advanced TypeScript patterns for Claude Code
   ⭐ 234 | `claude skill add owner/repo/typescript-patterns`

2. **react-hooks-guide** - 1 day ago
   Comprehensive React Hooks reference
   ⭐ 156 | `claude skill add owner/repo/react-hooks-guide`

3. **python-debugging** - 2 days ago
   Python debugging techniques and tools
   ⭐ 89 | `claude skill add owner/repo/python-debugging`

---

### MCP Servers (3 new)

1. **notion-mcp** - 3 hours ago
   Notion API integration for Claude
   ⭐ 567 | See MCP config

2. **linear-mcp** - 1 day ago
   Linear issue tracking integration
   ⭐ 234 | See MCP config

---

### Plugins (2 new)

1. **test-runner** - 5 hours ago
   Automated test execution plugin
   ⭐ 123 | `claude plugin add owner/repo`

---

**Browse all:** https://vibeindex.ai/browse?sort=newest
**Submit yours:** https://vibeindex.ai/submit
```

---

## Why Track New Resources?

- **Early adopter advantage** - Try new tools before they become mainstream
- **Ecosystem growth** - See how fast the ecosystem is expanding
- **Contribution ideas** - Find gaps to fill with your own resources

---

## Related Commands

- `/rising` - Trending resources (popularity)
- `/vibe top` - All-time top resources (stars)
- `/ecosystem` - Full ecosystem overview

---

Built by [Vibe Index](https://vibeindex.ai)
