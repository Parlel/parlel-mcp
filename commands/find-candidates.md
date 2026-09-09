---
description: Source candidates on Parlel by skills, location, and availability.
---

Source candidates for a role using Parlel's `search_people` / `get_person` tools.

1. Ask (or infer from context): required skills, location, remote flexibility, seniority sought.
2. Call `search_people` with exact skill tags (`skill=rust&skill=go`), `based_in` for current location, `open_to_work=true` if the user wants active seekers. Remember `q` does not match skills — never put a skill only in `q`.
3. Present 5–10 candidates with headline, location, and profile URL (`https://parlel.com/u/{handle}`). Never invent contact details — they are never in the data.
4. Offer to fetch full profiles via `get_person` for the shortlist, or page further with `next_cursor`.
