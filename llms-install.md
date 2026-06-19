# Installing Daxoom in Cline (and other agents)

Daxoom is a **remote, hosted** MCP server (Streamable HTTP) — there is **nothing to
clone, build, or run locally**. "Installing" means adding the remote endpoint to the
client's MCP settings with an API key.

## Steps for the agent

1. **Get an API key.** Ask the user for their Daxoom Developer API key (free,
   3,000 queries/month). If they don't have one, point them to
   https://daxoom.com/developer to create one. Keys start with `dxm_`. Never commit
   or log the key.

2. **Add the server to the client config** (in Cline: MCP Servers → Configure,
   `cline_mcp_settings.json`):

   ```json
   {
     "mcpServers": {
       "daxoom": {
         "url": "https://mcp.daxoom.com/",
         "transport": "http",
         "headers": { "X-API-Key": "dxm_USER_KEY_HERE" },
         "disabled": false,
         "autoApprove": ["search_businesses", "get_business", "get_business_ai_context"]
       }
     }
   }
   ```

3. **Insert the user's key** in place of `dxm_USER_KEY_HERE`.

4. **Verify the connection** by calling `get_categories` (no arguments). A normal
   response confirms the server is connected and the key is valid. An HTTP 401 means
   the `X-API-Key` is missing or wrong.

## Notes

- No local install, environment variables, or build step — this is a hosted service.
- 12 tools + 5 resources. Discovery (the tool list) is keyless; tool **calls** require
  the `X-API-Key`.
- Full tool catalog: [`TOOLS.md`](TOOLS.md). Manifest: [`server.json`](server.json).
- Already published to the official MCP Registry (`com.daxoom/daxoom`) and listed on
  Smithery (`citroot/daxoom`).
