---
name: exa-fetch
description: "Read clean content from one or more known URLs with Exa. Use when the user shares a link or when a search result's content is not enough."
---

# Fetch Web Pages (Exa)

Use the available tool whose name ends with `web_fetch_exa` (for example, `web_fetch_exa` or `mcp_exa_web_fetch_exa`). The client may add a server prefix; match the tool by its name and description. It returns the page content as clean markdown, including JavaScript-rendered pages and PDFs.

## When to use

- The user shares a URL or asks what a page says
- Reading documentation, a changelog, an issue or a blog post
- Following up on a search result whose content is not enough

Use the `exa-web-search` skill instead when you need to find pages first.

## Parameters

- `urls` (required). The URLs to read. Batch several URLs in one call.
- `maxCharacters`. Maximum characters returned per page. Defaults to 3000. Set it only when you need more or less than the default.

Example:

```json
{
  "urls": ["https://example.com/page1", "https://example.com/page2"]
}
```

## Answer format

1. Present the key information from the page.
2. If the user asked a question, answer it from the page content.
3. Include the source URL.

## Free rate limits

The plugin connects without credentials, so it uses Exa's free rate limits. If a call returns a rate-limit error (429) or a normal tool result saying the free limit has been reached, treat it as a rate limit, not source content. Tell the user that signing in to Exa or adding an Exa API key moves requests to their own plan and limits, as the plugin README explains. The server may suggest an `exaApiKey` URL parameter; the README uses an `x-api-key` header to avoid putting a key in the URL. Both authenticate requests. Never ask the user to paste a key into chat.

## If the tool is missing

Check for client-prefixed names before deciding the tool is missing. If no matching tool is in your tool list, do not answer from memory or fall back to another search tool. Tell the user the Exa plugin's MCP server is not connected and ask them to enable the plugin: in Antigravity, use Customizations > Installed; in Gemini CLI, run `gemini extensions enable exa-web`. Start a new session and check the MCP connection if it is still missing.
