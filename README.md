# Todo4 — Claude Code Plugin

Task management for Claude Code. Create, update, and query tasks across sessions via 16 MCP tools backed by [todo4.io](https://todo4.io), plus `/todo4:connect` and `/todo4:status` convenience commands.

## What you get

- **16 MCP tools** — `list_tasks`, `create_task`, `update_task`, `close_task`, `add_subtask`, `add_comment`, `notify_human`, and more. Claude can call these automatically based on your requests.
- **`/todo4:connect`** — prime the OAuth flow on first install and confirm the session is authenticated.
- **`/todo4:status`** — a single command that shows overdue tasks, tasks due today, and your top open items ranked by priority.
- **Cross-session persistence** — tasks live in your Todo4 account, not in local files. They follow you across projects, devices, and agents.

## Install

### Claude Code (CLI)

Register this repo as a plugin marketplace and install the plugin:

```
/plugin marketplace add panitw/todo4-claude-plugin
/plugin install todo4@todo4
```

### Claude Cowork (claude.ai)

Paste into a new chat:

> Install this Claude Code plugin: https://github.com/panitw/todo4-claude-plugin

Cowork will present a **Save plugin** card — click it to install. (Cowork narrates a brief "packaging" step while it wraps the repo for its install card. That's normal — ignore it.)

### First-time setup: authenticate the MCP connection

After install, the plugin is registered but **not yet authenticated**. How you authenticate depends on the client:

**Claude Code CLI** — the OAuth flow works automatically. Run `/mcp`, select `todo4`, and approve the sign-in. Or just call any Todo4 tool and the OAuth tab opens on the 401.

**Claude Cowork (claude.ai)** — Cowork does **not** currently launch OAuth for plugin-supplied MCP servers from chat. You need to authenticate through the Cowork UI:

1. Open **Settings → Personal plugins → Todo4 → Connectors**. If you see a **Connect** / **Authenticate** button next to the Todo4 MCP server, click it and complete sign-in there.
2. If no connect button appears, add Todo4 as a **Custom Connector** instead: **Settings → Connectors → Add custom connector**, URL `https://todo4.io/mcp`. Cowork's custom-connector flow handles OAuth end-to-end.

Once authenticated, run `/todo4:connect` in chat to confirm — it should reply with your tier. If you don't have a Todo4 account yet, OAuth will create one for you on first sign-in.

> **Note on `/todo4:connect`**: this command only *checks* the connection and shows setup instructions if you're not signed in. It does not itself trigger OAuth (the MCP client owns that flow).

## Usage

Once installed, Claude has access to Todo4 tools throughout the session. You can:

- Ask in chat: *"What's on my plate this week?"*, *"Add a task to review the Q2 report by Friday, p2"*, *"Close the deploy task and add a note about the rollback."*
- Run the `/todo4:status` slash command for a compact dashboard.

## The tools

| Tool | What it does |
|------|-------------|
| `get_platform_info` | Orientation — available tools, tier, timezone, connected agents |
| `list_tasks` | Paginated task list with status / priority / tag / date filters |
| `get_task` | Full task details including subtasks, comments, history |
| `create_task` | Create a single task with duplicate detection |
| `bulk_create_tasks` | Create up to 20 tasks in one call |
| `update_task` | Update any field; natural-language due dates |
| `close_task` | Close with optional completion note |
| `delete_task` | Soft-delete (recoverable) |
| `add_subtask` / `complete_subtask` / `list_subtasks` | Checklist items on a task |
| `list_tags` | All tags currently in use |
| `add_comment` | Post a comment attributed to the calling agent |
| `notify_human` | Proactive notification (rate-limited to 1/min) |
| `list_agents` | Connected AI agents and last activity |
| `list_attention_items` | Items requiring human attention |

## Requirements

- Claude Code with plugin support
- A free Todo4 account (created automatically via OAuth on first use)

## License

MIT — see [LICENSE](./LICENSE).

## Author

[Panit Wechasil](https://todo4.io) — feedback & issues welcome in this repo.
