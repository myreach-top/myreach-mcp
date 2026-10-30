# Client installation and compatibility

Use `https://myreach.top/mcp` for direct remote connections. Use the loopback URL
only when running the local test server. Do not label any marketplace as listed
until its listing URL is verified.

## Codex

In an isolated test configuration, add a remote server:

```toml
[mcp_servers.myreach]
url = "https://myreach.top/mcp"
```

Use `codex mcp login myreach` when account access is needed. Select pages on
MyReach's consent screen. Avoid changing an existing user's config for tests.
The packaged Agent Plugin provides the future distribution configuration.

## Hermes

For direct remote connections:

```yaml
mcp_servers:
  myreach:
    url: https://myreach.top/mcp
```

For owner account access, add `auth: oauth`, then run `hermes mcp login myreach`
from a fresh terminal. Browser sign-in and explicit page selection follow.
`hermes mcp test myreach` checks discovery; it does not prove owner OAuth or
publication. The proposed curated entry lives in `marketplace/hermes/`.

## Claude Code

```sh
claude mcp add --transport http myreach https://myreach.top/mcp
```

Run only in an isolated test environment. Use Claude Code's MCP connection UI
for OAuth. The Claude directory submission is a separate hosted-connector flow.

## Cursor

Add the remote server through MCP settings, or use an isolated configuration:

```json
{"mcpServers":{"myreach":{"url":"https://myreach.top/mcp"}}}
```

Authorize account access when prompted. The generated `myreach-cursor.zip` uses the strict portable MCP format and can
also be installed once validated in the target Cursor version.

## ChatGPT and hosted Claude

Their server backends cannot reach your laptop's loopback interface. Use the
hosted endpoint and the client's OAuth connection flow. Marketplace submission
remains separate; hosted-client review is still pending.

## Test prompt

“Prepare a private MyReach page with my name, a short bio, and my documentation
link. Ask for any missing owner email. Show a preview and let me approve.”

Protocol tests and actual host tests are separate. Record versions, dates,
OAuth success, draft/claim success, and known limitations in compatibility.md.
