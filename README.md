# Exa for Antigravity and Gemini CLI

Install the Exa plugin to give Google Antigravity and Gemini CLI access to the live web through Exa, web search built for agents. Search for up-to-date information and read the sources that matter without leaving your coding session.

No API key is required to get started.

## Install

**Antigravity Marketplace**

In the Antigravity app, open **Customizations** in the left sidebar, then **Marketplace**, find **Exa** and select **+**. Installed plugins are listed under **Customizations → Installed** and sync to the Antigravity CLI.

**Antigravity CLI**

```bash
agy plugin install https://github.com/exa-labs/exa-antigravity-plugin
```

**Gemini CLI**

```bash
gemini extensions install https://github.com/exa-labs/exa-antigravity-plugin
```

Start a new session and ask for something that needs the web. The plugin identifier is `exa-web`; its MCP server is named `exa`.

## Build with what's on the web right now

The libraries, APIs and tools you build with change every day. With Exa installed, your agent can search for the latest documentation, issues, changelogs and real-world examples while it works.

From inside your repo:

```text
Find the current upgrade guide for a dependency in this project and
summarize the changes before proposing a migration.
```

The same works whenever the answer might be somewhere outside your repo:

- "Search the `tokio-tungstenite` issues and changelog for this error before you try to fix it."
- "Find real examples of Postgres advisory locks in Rust and recommend the pattern that fits this worker pool."
- "Read the current Stripe webhook docs and check our implementation against them."

## What the plugin includes

| Component | What it does |
| --- | --- |
| `web_search_exa` | Searches the web in natural language and returns the content of the best pages, not a list of links. |
| `web_fetch_exa` | Reads clean content from one or more known URLs, such as docs, a changelog, an issue or a blog post. |
| `exa-web-search` skill | Guides the agent on writing queries and citing sources. Invoke it with `/exa-web-search`. |
| `exa-fetch` skill | Guides the agent on reading pages. Invoke it with `/exa-fetch`. |
| Rule | Reminds the agent to use Exa when a task depends on information outside the repository. |

## Rate limits and your Exa account

Exa offers free usage without an API key. To use your own plan and limits, connect your Exa account.

### Antigravity

Open **Customizations → Installed → Exa → Accounts** and select **Sign in**. Complete the browser sign-in and paste the authorization code back into Antigravity if prompted. The bundled server then uses your account; no second server is needed.

Antigravity may require this sign-in before enabling the tools, even though the Exa endpoint supports keyless requests.

### Gemini CLI

Add your [Exa API key](https://dashboard.exa.ai/api-keys) to `~/.gemini/settings.json`, merging this entry with your existing settings:

```json
{
  "mcpServers": {
    "exa": {
      "httpUrl": "https://mcp.exa.ai/mcp",
      "headers": {
        "x-api-key": "YOUR_EXA_API_KEY"
      }
    }
  }
}
```

Keep the server name `exa`: this overrides the extension's bundled connection without disabling its skills or rule. Start a new session after changing the configuration. Keep your key out of chat and version control.

## Data and security

The bundled MCP configuration connects to `https://mcp.exa.ai` over HTTPS. Search queries and requested URLs are sent to Exa, along with an `x-exa-source` header that identifies the plugin's traffic. The default configuration sends no credentials. If you configure your own account, the client also sends your API key or OAuth token to authenticate requests. The plugin includes no local executables or shell commands; its skills and rule are instructions read by the client. See the [privacy policy](https://exa.ai/privacy-policy).

To uninstall from Antigravity:

```bash
agy plugin uninstall exa-web
```

To uninstall from Gemini CLI:

```bash
gemini extensions uninstall exa-web
```

If you configured a personal server, remove that entry separately to disconnect it.

## Resources

- [Exa MCP documentation](https://exa.ai/docs/get-started/exa-mcp)
- [Exa Search API](https://exa.ai/docs/search/quickstart)
- [Exa MCP server source](https://github.com/exa-labs/exa-mcp-server)
- Support: [hello@exa.ai](mailto:hello@exa.ai)

## License

MIT
