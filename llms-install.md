# Installing the Browser.lol MCP server

Browser.lol is a hosted, remote MCP server. There is nothing to install or run locally.

1. Add a remote MCP server with the transport Streamable HTTP and this URL:

   ```
   https://api.browser.lol/mcp
   ```

   For Cline, add it to `cline_mcp_settings.json`:

   ```json
   {
     "mcpServers": {
       "browserlol": {
         "type": "streamableHttp",
         "url": "https://api.browser.lol/mcp"
       }
     }
   }
   ```

2. Start the sign-in from the MCP server list. A Browser.lol page opens: sign in and allow access (OAuth). Clients without OAuth send an API key instead, in the `Authorization: Bearer <key>` or `x-api-key` header; keys are created on https://browser.lol/en/dash/agents under Advanced.

3. The account needs the Premium plan: https://browser.lol/en/upgrade

4. Test it with: "Open example.com in a Browser.lol session and tell me what the page says." The answer includes a live view link to watch the session and take over.

Docs: https://browser.lol/en/docs/mcp
