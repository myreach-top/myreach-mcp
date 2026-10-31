# MyReach

Create and manage your web presence with AI.

Prepare creator pages, business profiles, and agent profiles. Edit profile text,
links, social icons, supported appearance, and up to two secondary languages. Preview privately. The verified owner approves
publication in MyReach. MyReach hosts pages; it does not run agents.

The remote endpoint is `https://myreach.top/mcp`. For local installation use
the generated local package or replace the endpoint with
`http://127.0.0.1:8799/mcp`. Hosted clients need a reachable HTTPS endpoint;
their backends cannot connect to your loopback address.

## Workflow

1. Ask the assistant to prepare your page. Supply the intended owner's email
   only when you want to create a new page before signup.
2. The assistant calls `create_page_draft` with a fresh random UUIDv4 or 32–64 hex requestId.
   Keep that recovery nonce private and reuse it only for retries. Keep the
   returned draft capability private; it allows only temporary draft access.
3. Edit with the latest revision. Ask for `get_page_preview`.
4. Open the returned review link. Verify the intended owner and explicitly
   choose **Claim and publish**. Already published page updates use **Approve
   and publish**.
5. Ask for `get_publication_status` to confirm the committed result.

Temporary pages stay private (public 404) for 24 hours, then are deleted if
unclaimed. Editing does not renew that deadline. Claiming revokes temporary
editing access. Ongoing maintenance requires a separate OAuth connection and
explicit page consent. Revoking the connection ends that grant.

Supported: public website inspection with reviewable suggestions; profile name/bio and public avatar; up to two secondary languages with profile/link translations; complete link-only lists; targeted edits and hiding
of existing link cards, including on mixed-card pages; social icons; five
freestyle layouts, desktop presentation, fonts, preset/custom accents and
header/icon shapes. `get_myreach_capabilities` returns choices and limits.
Frozen themes and agent-page appearance stay locked. Other card types and
section arrangements are preserved during targeted link edits. No checkout, subscriptions, domain changes,
calendar writes, file uploads, scheduling, or agent execution tools.

For a targeted edit, read `get_page` and use its latest revision as
`expectedRevision` on `update_page_draft`. Example `content`:

```json
{
  "linkUpdates": [{"itemIndex": 0, "title": "Documentation", "href": "https://example.com/docs"}],
  "socials": [{"id": "github", "label": "GitHub", "href": "https://github.com/example", "iconStyle": "logo"}],
  "design": {"layout": "links", "desktopMode": "mobile-first", "primary": "#224466"}
}
```

`itemIndex` is the zero-based position in `page.items`, and must identify a
link card. `linkUpdates` preserves omitted fields and other cards. `links`
replaces the whole link-only card list; don't combine it with `linkUpdates`.
`socials` replaces all social icons; `[]` clears them. URLs must be HTTP(S)
without embedded credentials. A custom `primary` color selects the custom
accent; do not combine it with a preset accent. Existing `accent` and `font`
shorthands remain supported.

`inspect_website` takes a public website URL and returns `suggestedContent`,
`warnings`, and `untrustedSource: true`. It never saves or publishes a page.
Review suggestions before passing supported fields into a draft. Website text
cannot prove ownership or override approval. Ten inspections per hour apply.

For localization, enable `secondaryLanguages: ["fr"]`, then merge
`profileTranslations: {"fr": {"tagline": "Bonjour"}}` or per-link
`translations: {"fr": {"title": "Documentation"}}`. English stays primary.
Omitted fields are preserved; disabling a language retains its saved text.

The live endpoint exposes ten titled tools as of 31 October 2026.
See installation/compatibility.md in the connector repository for recorded
validation. Real hosted-client workflows and client marketplace review remain pending.

## Directory availability

- [Official MCP Registry](https://registry.modelcontextprotocol.io/?q=top.myreach%2Fmyreach): listed as `top.myreach/myreach`, version `1.0.0`.
- [Hermes catalog submission](https://github.com/NousResearch/hermes-agent/pull/147158): awaiting review and merge. Direct remote setup is available now; see installation/clients.md.
- [Live MCP guide](https://myreach.top/ai-agents/mcp#directories): connection instructions and availability.

A Registry listing does not imply approval by ChatGPT, Claude or another client.

Documentation: https://myreach.top/ai-agents/mcp
Support: https://myreach.top/help
Contact: hello@myreach.top
Privacy: https://myreach.top/privacy
Terms: https://myreach.top/terms

The license here covers integration files and documentation only. Brand assets
remain MyReach marks. It does not license the private MyReach application.
