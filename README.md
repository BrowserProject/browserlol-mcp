<p align="center">
  <img src="assets/browserlol-icon-400.png" width="96" height="96" alt="Browser.lol">
</p>

# Browser.lol MCP server

A real cloud browser for your AI agent. Connect Claude, ChatGPT, Cursor or any other MCP client to Browser.lol, and your agent opens pages, clicks, types and reads them in an isolated session on our servers. You watch live and take over whenever you want.

This repository holds no code. The server is hosted by Browser.lol: you add one address to your client and sign in.

## What your agent gets

- **A real browser in the cloud.** Each session runs in its own container. Nothing to install, no browser driver on your machine.
- **Input like a person.** Every click, keystroke and scroll is real mouse and keyboard input with human timing.
- **A live view link.** Your agent shares a link to the session. Open it to watch, take over at any time and hand control back. For a login or a captcha, your agent asks you to step in.
- **Apps and developer tools.** Your agent installs what a session needs: Anonymous Mail for sign-ups and verification codes, Files for uploads and downloads. Agent DevTools for web development and debugging are part of every session.
- **Sessions in other countries.** Start a session with an exit location in another country, a residential address or your own proxy, and with its own language and keyboard layout.
- **Saved profiles.** Continue a saved profile with its logins and settings, or keep a session as a new one.

Available browser images and exit locations depend on your account.

## Quick start

