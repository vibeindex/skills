---
name: vibe
description: Analyze your project and get personalized recommendations for Claude Code skills, MCP servers, and plugins
---

# vibe

Analyze your project and get personalized recommendations for Claude Code skills, MCP servers, and plugins from [Vibe Index](https://vibeindex.ai).

## Prerequisites

This skill requires the **Vibe Index MCP Server** to be configured with an API key.

1. Get your free API key at https://vibeindex.ai/developer
2. Add to your MCP config (see https://vibeindex.ai/tools/mcp)

## Commands

### /vibe
Analyze your project and recommend matching resources with detailed descriptions.

```
/vibe
```

### /vibe -s
Show recommendations in a compact table format.

```
/vibe -s
```

### /vibe search <query>
Search for resources by keyword.

```
/vibe search git
/vibe search database mcp
```

### /vibe top [type]
Show top resources by stars.

```
/vibe top
/vibe top skill
/vibe top mcp
```

### /vibe install <name>
Get install command for a specific resource.

```
/vibe install github
```

---

## How It Works

When the user runs `/vibe`, follow these steps:

### Step 1: Analyze Project Context

Read the following files to understand the project:

1. **package.json** - Extract dependencies
2. **File structure** (use Glob)
   - `*.py` → Python
   - `*.go` → Go
   - `*.tsx/*.jsx` → React
   - `Dockerfile` → Docker
   - `supabase/` → Supabase
   - `prisma/` → Prisma
3. **Configuration files**
   - `tsconfig.json` → TypeScript
   - `tailwind.config.*` → Tailwind
   - `next.config.*` → Next.js
   - `.github/workflows/` → GitHub Actions

### Step 2: Search for Matching Resources

Use `mcp__vibeindex__search` for each detected technology:

| Detected | Search Query |
|----------|--------------|
| React | `react` |
| TypeScript | `typescript` |
| Supabase | `supabase` |
| Docker | `docker` |
| Next.js | `nextjs` |
| Python | `python` |

### Step 3: Calculate Match Probability

```
Base Score:
- Direct dependency match: +40%
- File type match: +25%
- Config file match: +20%
- Tag overlap: +15%

Bonuses:
- High stars (>10k): +5%
- Multiple matches: +5% per additional

Maximum: 99%
```

### Step 4: Present Results

**Full format (`/vibe`):**
```markdown
## Suggested for Your Project

Based on analysis:
- Framework: Next.js + React + TypeScript
- Database: Supabase

---

### 1. supabase-mcp (mcp)
**Match: 95%** - @supabase/supabase-js detected

Supabase MCP server for database operations with Row Level Security support.

Stars: 6,616 | Install: See MCP config
```

**Short format (`/vibe -s`):**
```markdown
| Match | Name | Type | Install |
|-------|------|------|---------|
| 95% | supabase-mcp | mcp | See config |
| 88% | react-best-practices | skill | `claude skill add ...` |
```

---

## MCP Tools Reference

| Tool | Parameters |
|------|------------|
| `mcp__vibeindex__search` | `query`, `type?`, `limit?` |
| `mcp__vibeindex__top` | `type?`, `limit?` |
| `mcp__vibeindex__install` | `name`, `type?` |

---

Built by [Vibe Index](https://vibeindex.ai)
