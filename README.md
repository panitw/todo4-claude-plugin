# Todo4 — Claude Code Plugin

Task management for Claude Code. Create, update, and query tasks across sessions via 16 MCP tools backed by [todo4.io](https://todo4.io), plus `/todo4:connect` and `/todo4:status` convenience commands.

## What you get

- **16 MCP tools** — `list_tasks`, `create_task`, `update_task`, `close_task`, `add_subtask`, `add_comment`, `notify_human`, and more. Claude can call these automatically based on your requests.
- **`/todo4:connect`** — prime the OAuth flow on first install and confirm the session is authenticated.
- **`/todo4:status`** — a single command that shows overdue tasks, tasks due today, and your top open items ranked by priority.
- **Cross-session persistence** — tasks live in your Todo4 account, not in local files. They follow you across projects, devices, and agents.

## Install

Pick the install path for your client:

### Claude (any client) — recommended

Todo4 works best as a **Custom Connector** — the same setup works in Claude Chat, Cowork, and Desktop:

1. In Claude, go to **Settings → Connectors → Add custom connector**.
2. Paste URL: `https://todo4.io/mcp`
3. Click **Connect** — a browser tab opens, you sign in with Todo4 (OAuth creates an account if you don't have one), approve the scopes, and land back in Claude authenticated.
4. Start using Todo4: ask Claude *"list my tasks"*, *"create a task to review Q2 report by Friday"*, etc.

> **Tier note:** Custom Connectors require Claude **Pro** or **Max**.
>
> **Cowork-specific caveat:** in Cowork only, Custom Connectors may need re-authentication after very long conversations due to a compaction bug ([#34832](https://github.com/anthropics/claude-code/issues/34832)) — just click Connect again if tools stop working.

For a guided setup with screenshots, see **[todo4.io/setup/cowork](https://todo4.io/setup/cowork)**.

### Claude Code (CLI)

Register this repo as a plugin marketplace and install the plugin:

```
/plugin marketplace add panitw/todo4-claude-plugin
/plugin install todo4@todo4
```

Then authenticate: run `/mcp`, select `todo4`, and approve the sign-in. Or just call any Todo4 tool — the OAuth tab opens automatically on the 401.

### Cowork plugin install (experimental, not recommended yet)

You can also install Todo4 as a plugin in Cowork (`Install this Claude Code plugin: https://github.com/panitw/todo4-claude-plugin`), but Cowork specifically has an OAuth bug ([anthropics/claude-code #28695](https://github.com/anthropics/claude-code/issues/28695)) that prevents plugin-supplied MCP servers from authenticating. Use the Custom Connector path above until Anthropic ships the fix.

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
