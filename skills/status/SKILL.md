---
description: Show the user's current Todo4 task status — overdue, due today, and top open tasks by priority
---

# Todo4 Status

Give the user a compact dashboard of their current task state. Do not improvise or ask clarifying questions — just run the procedure.

## Procedure

1. Call the `list_tasks` MCP tool with `status: "open,in_progress"` and `limit: 50`.
2. From the returned tasks, bucket them into three groups:
   - **Overdue** — `due_date` before today's date
   - **Due today** — `due_date` equals today's date
   - **Other open** — everything else, sorted by priority (p1 → p4), then by `due_date` ascending
3. Render the dashboard exactly in this order, only showing buckets that have tasks:

   - `### Overdue` — list all, p1 first. Each line: `**[priority]** title — was due [date]`
   - `### Due today` — list all, p1 first. Each line: `**[priority]** title`
   - `### Top open` — first 5 of "Other open". Each line: `**[priority]** title` and `— due [date]` if set
4. End with a single-line suggestion of what to tackle first, based on overdue → due today → highest-priority open.
5. If the user has zero open or in-progress tasks, say `No open tasks. You're clear.` and stop.

## Rules

- Keep the entire response under 20 lines.
- Do not print task IDs, tags, or descriptions.
- Do not ask follow-up questions — this is a status readout, not a conversation.
- If `list_tasks` fails, report the error in one line and stop.
