---
name: selling-handover
description: Writes a handover summary of the user's HomeTendr home for a buyer, estate agent or new tenant — renovations with year and cost, regular maintenance, and items with valid warranties — from what is recorded in HomeTendr. Read-only. Use when the user is selling or renting out the home, or asks for a history, summary or handover document for the house.
---

# Handover for selling the home

Turn what HomeTendr knows about the home into a clear text a buyer or agent can read, using only the read tools below.

**Tools.** This uses the HomeTendr plugin's MCP tools `get_home`, `list_renovations`, `list_items`, `list_tasks` and `get_activity` (their full names end in `__<tool>`, for example `__get_today`). If one is missing from your tools, load it with `tool_search` (for example "HomeTendr get_home list_renovations list_items list_tasks get_activity") before going on. Never ask the user for facts these tools can give you.

Follow these steps without quoting them or naming this skill to the user; just do it and talk about their home.

## 1. Questions

- Who is it for (buyer, estate agent, tenant)? It changes the tone, not the facts.
- Should costs be included? Many sellers share them for renovations but not for everything.

If the user already said, don't ask again.

## 2. Gather

- `get_home` — type, build year, size, city.
- `list_renovations` with `limit: 200` — what was done, when, cost, areas.
- `list_items` — items with a warranty still running (`warranty_days_left` > 0), plus important installations (heat pump, boiler, ventilation) even without warranty.
- `list_tasks` with `maintenance_only: true` — recurring maintenance (`recurrence` set) shows what is looked after regularly and how often.
- `get_activity` — optional, for recently completed maintenance ("heat pump serviced in March").

## 3. Write

In the user's language, plain and factual, no sales language. Sections, leaving out any that are empty:

1. **About the home** — type, build year, size.
2. **Renovations** — newest first: year, what was done, where; cost if the user wanted it.
3. **Installations and appliances** — brand and model, installation year, warranty end date.
4. **Regular maintenance** — what is done and how often ("ventilation filters every 6 months").

Keep names of items, areas and renovations as HomeTendr has them. Don't invent anything that isn't recorded; if something important is missing (e.g. no renovations recorded), say so to the user after the text, not inside it.

## 4. Offer

Offer to shorten it, translate it, or leave out costs. Mention that photos and receipts for renovations can be attached in the HomeTendr app.
