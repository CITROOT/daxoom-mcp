# Daxoom — AI-Visibility Business Data (MCP + REST)

[![smithery badge](https://smithery.ai/badge/citroot/daxoom)](https://smithery.ai/servers/citroot/daxoom)

> What schema.org is to web crawlers, Daxoom is to AI agents.

**Daxoom** is a hosted, owner-verified business-data layer for AI agents. Every
response carries provenance (verification level, completeness score, freshness,
upstream sources). One profile feeds ChatGPT, Claude, Perplexity, Gemini, and
any MCP-compatible client.

This repository holds the **public developer artifacts** for the service — the
MCP manifest, OpenAPI spec, `llms.txt`, the tool catalog, and copy-paste client
configs. **It contains no server source: Daxoom is a proprietary, hosted
service** (see [License](#license)).

- 🌐 Website: https://daxoom.com
- 📚 Docs / OpenAPI: https://daxoom.com/docs · https://daxoom.com/docs/openapi.yaml
- 🤖 LLM entry point: https://daxoom.com/llms.txt
- 🔑 Free Developer key (3,000 queries/month): https://daxoom.com/developer

## Connect (MCP — remote Streamable HTTP)

Daxoom is a **remote-only** MCP server at `https://mcp.daxoom.com/`, authenticated
with an `X-API-Key` header (same key as the REST `/pubapi`). There is no local
install — the server runs on Daxoom's infrastructure.

```json
{
  "mcpServers": {
    "daxoom": {
      "url": "https://mcp.daxoom.com/",
      "transport": "http",
      "headers": { "X-API-Key": "dxm_YOUR_KEY_HERE" }
    }
  }
}
```

Per-client snippets (Claude Desktop, Cursor, Continue, Cline) are in
[`examples/`](examples/).

## Capabilities

- **12 tools** — search, full profiles, hours, offerings (menu/services/prices),
  attributes, owner Q&A, AI-grounding context, categories; a feedback loop
  (`report_incorrect_data`, `submit_review`); and schema explainability
  (`list_fields`, `describe_field`).
- **5 browsable resources** — `daxoom://categories`, `daxoom://schema/business`,
  `daxoom://schema/attributes`, `daxoom://schema/questions`, `daxoom://stats`.
- **Provenance envelope** — every payload is `{data, _meta}` with verification
  level (O/E/S/C), completeness, freshness, sources, and pagination.

Full catalog: [`TOOLS.md`](TOOLS.md) · Machine manifest: [`mcp-server.json`](mcp-server.json).

## REST API

```
GET https://api.daxoom.com/pubapi/v1/businesses?city=irvine&category=restaurant
Header: X-API-Key: dxm_YOUR_KEY_HERE
```

Formats: `application/json` (default), `application/ld+json` (schema.org JSON-LD),
`text/plain` (AI-friendly narrative). Spec: [`openapi.yaml`](openapi.yaml).

## Data model

- **Public business data** (open data + public records) is public.
- **Owner-entered data** stays the owner's — contributed to Daxoom for AI-agent use.
- **Daxoom-generated data** (enrichment, computed signals) is Daxoom's.

All access is governed by the Daxoom API Terms.

## License

The Daxoom platform and hosted service are **proprietary © CITROOT LLC** — the
server source is not licensed for self-hosting or redistribution. The contents
of *this repository* (docs, manifest, OpenAPI, and the example configuration
snippets) may be freely used and copied to connect to the hosted service. See
[`LICENSE`](LICENSE).
