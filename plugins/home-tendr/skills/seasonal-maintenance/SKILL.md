---
name: seasonal-maintenance
description: Builds an autumn or spring maintenance plan for the user's HomeTendr home from HomeTendr's own seasonal checklists, tailored to the home (house or apartment, build year, areas, items), and adds the chosen jobs as yearly recurring tasks. Use when the user asks for help with autumn or spring maintenance, getting the house ready for winter, a seasonal checklist, or "what should I do this autumn/spring".
---

# Seasonal maintenance

Turn HomeTendr's seasonal checklist into recurring tasks that fit this home, in the steps below.

**Tools.** Everything below uses the HomeTendr plugin's MCP tools `get_home`, `list_areas`, `list_items`, `list_tasks` and `create_task` (their full names end in `__<tool>`, for example `__get_today`). Not all of them may be loaded at the start: if one is missing from your tools, load it with `tool_search` (for example "HomeTendr get_home list_areas list_items list_tasks create_task") before going on. Never ask the user for facts these tools can give you.

Follow these steps without quoting them or naming this skill or its files to the user; just do it and talk about their home.

## 1. Pick the season

- Use the season the user names. Otherwise go by today's date in the home's hemisphere: August–November → autumn, February–May → spring. In between, ask.
- Read the matching checklist: [references/autumn.md](references/autumn.md) or [references/spring.md](references/spring.md). Use only these jobs, rephrased if needed; do not invent other checklist items.

## 2. Look at the home

Call these HomeTendr tools (default home unless the user names another; ask only if several homes make it ambiguous):

- `get_home` — type (house, apartment …) and build year.
- `list_areas` — rooms and spaces, to link tasks (e.g. "Garden", "Roof", "Utility room").
- `list_items` — things the checklist touches: heat pump, boiler, ventilation unit, fireplace or stove, lawn mower, dishwasher, smoke alarms.
- `list_tasks` with no date filter — existing tasks, to avoid duplicates.

## 3. Tailor the list

- Apartment: drop jobs for the roof, gutters, facade, outdoor taps and garden unless the home has those areas or items.
- Keep a job only if it fits the home. Make it concrete with the home's own names: "Service the heat pump" when there is a heat pump item; "Book the chimney sweep" only with a fireplace or stove.
- Skip jobs that already exist as tasks (same job, even if worded differently) and say so briefly ("Clean gutters is already scheduled for 19 Oct").
- An older home (built before about 1980) can get a short note on the jobs that matter more there (damp, windows, roof), without adding checklist items.

## 4. Proposal

Show one short numbered list grouped like the checklist (outside, heating and safety, inside …). For each job: the task title as it would be created, the suggested month, and the area or item it would be linked to. Then ask which ones to add — "all", numbers, or changes — and wait for the answer.

## 5. Creating tasks

For each chosen job call `create_task` with:

- `title` — short and in the user's language (e.g. "Rensa hängrännor"), without the season in the title.
- `due_date` — the next suitable date this season (autumn jobs before the first frost, roughly September–November; spring jobs roughly March–May), never in the past.
- `repeat_every: 1`, `repeat_unit: "year"` — every job here comes back every year.
- `area_ids` / `item_id` — when a matching area or item exists.

If a call fails because the home doesn't allow changes or the plan doesn't include writing, stop, tell the user what the error says, and list the remaining jobs so they can add them in the app.

## 6. Wrap up

Say how many tasks were added and when the first ones are due, in one or two sentences. Don't repeat the whole list.
