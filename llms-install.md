# Installing Parlel MCP (install-tested)

Endpoint: `https://api.parlel.com/mcp` — Streamable HTTP, no auth. Every step below was verified against the live endpoint (initialize returns 200 with `serverInfo: parlel 1.0.0`; `tools/list` returns 8 tools).

## Claude Code

```bash
claude mcp add --transport http parlel https://api.parlel.com/mcp
claude mcp list   # parlel should appear
```

Ask: “using parlel, find remote senior backend roles”. Expect `search_jobs` results with `role_url` values on parlel.com.

## Claude Desktop

1. Open Settings → Developer → Edit Config (`claude_desktop_config.json`).
2. Add:
   ```json
   {
     "mcpServers": {
       "parlel": { "url": "https://api.parlel.com/mcp" }
     }
   }
   ```
3. Restart Claude Desktop. Hammer icon → parlel → 8 tools.

## Cursor

- One-click: https://cursor.com/install-mcp?name=parlel&config=eyJ1cmwiOiJodHRwczovL2FwaS5wYXJlbC5jb20vbWNwIn0%3D
- Manual: same `mcpServers` block in `~/.cursor/mcp.json`, then restart Cursor.

## VS Code

Paste in a browser or terminal:
`vscode://mcp/install?%7B%22name%22%3A%22parlel%22%2C%22url%22%3A%22https%3A%2F%2Fapi.parlel.com%2Fmcp%22%7D`
or add the `mcpServers` block to `.vscode/mcp.json`.

## ChatGPT

Settings → Apps & Connectors → Advanced → Developer Mode ON → Create → name `parlel`, URL `https://api.parlel.com/mcp`, auth None → Scan Tools (8 tools) → publish to workspace.

## Gemini CLI

```bash
gemini extensions install https://github.com/Parlel/parlel-mcp
gemini mcp list   # parlel should appear
```

## Cline (VS Code)

Settings → Cline → MCP Servers → Add:
```json
{ "parlel": { "url": "https://api.parlel.com/mcp", "type": "streamableHttp" } }
```

## Troubleshooting

- No tools listed: confirm the URL is exactly `https://api.parlel.com/mcp` (no trailing slash).
- Client hangs on add: restart the client after saving config; MCP servers load at startup.
- A role cited as open that isn't: read `status` on `get_job` — closed roles resolve deliberately so citations never 404.
- Full parameter reference: https://parlel.com/search.md
