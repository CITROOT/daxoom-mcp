# Daxoom MCP — Tools & Resources

Server `daxoom` v1.1.0 · remote Streamable HTTP at `https://mcp.daxoom.com/` ·
`X-API-Key` auth. Every response is a `{data, _meta}` envelope (see below).

## Tools (12)

| Tool | Description |
|------|-------------|
| `search_businesses` | Paginated business search by name, category, city, or geo radius. |
| `get_business` | Full business profile with provenance metadata. |
| `get_business_hours` | Operating hours by day of week. |
| `get_business_offerings` | Menu items, services, products (with prices). |
| `get_business_attributes` | Amenities, accessibility, parking, policies. |
| `get_business_answers` | Pre-written Q&A authored by the business owner. |
| `get_business_ai_context` | Verified facts, canonical corrections, tone preferences, query hints — the LLM grounding payload. |
| `get_categories` | Business taxonomy with schema.org type mapping. |
| `report_incorrect_data` | Flag stale or wrong fields for human triage. No auto-changes. |
| `submit_review` | Submit a consumer star rating + optional text (5 trust guards: key age, prior queries, lifetime cap, monthly cap). |
| `list_fields` | Enumerate every field available on a business profile (core + attributes + Q&A). |
| `describe_field` | Explain a single field — meaning, type, allowed values, source of truth. |

## Resources (5)

| URI | Description |
|-----|-------------|
| `daxoom://categories` | Business taxonomy dump. |
| `daxoom://schema/business` | Full field catalog (core + attributes + questions, merged). |
| `daxoom://schema/attributes` | Queryable attribute catalog. |
| `daxoom://schema/questions` | Canonical Q&A prompts. |
| `daxoom://stats` | Platform-wide totals by verification level + top categories. |

## Response envelope

Every payload is `{data, _meta}`:

- `_meta.generated_at` — RFC3339 timestamp
- `_meta.source` — always `"daxoom"`
- `_meta.provenance` (single-business tools) — `verification_level` (O/E/S/C),
  `completeness_score` (0.00–1.00), `updated_at`, `verified_at`, `sources[]`
- `_meta.pagination` (list tools) — `limit`, `offset`, `total`, `has_more`,
  `next_offset`

`verification_level`: **O** owner-verified · **E** enriched · **S** seed ·
**C** claimed.
