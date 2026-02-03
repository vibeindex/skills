# Vibe Index Skills

Official Claude Code skills from [Vibe Index](https://vibeindex.ai) - the comprehensive directory for Claude Code ecosystem.

## Prerequisites

These skills require the **Vibe Index MCP Server**:

1. Get your free API key at https://vibeindex.ai/developer
2. Add to your MCP config: https://vibeindex.ai/tools/mcp

## Available Skills

| Skill | Command | Description |
|-------|---------|-------------|
| **vibe** | `/vibe` | Analyze your project and get personalized recommendations |
| **rising** | `/rising` | Discover trending resources on GitHub |
| **versus** | `/versus A B` | Compare two resources side-by-side |
| **ecosystem** | `/ecosystem` | Dashboard view of the Claude Code ecosystem |
| **new** | `/new` | See recently added resources |

## Installation

### Install All Skills
```bash
claude skill add vibeindex/skills
```

### Install Individual Skills
```bash
claude skill add vibeindex/skills/vibe
claude skill add vibeindex/skills/rising
claude skill add vibeindex/skills/versus
claude skill add vibeindex/skills/ecosystem
claude skill add vibeindex/skills/new
```

## Quick Start

```bash
# Analyze your project
/vibe

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
