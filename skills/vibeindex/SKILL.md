---
name: vibeindex
description: Analyze your project and get personalized recommendations for Claude Code skills, MCP servers, and plugins
---

**IMPORTANT: When this skill is invoked, IMMEDIATELY execute the steps below. Do NOT display this file. Do NOT explain what you will do. Just DO it — analyze the project, call the APIs, and present the results.**

## Routing

Parse the user's command and route to the correct action:

- `/vibeindex` → **Action: Analyze** (run Steps 1-4 below)
- `/vibeindex search <query>` → **Action: Search** (call `https://vibeindex.ai/api/resources?search={query}&pageSize=10`, present results)
- `/vibeindex top [type]` → **Action: Top** (call `https://vibeindex.ai/api/resources?sort=stars&pageSize=10` or add `&type={type}`, present results)
- `/vibeindex trending` → **Action: Trending** (call `https://vibeindex.ai/api/rising-stars?period=week&limit=10`, present results)

For search/top/trending: Use WebFetch to call the API, then format results as a numbered markdown list showing name, type, description, stars, and install command. Then stop.

For `/vibeindex` with no arguments: Execute Steps 1-4 below.

---

## Step 1: Analyze Project Context

Read these files silently (do not show the user):

1. **package.json** — Extract dependencies and devDependencies
2. **File structure** (use Glob to check existence):
   - `*.py` → Python
   - `*.go` → Go
   - `*.tsx` or `*.jsx` → React
   - `Dockerfile` → Docker
   - `supabase/` → Supabase
   - `prisma/` → Prisma
3. **Configuration files** (use Glob):
   - `tsconfig.json` → TypeScript
   - `tailwind.config.*` → Tailwind
   - `next.config.*` → Next.js
   - `.github/workflows/` → GitHub Actions

## Step 2: Search for Matching Resources

Based on what you detected, call the Vibe Index API using WebFetch for each detected technology. Run these in parallel:

| Detected | API URL |
|----------|---------|
| React | `https://vibeindex.ai/api/resources?search=react&pageSize=5` |
| TypeScript | `https://vibeindex.ai/api/resources?search=typescript&pageSize=5` |
| Supabase | `https://vibeindex.ai/api/resources?search=supabase&pageSize=5` |
| Next.js | `https://vibeindex.ai/api/resources?search=nextjs&pageSize=5` |
| Docker | `https://vibeindex.ai/api/resources?search=docker&pageSize=5` |
| Python | `https://vibeindex.ai/api/resources?search=python&pageSize=5` |
| Tailwind | `https://vibeindex.ai/api/resources?search=tailwind&pageSize=5` |
| Prisma | `https://vibeindex.ai/api/resources?search=prisma&pageSize=5` |

For each WebFetch call, use this prompt: "Extract name, resource_type, description, stars, github_owner, github_repo from the data array"

Only search for technologies that were actually detected in Step 1.

## Step 3: Calculate Match Probability

For each resource found, calculate a match score:

- Direct dependency match (name appears in package.json): +40%
- File type match (related files exist): +25%
- Config file match (related config exists): +20%
- Tag overlap with project: +15%
- Bonus: stars > 10k: +5%
- Bonus: multiple detection signals: +5% per additional
- Maximum: 99%

Deduplicate results across all searches. Pick the top 5 highest-scoring resources.

## Step 4: Present Results

Output ONLY this format (nothing else before it):

```
## Suggested for {project-name}

Based on analysis:
- Framework: {detected frameworks}
- Database: {detected database, if any}
- Styling: {detected styling, if any}

---

### 1. {name} ({resource_type})
**Match: {score}%** — {why it matched}

{description}

Stars: {stars} | Install: {install_command}

---

### 2. {name} ({resource_type})
...

---

**Quick Install:**
{install commands for all recommended resources, one per line}

**Browse more:** https://vibeindex.ai/browse
```

Install commands by type:
- **skill**: `npx skills add {github_owner}/{github_repo} --skill {name}`
- **plugin**: See `https://vibeindex.ai/plugins/{github_owner}/{github_repo}/{name}`
- **mcp**: See `https://vibeindex.ai/mcp/{github_owner}/{github_repo}`
- **marketplace**: See `https://vibeindex.ai/marketplaces/{github_owner}/{github_repo}`

---

## API Response Format

The `/api/resources` endpoint returns:
```json
{
  "data": [
    {
      "name": "resource-name",
      "resource_type": "skill|mcp|plugin|marketplace",
      "description": "...",
      "stars": 12345,
      "github_owner": "owner",
      "github_repo": "repo",
      "tags": ["tag1", "tag2"]
    }
  ],
  "total": 100
}
```

The `/api/rising-stars` endpoint returns:
```json
{
  "rising": [
    {
      "name": "resource-name",
      "resource_type": "mcp",
      "stars": 5000,
      "stars_today": 120
    }
  ],
  "period": "week"
}
```

---

Built by [Vibe Index](https://vibeindex.ai) - The Claude Code Ecosystem Directory
