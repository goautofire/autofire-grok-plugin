---
name: autofire-dealership
description: Read a car dealership's inventory, leads, test drives, follow-up priorities, and daily insights from AutoFire. Use when the user asks about their lot, vehicles, leads, test drives, or dealership performance on AutoFire.
---

AutoFire is the dealership's website and inventory platform. The `autofire` MCP server exposes read-only tools fixed to the one dealership the user chose when they signed in.

## Connecting

If no AutoFire tools are available, tell the user to connect AutoFire: it opens AutoFire in their browser, where they sign in with their AutoFire account, pick the dealership, and choose permissions. There is no API key to paste.

## Tools

- `get_dealership_profile`: name, location, hours, website.
- `search_inventory`: optional text query, `status` (`available` by default, or `pending`, `sold`), `limit` up to 50, `offset`. Returns year, make, model, trim, price, mileage, photos. No VINs.
- `get_vehicle`: full details for one vehicle by its AutoFire id.
- `list_leads`: lead workflow records (status, source, linked vehicle, timestamps) without names or contact details.
- `list_followup_priorities`: which leads are due for follow-up and why, by lead id.
- `get_lead`: one lead including name, email, phone, message, and notes. Only present when the user granted **Lead contact details**; never ask the user to work around a missing tool.
- `list_test_drives`: test-drive requests by status and date, without customer contact details.
- `get_dealership_insights`: the most recent daily insight reports.

## Working well

- Never pass or ask for a dealership id; the server derives it from the sign-in.
- Page through results with `offset` instead of asking for more than 50 at once.
- Treat the data as the dealership's confidential business records. Do not infer or fabricate customer contact details when they are not returned.
- Monthly tool-call allowances apply per dealership; if a tool reports the allowance is used up, say so and stop retrying.
