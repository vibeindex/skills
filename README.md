# Vibe Index Skills

Official Claude Code skills from [Vibe Index](https://vibeindex.ai) - the comprehensive directory for Claude Code ecosystem.

## Available Skills

| Skill | Command | Description |
|-------|---------|-------------|
| **vibeindex** | `/vibeindex` | Analyze your project and get personalized recommendations |
| **rising** | `/rising` | Discover trending resources on GitHub |
| **versus** | `/versus A B` | Compare two resources side-by-side |
| **ecosystem** | `/ecosystem` | Dashboard view of the Claude Code ecosystem |
| **new** | `/new` | See recently added resources |

## Installation

### Install All Skills
```bash
npx skills add vibeindex/skills
```

### Install Individual Skills
```bash
npx skills add vibeindex/skills --skill vibeindex
npx skills add vibeindex/skills --skill rising
npx skills add vibeindex/skills --skill versus
npx skills add vibeindex/skills --skill ecosystem
npx skills add vibeindex/skills --skill new
```

## Quick Start

```bash
# Analyze your project
/vibeindex

# See what's trending
/rising

# Compare two MCP servers
/versus postgres-mcp supabase-mcp

# Check ecosystem stats
/ecosystem

# See newest resources
/new
```

## Links

- **Website:** https://vibeindex.ai
- **API Docs:** https://vibeindex.ai/developer
- **MCP Setup:** https://vibeindex.ai/tools/mcp
- **Submit Resource:** https://vibeindex.ai/submit

## License

MIT

---

Built by [Vibe Index](https://vibeindex.ai)
