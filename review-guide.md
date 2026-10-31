# MyReach client review guide

Use these examples in any client that supports remote MCP over Streamable HTTP.
The endpoint is `https://myreach.top/mcp`. Resource and prompt interfaces vary
by client; the plain-language requests below work without a prompt picker.
See [client setup](https://github.com/myreach-top/myreach-mcp/blob/main/installation/clients.md)
and [recorded compatibility](https://github.com/myreach-top/myreach-mcp/blob/main/installation/compatibility.md).

## Public page examples

| Audience | View-only example | Starter prompt |
|---|---|---|
| Creator | [Whitney Sweeney](https://myreach.top/youruser), fictional creator with AI-made artwork | `create_creator_page` |
| Business | [Feel.](https://myreach.top/yourbusiness), fictional brand | `create_business_page` |
| Agent builder | [SuperClaw](https://myreach.top/youragent), fictional agent project | `create_agent_page` |

These protected demonstration pages show the renderer and layout. They are
not editable review accounts. Build a fresh draft using an email you control,
or select your own page through OAuth. An agent profile describes an agent;
MyReach does not run it or confer AgentID verification.

## Requests to try

Replace the bracketed details with your own public content. Give the assistant
your intended owner email when asked; enter verification codes only in MyReach.

**Creator:** “Prepare a private MyReach creator page for [name], with [short
bio], my portfolio [URL] and newsletter [URL]. Ask for missing details. Show
the preview, then let me claim and publish the reviewed page.”

**Business:** “Prepare a private MyReach profile for [business], with [short
description], website [URL] and contact link [URL]. Review any website
suggestions with me. Show the preview before I claim it.”

**Agent builder:** “Prepare a private profile describing [agent name] and
[truthful capabilities]. Include documentation [URL] and demo [URL]. Do not
invent a verification badge. Show the preview before I claim it.”

**Existing page:** “Read my authorized page [slug]. Prepare a separate draft
with [changes], keeping my other cards, sections, translations and theme.
Show the preview and owner approval link. Confirm status after I approve.”

## Read docs and retrieve prompts

`resources/list` returns these public resources. Pass the exact URI to
`resources/read`; no account or page access is needed.

| Resource | URI |
|---|---|
| MCP guide | `https://myreach.top/ai-agents/mcp` |
| Agent API guide | `https://myreach.top/ai-agents-guide` |
| REST OpenAPI schema | `https://myreach.top/openapi.json` |

`prompts/list` returns four prompts. The three creation prompts accept optional
string arguments `name`, `description`, `links` and `ownerEmail`; omitted
details should be requested before creating a page. `update_page_safely`
requires string arguments `slug` and `changes`.

After normal MCP initialization, an example `prompts/get` request is:

```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "method": "prompts/get",
  "params": {
    "name": "create_creator_page",
    "arguments": {
      "name": "My creator example",
      "description": "Independent illustrator sharing work and updates.",
      "links": "Portfolio: https://example.com/portfolio; Newsletter: https://example.com/newsletter"
    }
  }
}
```

Use `create_business_page` or `create_agent_page` with the same argument names
for the other audiences. For an owned page:

```json
{
  "jsonrpc": "2.0",
  "id": 3,
  "method": "prompts/get",
  "params": {
    "name": "update_page_safely",
    "arguments": {
      "slug": "my-owned-example",
      "changes": "Shorten my bio and preserve all other content."
    }
  }
}
```

Example URLs and slugs above are placeholders, not review credentials.
Retrieving a prompt returns instructions only: it does not create, edit,
publish, authorize an account, or consume a page-creation quota.

## New owner: anonymous draft and verified claim

1. Read `get_myreach_capabilities`. Supply the intended owner's email, an
   available slug, supported content and a fresh random UUIDv4 `requestId` to
   `create_page_draft`. Retry with the same ID and identical input.
2. Keep its draft capability private. Read or edit only that draft, using
   the latest revision. Obtain `get_page_preview` and
   `request_publication_approval`. The public page must still return 404.
3. The owner opens the claim link and verifies the intended email by code or
   Google. Verification creates an account if needed or retains the existing
   account. If an older screen offers account choices, choose **Create account
   and claim**; no separate signup is needed. Free allows one page; active Pro
   allows three. A full account cannot claim another page; the draft stays private.
   No existing account, password or OAuth connection is required
   for anonymous creation. A host may separately require connection before
   exposing its tools.
4. The owner reviews the exact revision and chooses **Claim and publish**.
   Changed revisions require fresh review. Ask `get_publication_status`;
   report success only after it returns published.
5. Builder editing access ends after claim. The capability remains a
   status-only receipt. Unclaimed drafts expire 24 hours after creation;
   edits do not extend that deadline.

## Existing owner: OAuth and approved changes

Use the client's OAuth flow with S256 PKCE and the exact resource audience
`https://myreach.top/mcp`. Discovery is at:

- [Protected-resource metadata](https://myreach.top/.well-known/oauth-protected-resource/mcp)
- [Authorization-server metadata](https://myreach.top/.well-known/oauth-authorization-server)

MyReach supports CIMD and public-client dynamic registration. No client secret
or owner REST key is required. Request `pages:read` for reads; drafting and
approval requests also need `drafts:write` and `publication:request`.

1. Sign in and explicitly select only the pages needed. Verify
   `get_connected_account` and `list_pages` before reading an owned page.
2. Read the current page revision and create a separate draft. Preserve
   unrelated content. Existing public content must remain unchanged.
3. Get a private preview and owner approval link. The owner reviews and
   chooses **Approve and publish** in MyReach. An intervening admin edit,
   ownership change or draft edit invalidates stale approval.
4. Confirm the committed revision with `get_publication_status`. Retrying
   a completed approval must not publish another revision.

The same examples and protocol apply across clients. Each client still needs
its own authorization and page selection. Claiming a page does not grant
ongoing access, and one client's token is not a credential for another client.
Never put reviewer passwords, OAuth tokens, or private preview/claim/approval
links in a public issue, catalog PR or documentation repository.

## Review checks and evidence

Check public 404 before claim, private preview, exact-revision approval,
successful status after commit, builder revocation, insufficient scopes,
cross-account denial and stale-approval rejection. Expiry and concurrency
checks belong in an isolated test environment; do not alter customer pages.

Recorded 31 October 2026: the live endpoint exposes **10 tools, 3 resources
and 4 prompts**. The TypeScript SDK reads every resource and prompt. Muse's
portal completed its own CIMD OAuth, selected-page consent and token exchange,
and reports the same catalog. A controlled inbox test completed email-code
claim and builder revocation. These are reusable test cases, not proof that
every client completed its own OAuth or publishing conversation.

Hermes-specific results and the login-probe limitation are recorded in the
[compatibility tracker](https://github.com/myreach-top/myreach-mcp/blob/main/installation/compatibility.md).
Public examples and this guide need no private reviewer login. If a marketplace
needs hosted reviewer access, arrange isolated credentials privately for that
recipient; never reuse customer accounts or publish the credentials.

Registry metadata revision [1.0.1](https://registry.modelcontextprotocol.io/?q=top.myreach%2Fmyreach)
includes these documentation, prompt, OAuth and fictional example links.
Publisher extensions may not appear in every directory UI; the actual catalog
is discovered from `/mcp`. Credentials and private review links are excluded.
