# Todo4 — Claude Code Plugin

Task management for Claude Code. Create, update, and query tasks across sessions via 16 MCP tools backed by [todo4.io](https://todo4.io), plus a `/todo4:status` convenience command.

## What you get

- **16 MCP tools** — `list_tasks`, `create_task`, `update_task`, `close_task`, `add_subtask`, `add_comment`, `notify_human`, and more. Claude can call these automatically based on your requests.
- **`/todo4:status`** — a single command that shows overdue tasks, tasks due today, and your top open items ranked by priority.
- **Cross-session persistence** — tasks live in your Todo4 account, not in local files. They follow you across projects, devices, and agents.

## Install

In Claude Code, register this repo as a plugin marketplace and install the plugin:

```
/plugin marketplace add panitw/todo4-claude-plugin
/plugin install todo4@todo4
```

### First-time setup: trigger authentication

After install, the plugin is registered but **not yet authenticated**. Some clients (notably Claude Cowork on claude.ai) don't probe the MCP server until a tool is actually called — so you need to prime it with one prompt:

> *"List my todo4 tasks"* — or any question that needs Todo4.

On that first tool call, the client hits the server, gets a 401, and launches OAuth against [todo4.io](https://todo4.io) in a new browser tab. Approve the request once and you're done — tokens are refreshed automatically after that. No tokens to paste.

If you don't have a Todo4 account yet, OAuth will create one for you on first sign-in.

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
