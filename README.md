# Parlel MCP Server

Search **people, companies, and open roles** on [Parlel](https://parlel.com), an open professional network — from any MCP client. Free, no API key, no sign-up.

- **Endpoint:** `https://api.parlel.com/mcp` (Streamable HTTP, stateless)
- **Full guide:** [parlel.com/search.md](https://parlel.com/search.md) — every parameter, worked `curl` examples, paging
- **Machine index:** [api.parlel.com/api/public/index](https://api.parlel.com/api/public/index) · **OpenAPI:** [api.parlel.com/api/public/openapi.json](https://api.parlel.com/api/public/openapi.json)
- **Registry:** `com.parlel/parlel` on the [official MCP Registry](https://registry.modelcontextprotocol.io)

## Tools

| Tool | What it does |
|---|---|
| `search_jobs` | Open roles. `q` matches the **title only**; filter by `remote`, `seniority`, `comp_min` |
| `get_job` | One role with description, skills, pay, company. Closed roles resolve too — read `status` |
| `search_companies` | Companies. `q` matches name/tagline/industry; `industry` is exact; `hiring=true` narrows to hiring |
| `get_company` | One company with open roles inline |
| `search_people` | Published profiles. `q` matches name/headline/company/history (**not** skills/bio); `skill` is exact and AND-ed |
| `get_person` | One profile: headline, bio, work history, education, skills, posts, published agents |
| `search_agents` | Published watch agents (`sort=recent\|popular`) |
| `get_agent` | One agent: brief, schedule, findings with sources |

Lists return `{items, next_cursor}`; pass `next_cursor` back as `cursor`. Contact details are never returned.

## Install

**Claude Code**

```bash
claude mcp add --transport http parlel https://api.parlel.com/mcp
```

**Claude Desktop** (`claude_desktop_config.json`)

```json
{
  "mcpServers": {
    "parlel": {
      "url": "https://api.parlel.com/mcp"
    }
  }
}
```

**Cursor** — [one-click install](https://cursor.com/install-mcp?name=parlel&config=eyJ1cmwiOiJodHRwczovL2FwaS5wYXJlbC5jb20vbWNwIn0%3D), or add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "parlel": {
      "url": "https://api.parlel.com/mcp"
    }
  }
}
```

**VS Code** — `vscode://mcp/install?%7B%22name%22%3A%22parlel%22%2C%22url%22%3A%22https%3A%2F%2Fapi.parlel.com%2Fmcp%22%7D`, or `.vscode/mcp.json` with the same `mcpServers` block.

**ChatGPT** — Settings → Apps & Connectors → Developer Mode → Create, paste `https://api.parlel.com/mcp`, auth None.

**Gemini CLI** — this repo is a Gemini extension: `gemini extensions install https://github.com/Parlel/parlel-mcp`

## Example prompts

- “Find remote senior backend roles paying over £130k on Parlel”
- “Find Rust and Go engineers in Berlin who are open to work”
- “Which small fintechs in London are hiring right now?”

## Source

This repo is a public brochure for the hosted endpoint. The server implementation lives in the private `Parlel/parlel-mono` monorepo (`apps/api/src/api/routes/mcp_server.py`). `server.json` here is the canonical registry metadata.
