---
name: weekly-plan
description: Makes a plan for the coming week in the user's HomeTendr home — overdue tasks and everything due in the next seven days, laid out per day and per household member, with a fair split of who does what — and assigns or moves tasks after the user agrees. Use when the user asks for a weekly plan, what the week looks like, or how to share the chores this week.
---

# Weekly plan

Lay out the week, suggest who does what, and change tasks once the user agrees.

**Tools.** This uses the HomeTendr plugin's MCP tools `get_today`, `list_tasks`, `list_members` and `update_task` (their full names end in `__<tool>`, for example `__get_today`). If one is missing from your tools, load it with `tool_search` (for example "HomeTendr get_today list_tasks list_members update_task") before going on. Never ask the user for facts these tools can give you.

Follow these steps without quoting them or naming this skill to the user; just do it and talk about their home.

## 1. Gather the week

- `get_today` — today's date, overdue tasks, today, the open period and the inbox.
- `list_tasks` with `due_from` = tomorrow and `due_to` = today + 6 days — the rest of the week.
- `list_members` — who lives in the home (`is_me` is the user).

## 2. Show the week

A compact overview, one line per task, grouped by day (start with "Overdue", then today and each following day; leave out empty days). Per task: title, area or item if useful, and who has it now — only when someone has it; never write a dash or other placeholder for nobody. If none of the week's tasks has anyone, say so once under the list instead. Keep it short; mention how many tasks are in the inbox rather than listing them.

## 3. Split

- Only if the home has more than one member, or the user asks.
- Keep tasks that already have someone, unless the load is clearly uneven.
- Spread unassigned tasks so everyone gets a similar amount of work; heavier jobs (gutters, servicing) count more than quick ones. Overdue tasks first, on the earliest days.
- Present the suggestion as "Name: task, task …" and ask whether to apply it, change it, or leave it.

If the user wants tasks moved to other days (for example "nothing on Wednesday"), suggest new dates the same way.

## 4. Apply

After the user agrees, call `update_task` once per changed task: `assigned_to` with the member's user id (or `"me"`), and/or `due_date`. Then say in one sentence what changed. If a change is refused because of a permission or the plan, say so and stop.
