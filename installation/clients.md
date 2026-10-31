# Client installation and compatibility

Use `https://myreach.top/mcp` for direct remote connections. Use the loopback URL
only when running the local test server.

## Directory status

- [Official MCP Registry](https://registry.modelcontextprotocol.io/?q=top.myreach%2Fmyreach): listed as `top.myreach/myreach`, version `1.0.0`, verified 31 October 2026.
- [Hermes catalog submission](https://github.com/NousResearch/hermes-agent/pull/147158): awaiting review and merge. Use direct setup below meanwhile.
- [OpenClaw / ClawHub](https://clawhub.ai/myreach-top/plugins/myreach): listed, configuration-only bundle version 1.0.1; metadata warning fixed.
- Muse: intake and all three follow-up requirements submitted; CIMD OAuth sign-in and ten-tool discovery passed. Review pending; no public listing.
- Other directory reviews remain separate. Registry publication does not imply approval by a client marketplace.

Canonical [MCP guide and current availability](https://myreach.top/ai-agents/mcp#directories).

## New owner versus existing page

Build a new page anonymously with the intended owner's email. Open the returned
claim link, choose **Create account and claim**, verify the email code (or
Google), review the exact revision, then **Claim and publish**. A password or
existing account is not required. Claiming does not grant ongoing assistant
access. OAuth and explicit page selection are for maintaining an owned page.
Some clients require account connection before exposing tools; their connection
screen is separate from MyReach's anonymous creation/claim journey.

## Public documentation and starter prompts

The live server lists three public resources: the MCP guide, Agent API guide,
and complete REST OpenAPI JSON. Read them through `resources/list` and
`resources/read`; no account is required. Four optional prompts are available
through `prompts/list` and `prompts/get`: `create_creator_page`,
`create_business_page`, `create_agent_page`, and `update_page_safely`.
Retrieving a prompt returns instructions; it makes no page changes and grants
no access. A client's UI must support MCP resources/prompts to expose them.
Live SDK retrieval of every resource and prompt passes. Muse's authenticated
submission snapshot also shows 10 tools, 3 resources and 4 prompts.

Use the [shared client review guide](https://github.com/myreach-top/myreach-mcp/blob/main/review-guide.md)
for view-only creator/business/agent pages, requests usable without a prompt
picker, exact resource URIs, prompt arguments, anonymous claim and OAuth
approval checks. Each client needs its own authorization; these examples do
not share Muse reviewer credentials or tokens with other clients.

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
The catalog PR above contains the submitted curated entry. MyReach's discovery
is public: the tested Hermes login probe lists tools without obtaining a token
and reports “no OAuth token was obtained”. That is not authenticated account
access. MyReach supports public-client DCR/PKCE and requires no client secret;
do not add a fake secret or an owner REST key to work around this result.
Full native Hermes OAuth and publishing-conversation validation remain pending.

For anonymous creation and public documentation/prompts, omit `auth: oauth`.
With the server key `myreach`, Hermes exposes the utilities
`mcp__myreach__list_resources`, `mcp__myreach__read_resource`,
`mcp__myreach__list_prompts` and `mcp__myreach__get_prompt` when discovery advertises
those capabilities. Ask it to read the MCP guide, or retrieve
`create_creator_page`, `create_business_page`, `create_agent_page` or
`update_page_safely` with the arguments in the shared guide. Leave resource and
prompt utilities enabled. Restart or use `/reload-mcp` after a server catalog
update; native utilities do not add server-side tools to MyReach's count of ten.

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
compatible bundle for the hosted endpoint. The [ClawHub listing](https://clawhub.ai/myreach-top/plugins/myreach)
is live. Its verified catalog command is:

```sh
openclaw plugins install clawhub:@myreach-top/myreach
```

Enable the plugin and authorize only the MyReach pages needed. Follow the official
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
data-handling documentation. MyReach’s initial intake is submitted; the three
follow-up requirements are now completed. The portal accepted Muse's CIMD,
completed real OAuth sign-in and lists ten tools, three documentation resources
and four starter prompts as of 31 October 2026.
Three isolated Free reviewer accounts were supplied privately. Review and an
actual Muse conversation remain pending; the portal snapshot is not a public listing.

Grok, Claude and OpenAI/ChatGPT/Codex/Dot testing and submissions are deferred
at the user's request. Their instructions above are prepared setup guidance.

## Test prompt

“Prepare a private MyReach page with my name, a short bio, and my documentation
link. Ask for any missing owner email. Show a preview and let me approve.”

Protocol tests and actual host tests are separate. Record versions, dates,
OAuth success, draft/claim success, and known limitations in compatibility.md.
