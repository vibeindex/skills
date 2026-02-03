---
name: versus
description: Compare two Claude Code resources side-by-side with objective data and recommendations
---

# versus

Compare two Claude Code resources side-by-side. Get objective data and recommendations based on your project context from [Vibe Index](https://vibeindex.ai).

## Prerequisites

This skill requires the **Vibe Index MCP Server** to be configured with an API key.

1. Get your free API key at https://vibeindex.ai/developer
2. Add to your MCP config (see https://vibeindex.ai/tools/mcp)

## Commands

### /versus <resource1> <resource2>
Compare two resources by name.

```
/versus postgres-mcp supabase-mcp
/versus react-best-practices nextjs-best-practices
/versus github gitlab
```

---

## How It Works

1. Search for both resources using `mcp__vibeindex__search`
2. Fetch detailed info for each
3. Generate comparison table
4. Analyze project context for recommendation

---

## Implementation

When the user runs `/versus A B`:

### Step 1: Search for Resources

```javascript
// Search for resource A
mcp__vibeindex__search({ query: "A", limit: 1 })

// Search for resource B
mcp__vibeindex__search({ query: "B", limit: 1 })
```

### Step 2: Generate Comparison

Build a comparison table with:

| Metric | Description |
|--------|-------------|
| Stars | GitHub star count |
| Type | skill / mcp / plugin |
| Description | What it does |
| Key Features | Main capabilities |
| Install | Installation command |

### Step 3: Analyze Project Context

Read `package.json` and project structure to determine which resource fits better.

---

## Output Format

```markdown
## ⚔️ postgres-mcp vs supabase-mcp

|                | postgres-mcp | supabase-mcp |
|----------------|--------------|--------------|
| **Type**       | mcp          | mcp          |
| **Stars**      | 2,341 ⭐     | 6,616 ⭐     |
| **Focus**      | Raw SQL      | Supabase API |

### postgres-mcp
Direct PostgreSQL access with raw SQL execution. Best for:
- Custom PostgreSQL setups
- Complex SQL queries
- No ORM overhead

### supabase-mcp
Supabase-native with RLS, Auth, and Realtime. Best for:
- Supabase projects
- Row Level Security
- Auth integration

---

## 🎯 Recommendation for Your Project

**Detected:** `supabase/` directory, `@supabase/supabase-js` in package.json

→ **supabase-mcp** is the better fit for your project.

You're already using Supabase, so the native MCP will integrate seamlessly with your existing RLS policies and auth setup.

---

**Install supabase-mcp:**
See setup guide at https://vibeindex.ai/mcp/supabase/supabase-mcp
```

---

## Edge Cases

### Similar Names
If search returns multiple matches, ask user to clarify:
```
Found multiple matches for "postgres":
1. postgres-mcp (mcp)
2. postgres-best-practices (skill)

Which one did you mean?
```

### No Match Found
```
Could not find "xyz" in Vibe Index.
Try searching: /vibe search xyz
```

### Same Resource
```
Both names refer to the same resource: supabase-mcp
Nothing to compare!
```

---

Built by [Vibe Index](https://vibeindex.ai)
