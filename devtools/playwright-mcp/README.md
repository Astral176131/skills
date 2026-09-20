# Playwright MCP

Source: [microsoft/playwright-mcp](https://github.com/microsoft/playwright-mcp)

An MCP **server**, not a SKILL.md-style skill — it gives Claude real browser
automation (navigate, click, fill forms, take accessibility snapshots) via
Playwright, using the accessibility tree instead of screenshots, so it's fast
and doesn't need a vision model.

Nothing is vendored into this repo for it since MCP servers are run, not
copied in as files. Register it instead:

## How to use it

**Claude Code CLI:**
```bash
claude mcp add playwright npx '@playwright/mcp@latest'
```

**Manual MCP config** (`.mcp.json` or your client's MCP settings):
```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

**Docker:**
```bash
docker run -i --rm mcr.microsoft.com/playwright/mcp
```

Once connected, Claude gets tools like `browser_navigate`, `browser_click`,
`browser_snapshot`, `browser_type`, etc. Use it for: testing your own web
app end-to-end, scraping/inspecting a page's structure, or driving a UI
flow that needs real DOM interaction rather than an HTTP request.
