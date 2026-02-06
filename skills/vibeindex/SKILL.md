---
name: vibeindex
description: Analyze your project and get personalized recommendations for Claude Code skills, MCP servers, and plugins
---

# vibeindex

Analyze your project and get personalized recommendations for Claude Code skills, MCP servers, and plugins from [Vibe Index](https://vibeindex.ai).

**No setup required!** Just install and use.

## Commands

### /vibeindex
Analyze your project and recommend matching resources.

```
/vibeindex
```

### /vibeindex search <query>
Search for resources by keyword.

```
/vibeindex search git
/vibeindex search database mcp
```

### /vibeindex top [type]
Show top resources by stars.

```
/vibeindex top
/vibeindex top skill
/vibeindex top mcp
```

### /vibeindex trending
Show trending resources this week.

```
/vibeindex trending
```

---

## How It Works

When the user runs `/vibeindex`, follow these steps:

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

**Use WebFetch to call Vibe Index API directly:**

```
WebFetch({
  url: "https://vibeindex.ai/api/resources?search=supabase&pageSize=5",
  prompt: "Extract resource names, types, descriptions, stars, and install commands"
})
```

| Detected | Search URL |
|----------|------------|
| React | `https://vibeindex.ai/api/resources?search=react&pageSize=5` |
| TypeScript | `https://vibeindex.ai/api/resources?search=typescript&pageSize=5` |
| Supabase | `https://vibeindex.ai/api/resources?search=supabase&pageSize=5` |
| Docker | `https://vibeindex.ai/api/resources?search=docker&pageSize=5` |
| Next.js | `https://vibeindex.ai/api/resources?search=nextjs&pageSize=5` |
| Python | `https://vibeindex.ai/api/resources?search=python&pageSize=5` |

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

```markdown
## Suggested for Your Project

Based on analysis:
- Framework: Next.js + React + TypeScript
- Database: Supabase

---

### 1. supabase-mcp (mcp)
**Match: 95%** - @supabase/supabase-js detected

Supabase MCP server for database operations with Row Level Security support.

Stars: 6,616 | Install: See https://vibeindex.ai/mcp/supabase/supabase-mcp

---

### 2. react-best-practices (skill)
**Match: 88%** - react detected in dependencies

Best practices for React development.

Stars: 12,345 | Install: `npx skills add owner/repo --skill react-best-practices`
```

---

## API Reference

All endpoints are public and require no authentication:

| Command | API Endpoint |
|---------|-------------|
| `/vibeindex search <query>` | `https://vibeindex.ai/api/resources?search={query}&pageSize=10` |
| `/vibeindex top` | `https://vibeindex.ai/api/resources?sort=stars&pageSize=10` |
| `/vibeindex top skill` | `https://vibeindex.ai/api/resources?sort=stars&type=skill&pageSize=10` |
| `/vibeindex trending` | `https://vibeindex.ai/api/rising-stars?period=week&limit=10` |

### Response Format

The resources API returns JSON with this structure:
```json
{
  "data": [
    {
      "name": "resource-name",
      "resource_type": "skill|mcp|plugin|marketplace",
      "description": "...",
      "description_ko": "...",
      "stars": 12345,
      "github_owner": "owner",
      "github_repo": "repo",
      "tags": ["tag1", "tag2"]
    }
  ],
  "total": 100
}
```

The rising-stars API (`/vibeindex trending`) returns a different format:
```json
{
  "rising": [
    {
      "name": "resource-name",
      "resource_type": "mcp",
      "stars": 5000,
      "stars_today": 120,
      "trending_rank": 1
    }
  ],
  "period": "week"
}
```

### Install Commands by Type

Generate install commands based on resource type:

- **skill**: `npx skills add {github_owner}/{github_repo} --skill {name}`
- **plugin**: Link to `https://vibeindex.ai/plugins/{github_owner}/{github_repo}/{name}`
- **mcp**: Link to `https://vibeindex.ai/mcp/{github_owner}/{github_repo}`
- **marketplace**: Link to `https://vibeindex.ai/marketplaces/{github_owner}/{github_repo}`

---

## Examples

### /vibeindex search git
```
WebFetch({
  url: "https://vibeindex.ai/api/resources?search=git&pageSize=10",
  prompt: "List the resources with name, type, description, stars. Format as markdown list."
})
```

### /vibeindex top mcp
```
WebFetch({
  url: "https://vibeindex.ai/api/resources?sort=stars&type=mcp&pageSize=10",
  prompt: "List top MCP servers with name, description, stars. Format as numbered list."
})
```

### /vibeindex trending
```
WebFetch({
  url: "https://vibeindex.ai/api/rising-stars?period=week&limit=10",
  prompt: "Show trending resources with star growth this week."
})
```

---

Built by [Vibe Index](https://vibeindex.ai) - The Claude Code Ecosystem Directory
