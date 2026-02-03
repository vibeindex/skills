---
name: new
description: Discover the latest Claude Code resources added to Vibe Index
---

# new

Discover the latest Claude Code resources from [Vibe Index](https://vibeindex.ai).

**No setup required!** Just install and use.

## Commands

### /new
Show recently added resources.

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
Show specific number of resources.

```
/new 20
```

---

## Implementation

When the user runs `/new [type] [limit]`:

### Fetch Recent Resources

Use WebFetch to get recent resources:

```
WebFetch({
  url: "https://vibeindex.ai/api/resources?sort=newest&pageSize=10",
  prompt: "List recently added resources with name, type, description, stars, and created date"
})
```

With type filter:
```
WebFetch({
  url: "https://vibeindex.ai/api/resources?sort=newest&type=skill&pageSize=10",
  prompt: "List recently added skills"
})
```

### Output Format

```markdown
## 🆕 Recently Added to Vibe Index

---

### Skills

1. **typescript-patterns** - Added 2 hours ago
   Advanced TypeScript patterns for Claude Code
   ⭐ 234 | `npx skills add owner/repo --skill typescript-patterns`

2. **react-hooks-guide** - Added 1 day ago
   Comprehensive React Hooks reference
   ⭐ 156 | `npx skills add owner/repo --skill react-hooks-guide`

---

### MCP Servers

1. **notion-mcp** - Added 3 hours ago
   Notion API integration for Claude
   ⭐ 567 | See https://vibeindex.ai/mcps/...

---

**Browse all:** https://vibeindex.ai/browse?sort=newest
**Submit yours:** https://vibeindex.ai/submit
```

---

## API Reference

| Command | API Endpoint |
|---------|-------------|
| `/new` | `https://vibeindex.ai/api/resources?sort=newest&pageSize=10` |
| `/new skill` | `https://vibeindex.ai/api/resources?sort=newest&type=skill&pageSize=10` |
| `/new mcp` | `https://vibeindex.ai/api/resources?sort=newest&type=mcp&pageSize=10` |
| `/new 20` | `https://vibeindex.ai/api/resources?sort=newest&pageSize=20` |

---

## Related Commands

- `/rising` - Trending resources (popularity)
- `/vibe top` - All-time top resources (stars)
- `/ecosystem` - Full ecosystem overview

---

Built by [Vibe Index](https://vibeindex.ai)
