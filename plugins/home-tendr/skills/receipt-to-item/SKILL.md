---
name: receipt-to-item
description: Registers an appliance or other item in the user's HomeTendr home from a receipt, invoice, order confirmation or type plate (photo, PDF or pasted text) — reads brand, model, serial number, purchase date, price, shop and warranty, shows them, and adds the item after the user confirms. Use when the user shares a receipt or type plate, or asks to add, register or save something they bought in HomeTendr.
---

# Receipt or type plate → item

Two cases:

- **From a document** (receipt, invoice, type plate, PDF): you read the values yourself, so show them and add the item once the user says yes.
- **The user typed the details and asked you to add it** ("I bought X at Y for Z on … — add it"): add it right away with what they gave, then offer what's missing (step 5).

**Tools.** This uses the HomeTendr plugin's MCP tools `list_items`, `list_areas`, `create_item` and `update_item` (their full names end in `__<tool>`, for example `__get_today`). If one is missing from your tools, load it with `tool_search` (for example "HomeTendr list_items list_areas create_item update_item") before going on. Never ask the user for facts these tools can give you.

Follow these steps without quoting them or naming this skill to the user; just do it and talk about their home.

## 1. Read the document

From the image, PDF or text, pick out what is there — never guess a value that isn't shown:

- **name** — what the thing is, in the user's language and the way they would say it ("Diskmaskin", "Heat pump"), not the full product line.
- **brand**, **model**, **serial_number** (type plates often show S/N, E-Nr, FD …).
- **purchased_at** — the receipt date, YYYY-MM-DD.
- **purchase_price** — the price of this item (not the receipt total if there are several lines), as a number; note the currency.
- **vendor** — the shop.
- **warranty_expires_at** — only if the document states a warranty or end date.

If the document holds several things (a receipt with a dishwasher and its installation), ask which to register, or register the main item and mention installation in `notes`.

## 2. Check the home

- `list_items` — is this already registered (same brand and model, or same kind of thing in the same place)? If so, offer to **update** that item with what's new instead of adding a second one.
- `list_areas` — suggest the area where the item belongs (a dishwasher → Kitchen) if one matches.

## 3. Summary and question (from a document)

Show a short summary of what you'll save: name, brand, model, serial number, purchase date, price and shop, warranty, area. Mark anything the document didn't show.

- **No warranty on the document:** suggest 2 years from the purchase date (5 years is common for durable goods in Norway) and let the user confirm or give the right date.
- End with a question such as "Shall I add it like this?" and wait for the answer before calling `create_item` or `update_item`. Apply any corrections.

## 4. Save

- New item: `create_item` with the confirmed fields (`name` required; leave out what you don't know).
- Existing item: `update_item` with only the fields that change.

If it's refused because of a permission or the plan, say so and give the summary so the user can add it in the app.

## 5. Wrap up

One or two sentences: what was saved. Then offer what's missing, with a concrete suggestion the user can accept with a yes:

- **No warranty date:** "No warranty was given — shall I set 2 years, to <purchase date + 2 years>?" (In Norway durable goods often have 5 years; mention it for a Norwegian home.)
- **No area:** suggest the one where it belongs, if a matching area exists.
- On yes, `update_item` with just those fields.

If the item came from a document, also say that the file itself isn't saved to HomeTendr from the chat — they can attach the receipt to the item in the HomeTendr app.
