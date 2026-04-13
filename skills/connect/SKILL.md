---
description: Connect this chat to the user's Todo4 account — triggers OAuth on first run, confirms the connection on subsequent runs
---

# Todo4 Connect

Prime the Todo4 MCP server so the user is authenticated and ready to use Todo4 tools. Run this silently — no preamble, no clarifying questions.

## Procedure

1. Call the `get_platform_info` MCP tool with no arguments.
2. Based on the result:
   - **Success (returns platform info)** — reply with one line: `Connected to Todo4 as [tier] tier. You can now ask me to list, create, or update tasks.`
   - **Authentication required / 401 / "Authentication required" error** — reply with one line: `Opening Todo4 sign-in in your browser — approve the request, then re-run /todo4:connect.` The MCP client will handle the browser redirect automatically on the failed call.
   - **Any other error** — reply with one line stating the error and stop.

## Rules

- Do not ask the user for credentials, tokens, or a URL — the MCP client owns the OAuth flow.
- Do not call any other Todo4 tool from this skill.
- Keep the entire response to one line.
