---
name: exa-web-search
description: "Search the web with Exa and get the content of the best pages back. Use for current documentation, changelogs, issues, code examples, news, fact-checking, or any question that needs live web data."
---

# Web Search (Exa)

Use the available tool whose name ends with `web_search_exa` (for example, `web_search_exa` or `mcp_exa_web_search_exa`). The client may add a server prefix; match the tool by its name and description. It returns ranked results with ready-to-use content from each page, not just a list of links.

## When to use

- Documentation, upgrade guides, changelogs and issues for the libraries and APIs in the project
- Real-world code examples
- Current events, news and recent developments
- Fact-checking a claim
- Any question whose answer may have changed since your training data

Use the `exa-fetch` skill instead when you already have the URL.

## Parameters

Follow the connected tool schema. Supply `query` and, when exposed, `objective`: a short explanation of what the search should establish for the user. The live server may mark `objective` as required even when it accepts calls without it.

## Writing the query

Describe the ideal page in natural language, not a list of keywords. "Blog post comparing React and Vue performance" finds more than "React vs Vue".

- Put recency in the query itself, with words such as "latest" or "recent". For relative dates such as "last week", work out the exact dates first and write them into the query.
- For a question with several parts, run one search per part and merge the results.
- Omit `numResults` unless the task needs a different number of results than the default of 10.
- Add `category:people` or `category:company` to the query only when the user wants people profiles or company pages.

## Reading the results

Each result carries content from the page. When that content is not enough to answer, read the best URLs with `web_fetch_exa`.

## Answer format

1. Lead with the direct answer.
2. Support it with specific facts, numbers and dates.
3. Cite the source URL for every fact.
4. Cite only URLs that appear in the results.

## Free rate limits

The plugin connects without credentials, so it uses Exa's free rate limits. If a call returns a rate-limit error (429) or a normal tool result saying the free limit has been reached, treat it as a rate limit, not source content. Tell the user that signing in to Exa or adding an Exa API key moves requests to their own plan and limits, as the plugin README explains. The server may suggest an `exaApiKey` URL parameter; the README uses an `x-api-key` header to avoid putting a key in the URL. Both authenticate requests. Never ask the user to paste a key into chat.

## If the tool is missing

Check for client-prefixed names before deciding the tool is missing. If no matching tool is in your tool list, do not answer from memory or fall back to another search tool. Tell the user the Exa plugin's MCP server is not connected and ask them to enable the plugin: in Antigravity, use Customizations > Installed; in Gemini CLI, run `gemini extensions enable exa-web`. Start a new session and check the MCP connection if it is still missing.
