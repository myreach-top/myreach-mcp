# Compatibility evidence — 31 October 2026

## Deployed release

`https://myreach.top/mcp` is live on Talia and the stopped Lovebirds fallback.
MCP implementation validation baseline: `3e3ae9fde675a24209153cbc960c31c69a44441b`.
Current app release is reported by `/api/health`; later docs-only rollouts can
have a newer SHA than this recorded implementation test.
[Exact-release GitHub quality gates](https://github.com/myreach-top/myreach-web/actions/runs/41205129748) pass.
Live SDK discovery confirms ten titled tools. The approved production smoke on
31 October verified private draft creation/editing, retry-safe creation, fixed
expiry, the real preview renderer, no-store/noindex/no-referrer, public-route
404s, and pending-claim status. The smoke page was never published. Read-only
MCP discovery was repeated after the latest application deployment.

A later explicitly authorized live test used a controlled AgentMail inbox:
anonymous creation and private preview, public 404, **Create account and claim**,
delivered email OTP, review of the exact revision, **Claim and publish**, public
200, builder reads/writes denied and status-only receipt still available.
The account was created through verified OTP on the Free plan. No password,
admin override, OTP bypass or automatic OAuth grant was used for this claim.
Muse then completed its own CIMD authorization and ten-tool listing against
only that fictional test page. The private portal shows 3/3 requirements
completed; review and an actual Muse conversation remain pending.

Local browser/Postgres tests also cover verified owner claim, OAuth PKCE
consent, approval of existing-page changes, revision conflicts, two-process
publication/restart, and physical expiry cleanup. Those checks use loopback
and isolated `myreach_test`; they do not prove a hosted client completed OAuth
or publication.

| Surface | Evidence recorded | Still pending |
|---|---|---|
| Official TypeScript SDK client 2.4.0 | Local full workflow; live discovery, private draft/preview/status and email-OTP claim with builder revocation | Real host conversations and live approval of an existing-page draft |
| Legacy MCP 2025-11-25 | Local ten-tool discovery/calls, auth errors and outputs | Host-specific UI validation |
| Hermes 0.21.5+7355.ge36a818 | Actual manifest parser passes; live discovery returns ten tools plus four Hermes utilities; all three resource reads and four prompt retrievals pass | Browser OAuth and complete publishing conversation; login probe stops after public discovery without obtaining a token |
| OpenClaw / ClawHub | Static compatible-bundle dry-run, security scan and public 1.0.1 listing verified; metadata warning fixed, zero inspector issues | Native OpenClaw OAuth and full publication workflow |
| Muse submission portal | Real CIMD authorization, owner login, explicit test-page consent, token exchange and 10-tool/3-resource/4-prompt discovery passed; all three submission requirements completed | Marketplace approval and an actual Muse publishing conversation |
| OpenAI dots | Plugin controls and shared OpenAI distribution route researched | Actual Dot installation and complete workflow |
| Codex CLI 0.153.4 | Configuration/package prepared | Interactive live connection, OAuth and complete workflow |
| Claude Code | Configuration prepared | Interactive live connection and OAuth |
| Cursor | Portable package schema-checked | Interactive live workflow |
| ChatGPT / hosted Claude | Live endpoint available; submission materials prepared | Conversation testing, OAuth, all review cases and reviewer access |

Previously run: `HERMES_HOME=/tmp/myreach-hermes-local hermes mcp test myreach_local`.
That profile is separate from the user's Hermes configuration. Client versions
above are versions actually recorded in the earlier checks, not claims about
currently installed or latest versions.

The local browser probe verifies mobile-first defaults, lone row/card centering
across five desktop layouts, explicit wide-desktop preservation and mobile
owner approval. The [Official MCP Registry listing](https://registry.modelcontextprotocol.io/?q=top.myreach%2Fmyreach)
is active at version 1.0.0. Public metadata readback and a fresh live SDK
connection, ten titled tools and capabilities call passed on 31 October 2026.
The [Hermes catalog submission](https://github.com/NousResearch/hermes-agent/pull/147158)
awaits Nous review and merge. These results do not claim client marketplace
approval or replace ChatGPT/Claude/Cursor/Codex/Hermes conversations.

## Live documentation and prompts

The live endpoint exposes three public resources and four starter prompts. Focused Node/Pages protocol tests cover actual document content,
bounded reads, no credential forwarding, unknown/private resource rejection,
validated prompt arguments and no page/account/grant mutations. The same candidate passed live SDK reads of every resource and prompt. Muse's
refreshed authenticated listing confirms 10 tools, 3 resources and 4 prompts.

## Hermes review refresh

The existing [catalog PR](https://github.com/NousResearch/hermes-agent/pull/147158)
includes the same view-only creator/business/agent examples and
[client-neutral review guide](https://github.com/myreach-top/myreach-mcp/blob/main/review-guide.md)
used for the other submission materials. The guide documents the actual
three-resource/four-prompt catalog, anonymous email-code claim, and a separate
selected-page OAuth maintenance flow. It includes no hosted reviewer passwords,
tokens, customer data or private capabilities.

At 15:17 UTC on 31 October, native Hermes discovery and its registered utility
handlers read all three live documentation resources and retrieved every starter
prompt, including the required arguments for `update_page_safely`. Hermes
registered 14 callable entries: ten MyReach server tools and four generated
resource/prompt utilities. No page was created or changed. An unauthenticated
`get_connected_account` call was denied, as required.

An isolated native `hermes mcp login` test on 31 October exposed a limitation:
MyReach's discovery is public, so the probe lists tools without starting the
authorization flow and reports that no OAuth token was obtained. The profile
has no authenticated account access. This is not evidence of missing DCR or
a requirement for a client secret. MyReach's public-client DCR/PKCE is covered
by separate protocol/browser checks; Muse's actual CIMD flow passed. A full
native Hermes OAuth and publishing conversation remains pending. Do not copy
Muse's token into Hermes or add an owner REST key as a workaround.

## Repository and release status

The application/backend repository remains private. The three reviewed MyReach
integration/API/docs repositories are public. Each export's SOURCE.json records
its exact source snapshot and dirty state; export updates and production
rollouts are separate. Neither packaging nor this document pushes repositories,
creates hosted reviewer data, hosts proofs, or submits listings.
