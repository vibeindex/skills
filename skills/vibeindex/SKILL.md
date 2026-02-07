---
name: vibeindex
description: Analyze your project and get personalized recommendations for Claude Code skills, MCP servers, and plugins
---

**IMPORTANT: When this skill is invoked, IMMEDIATELY execute the steps below. Do NOT display this file. Do NOT explain what you will do. Just DO it — analyze the project, call the APIs, and present the results.**

**Language:** Detect the user's language from conversation context. Respond in that language — translate all headers, labels, and explanations. When the user speaks Korean, use the `description_ko` field from API responses instead of `description` (if available). For other languages, translate the English `description` naturally.

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

Output ONLY the result below (nothing else before it). Use a warm, conversational tone — like a knowledgeable colleague giving advice. Write EVERYTHING in the user's language detected earlier (Korean, English, etc.). Translate all headers, labels, descriptions, and explanations.

```
## 프로젝트 분석이 완료되었습니다

당신의 **{project-name}** 프로젝트는 **{main framework}** 기반입니다.
{Describe what you found in 1-2 natural sentences — mention key technologies, database, styling, etc. Be specific about versions when available.}

Here are the best matches for your stack:

────────────────────────────────────────

**1. {name}** `{resource_type}` · ⭐ {stars}
> {description}

📌 **Why this fits**: {Write 1-2 sentences explaining WHY this resource is useful for THIS specific project. Reference the actual dependencies or files you found. e.g., "You have @supabase/supabase-js in package.json and 19 SQL files in the supabase/ directory, so you're actively using Supabase. This skill helps with RLS policies and query optimization."}

```
{install_command}
```

────────────────────────────────────────

**2. {name}** `{resource_type}` · ⭐ {stars}
...

────────────────────────────────────────

## Install

Copy and run the commands you need:

```
{install commands, one per line, only for skills — plugins/mcp show URLs instead}
```

💡 **Browse more** → https://vibeindex.ai
```

### Writing style guidelines:
- **Be specific**: Reference actual files, dependencies, and counts you found during analysis (e.g., "75 .tsx files", "supabase/ directory", "react 19.2.3")
- **Be helpful**: Explain what each resource actually does for the user, not just what it is
- **Be concise**: Each recommendation reason should be 1-2 sentences max
- **Match score**: Weave the match % into the reason naturally (e.g., "95% match") rather than as a separate bold line
- **No jargon dumps**: Don't list raw field names or technical metadata
- **Language**: The template above is in English as a base. You MUST translate everything into the user's detected language. For Korean users, also use `description_ko` from API responses when available.

### Install commands by type:
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