| | |
|---|---|
| Endpoint | `https://api.browser.lol/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth sign-in in your browser, or an API key in a header |
| OAuth discovery | `https://api.browser.lol/.well-known/oauth-protected-resource/mcp` |
| Plan | Premium ([plans](https://browser.lol/en/upgrade)) |

1. Add `https://api.browser.lol/mcp` to your client (see below).
2. Sign in on the Browser.lol page that opens and allow access.
3. Give your agent a task, for example: *Open example.com in a Browser.lol session and tell me what the page says.*

Clients without sign-in and your own code use an API key instead: `Authorization: Bearer YOUR_ACCESS_KEY` or `x-api-key: YOUR_ACCESS_KEY`. Create one on the [AI agents page](https://browser.lol/en/dash/agents) under Advanced. Keys in the URL are not accepted.

## Setup per client

Guides for more clients (Gemini CLI, GitHub Copilot CLI, Zed, Kiro, LM Studio, n8n and others) are in the [MCP docs](https://browser.lol/en/docs/mcp).

<details>
<summary><b>Claude</b> (web and desktop)</summary>

Open Customize › Connectors › + Add › Add custom connector. Enter the name `browserlol` and this URL, then click Continue and sign in on the Browser.lol page that opens.

```
https://api.browser.lol/mcp
```

On Team and Enterprise plans, an owner first adds the connector under Organization settings › Connectors.
</details>

<details>
<summary><b>Claude Code</b></summary>

```sh
claude mcp add --scope user --transport http browserlol https://api.browser.lol/mcp
```

Then type `/mcp` in Claude Code, choose browserlol and sign in.
</details>

<details>
<summary><b>ChatGPT</b></summary>

Turn on Developer mode under Settings › Security and login. Then add an app with + under Plugins: name it `browserlol`, paste this URL and choose OAuth.

```
https://api.browser.lol/mcp
```
</details>

<details>
<summary><b>Codex</b></summary>

```sh
codex mcp add browserlol --url https://api.browser.lol/mcp
codex mcp login browserlol
```
</details>

<details>
<summary><b>Cursor</b></summary>

Add this to `~/.cursor/mcp.json`, then click Connect next to browserlol under Settings › Tools & MCP.

```json
{
  "mcpServers": {
    "browserlol": {
      "url": "https://api.browser.lol/mcp"
    }
  }
}
```
</details>

<details>
<summary><b>VS Code</b> (GitHub Copilot)</summary>

Run MCP: Open User Configuration in the Command Palette and add this. VS Code asks you to trust the server and then to sign in.

```json
{
  "servers": {
    "browserlol": {
      "type": "http",
      "url": "https://api.browser.lol/mcp"
    }
  }
}
```
</details>

<details>
<summary><b>Devin Desktop</b> (formerly Windsurf)</summary>

```sh
devin mcp add --scope user browserlol https://api.browser.lol/mcp
devin mcp login browserlol
```
</details>

<details>
<summary><b>Cline</b></summary>

In the Cline panel, open MCP Servers › Configure › Configure MCP Servers and add this. Then start the OAuth sign-in for browserlol from the server list.

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
</details>

<details>
<summary><b>JetBrains AI Assistant</b> (API key)</summary>

Open Settings › Tools › AI Assistant › Model Context Protocol (MCP) › Add and paste this.

```json
{
  "mcpServers": {
    "browserlol": {
      "url": "https://api.browser.lol/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_ACCESS_KEY"
      }
    }
  }
}
```
</details>

<details>
<summary><b>Other clients and your own code</b> (API key)</summary>

```json
{
  "mcpServers": {
    "browserlol": {
      "type": "http",
      "url": "https://api.browser.lol/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_ACCESS_KEY"
      }
    }
  }
}
```
</details>

## Tools

27 tools. The developer tools are part of every session; the assistant uses them only when you ask.

| Tool | What it does |
|---|---|
| `browser_navigate` | Open a site through the address bar, search, go back or forward, or reload. Starts a session when none runs. |
| `browser_tabs` | List, open, switch to or close tabs. |
| `browser_snapshot` | Read the page as a tree of elements with references, dialogs first. |
| `browser_find` | Find elements by their text without reading the whole page. |
| `browser_screenshot` | See the whole screen as the live view shows it, toolbar included. |
| `browser_wait_for` | Wait until text appears or is gone, the URL matches, or a time has passed. |
| `browser_click` | Click an element or a screen point. The pointer moves there like a hand. |
| `browser_type` | Type into a field like a person. |
| `browser_fill_form` | Fill several fields one after another. |
| `browser_select_option` | Choose an option in a dropdown. |
| `browser_press_key` | Press a key or shortcut, or answer a JavaScript dialog. |
| `browser_scroll` | Turn the mouse wheel over the page or until an element is in view. |
| `browser_hover` | Move the pointer over an element to open menus and tooltips. |
| `browser_drag` | Drag and drop: lists, sliders, canvas. |
| `browser_file_upload` | Attach files through a file input. |
| `browser_downloads` | List the session's downloads with a link to fetch each file. |
| `browser_ask_user` | Hand the browser to the person watching for a login or a captcha. |
| `browser_session_create` | Start a session with a browser image, exit location, screen size, language or keyboard layout. |
| `browser_session_list` | List your sessions with quota and recent usage, also those you started yourself. |
| `browser_session_update` | Rename a session or change its exit location. |
| `browser_apps` | List, install and uninstall a session's apps. |
| `browser_session_close` | Close a session when the work is done. |
| `browser_account` | Read your plan features, browser images, saved profiles, quota and usage. |
| `browser_mail` | Your temporary mail inbox for sign-ups: address, incoming mail, links and codes. |
| `browser_inspect` | Read what DevTools shows: DOM, styles, network, cookies, storage, console. For web development and debugging. |
| `browser_evaluate` | Run JavaScript in the page like the DevTools console. For web development and debugging. |
| `browser_cdp` | Send Chrome DevTools Protocol commands and read their events. For web development and debugging. |

## Plans

The MCP server is included with Browser.lol Premium. See [the plans](https://browser.lol/en/upgrade) for pricing.

## How sessions work

- A page tool starts a session when none is running. With several sessions, your agent names the one to use.
- Your agent can use the sessions you start yourself, and you can watch and manage the ones it starts.
- Sessions end after their plan's idle or maximum runtime. Your agent closes its session when the work is done.
- While you are in control, your agent pauses. It continues once you hand control back.

## Security and privacy

- A connected agent or API key acts on your account like a password. Disconnect an agent or revoke a key on the [AI agents page](https://browser.lol/en/dash/agents) as soon as you no longer use it.
- Give each client or machine its own API key, so you can revoke access separately.
- Pages load in isolated browser containers on our servers. Your agent's model stays with its client.

[Privacy policy](https://browser.lol/en/legal/privacy) · [Terms](https://browser.lol/en/legal/terms) · [Acceptable use](https://browser.lol/en/legal/aup) · [Subprocessors](https://browser.lol/en/legal/subprocessors) · [Imprint](https://browser.lol/en/legal/imprint)

## Support

Docs: [browser.lol/en/docs/mcp](https://browser.lol/en/docs/mcp). Questions and problems: [support@browser.lol](mailto:support@browser.lol).

## License

The documentation in this repository is licensed under the [MIT License](LICENSE). The Browser.lol service is subject to its [terms](https://browser.lol/en/legal/terms).
