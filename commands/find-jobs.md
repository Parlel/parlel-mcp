---
description: Search open roles on Parlel by title, seniority, arrangement, and pay.
---

Search open roles using Parlel's `search_jobs` / `get_job` tools.

1. Ask (or infer): desired titles, seniority, `onsite`/`hybrid`/`remote`, pay floor.
2. Call `search_jobs`. `q` matches the **title only** — for description-level matching, list with structural filters first, then read each role via `get_job` and filter yourself.
3. Present matches with title, company, location/arrangement, pay where published, and role URL. Before calling anything "open", confirm `status` via `get_job` — closed roles resolve deliberately.
4. Offer to page with `next_cursor` or narrow with `comp_min` / `seniority`.
