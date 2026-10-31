# Client installation and compatibility

Use `https://myreach.top/mcp` for direct remote connections. Use the loopback URL
only when running the local test server.

## Directory status

- [Official MCP Registry](https://registry.modelcontextprotocol.io/?q=top.myreach%2Fmyreach): listed as `top.myreach/myreach`, version `1.0.0`, verified 31 October 2026.
- [Hermes catalog submission](https://github.com/NousResearch/hermes-agent/pull/147158): awaiting review and merge. Use direct setup below meanwhile.
- Other directory reviews remain separate. Registry publication does not imply approval by a client marketplace.

Canonical [MCP guide and current availability](https://myreach.top/ai-agents/mcp#directories).

## Codex

In an isolated test configuration, add a remote server:

```toml
[mcp_servers.myreach]
url = "https://myreach.top/mcp"
```

Use `codex mcp login myreach` when account access is needed. Select pages on
MyReach's consent screen. Avoid changing an existing user's config for tests.
The connector package provides the same remote configuration; client directory submission is separate.

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
publication. See the [official Hermes instructions](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp/).
The catalog PR above contains the submitted curated entry; full Hermes browser
OAuth and publishing-conversation validation remain pending.

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

## OpenClaw

The `openclaw/` folder in the public connector repository is a configuration-only
compatible bundle for the hosted endpoint. ClawHub publication is pending;
do not use an invented catalog installation command. Follow the official
[MCP setup](https://docs.openclaw.ai/tools/mcp) and
[plugin bundle instructions](https://docs.openclaw.ai/plugins/bundles).
OpenClaw OAuth and full publishing-workflow validation are pending.

## OpenAI dots

Dots use OpenAI's connected-app/plugin controls. Track the MyReach plugin's
availability and OAuth flow on a Dot separately from ChatGPT/Codex tests;
no Dot-specific submission route is verified. See the official
[dots permissions guide](https://learn.chatgpt.com/docs/enterprise/dots-admin-guide)
and [plugin documentation](https://learn.chatgpt.com/docs/plugins).

## Grok and Grok Bot

Grok documents custom remote MCP connections at `grok.com/connectors`: choose
New Connector, then Custom, supply `https://myreach.top/mcp`, and complete
authentication. See [official Grok connector instructions](https://docs.x.ai/grok/connectors).
This is setup guidance; MyReach-specific in-app/OAuth validation is pending.
Grok Bot has a separate [marketplace submission](https://x.ai/bot/marketplace/submit-a-plugin),
which requires in-app testing. MyReach is not listed there.

## Muse

The [Muse Connector Platform](https://platform.muse.ai/docs) accepts connector
submissions with reviewer access, business verification, tool permissions and
data-handling documentation. MyReach is not submitted or validated in Muse.

## Test prompt

“Prepare a private MyReach page with my name, a short bio, and my documentation
link. Ask for any missing owner email. Show a preview and let me approve.”

Protocol tests and actual host tests are separate. Record versions, dates,
OAuth success, draft/claim success, and known limitations in compatibility.md.
