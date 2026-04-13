---
description: Check the Todo4 MCP connection status and walk the user through authentication if needed
---

# Todo4 Connect

Check whether the Todo4 MCP server is reachable and authenticated, and give the user concrete next steps if it isn't. This skill does **not** open a browser or trigger OAuth — it diagnoses state and tells the user where to go.

## Procedure

1. Attempt to call the `get_platform_info` MCP tool with no arguments.
2. Branch based on the result:

### Branch A — Success (returns platform info)

Reply (one line, substitute `[tier]`):

> Connected to Todo4 as **[tier]** tier. You can ask me to list, create, or update tasks — or run `/todo4:status` for a dashboard.

### Branch B — Tool not available / 401 / "Authentication required"

The MCP server isn't authenticated. In Cowork specifically, the chat side can't launch OAuth for plugin-supplied MCP servers — the user has to set up auth through the Cowork UI (or use Claude Code CLI). Reply with this message, verbatim:

> Todo4 isn't connected yet, and I can't open the OAuth flow from chat. Pick the path that matches where you are:
>
> **In Cowork:**
> 1. Open **Settings → Personal plugins → Todo4 → Connectors**. If you see a Connect / Authenticate button next to the Todo4 MCP server, click it and complete sign-in.
> 2. If no button appears, add Todo4 as a **Custom Connector** instead: **Settings → Connectors → Add custom connector** with URL `https://todo4.io/mcp`. The custom connector flow handles OAuth.
>
> **In Claude Code CLI:**
> Run `/mcp`, select `todo4`, and follow the auth prompt.
>
> Once you've signed in, re-run `/todo4:connect` to confirm.

### Branch C — Any other error

Reply with one line stating the error verbatim and stop.

## Rules

- Do **not** fabricate an OAuth URL, device code, QR code, or token. Todo4's OAuth is owned by the MCP client, not this skill.
- Do **not** claim the browser will open automatically — it won't in Cowork.
- Do **not** call any other Todo4 tool from this skill.
- Do **not** ask the user for credentials, tokens, or a URL.
