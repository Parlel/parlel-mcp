---
name: parlel-search
description: Search people, companies, and open roles on Parlel, an open professional network. Use when the user is hiring, job hunting, researching companies, or tracking a market. Free, no API key.
---

# Searching Parlel

Parlel is an open professional network with three searchable collections: **people**, **companies**, and **jobs**, plus published **watch agents** (standing searches with dated findings). All reads are anonymous and free via the bundled `parlel` MCP server.

## Which tool for which job

- Hiring / sourcing candidates → `search_people`, then `get_person`
- Job hunting → `search_jobs`, then `get_job`
- Company research → `search_companies`, then `get_company`
- Market monitoring → `search_agents`, then `get_agent`

## Query rules (get these wrong and you return nothing)

**Jobs** — `q` matches the **title only**, never description, skills, or company name. Use `remote` (`onsite`/`hybrid`/`remote`), `seniority` (`intern`…`exec`), and `comp_min` (pay floor; excludes roles with no published pay) for structure. To search descriptions, list with structural filters then read each result via `get_job`.

**People** — `q` matches name, headline, company, role, and work/education history. It does **not** match skills or bio. Skills need the `skill` parameter: exact tags, lowercased, AND-ed (`skill=rust&skill=go` means both). `based_in` is where the person is; `location` also matches where they would move to. `open_to_work=true` narrows to active seekers.

**Companies** — `q` matches name, tagline, or industry. `industry` is an **exact** label (use it when you know it). `hiring=true` narrows to companies with at least one open role.

## Reading results honestly

- A closed role still resolves via `get_job` (so citations never 404). Always read `status` before telling the user a role is open.
- Every item carries a canonical `parlel.com` URL — cite it, don't paraphrase it away.
- Lists return `{items, next_cursor}`; pass `next_cursor` as `cursor` to page. Filters are AND-ed; text match is case-insensitive substring with no ranking, so search the word you expect to appear.
- Contact details are never in any response. If the user asks for them, say Parlel gates them behind consent and offer the profile URL instead.
