# Compatibility evidence — 31 October 2026

## Deployed release

`https://myreach.top/mcp` is live on Talia and the stopped Lovebirds fallback.
Current application release: `88aee6af0ac48bf9271a940cfe9e2d435e54bf0c`.
[Exact-release GitHub quality gates](https://github.com/myreach-top/myreach-web/actions/runs/41186830974) pass.
Live SDK discovery confirms ten titled tools. The approved production smoke on
31 October verified private draft creation/editing, retry-safe creation, fixed
expiry, the real preview renderer, no-store/noindex/no-referrer, public-route
404s, and pending-claim status. The smoke page was never published. Read-only
MCP discovery was repeated after the latest application deployment.

Local browser/Postgres tests also cover verified owner claim, OAuth PKCE
consent, approval of existing-page changes, revision conflicts, two-process
publication/restart, and physical expiry cleanup. Those checks use loopback
and isolated `myreach_test`; they do not prove a hosted client completed OAuth
or publication.

| Surface | Evidence recorded | Still pending |
|---|---|---|
| Official TypeScript SDK client 2.4.0 | Local full workflow; live ten-tool discovery and private draft/preview/status smoke | Real host conversations and live owner approval |
| Legacy MCP 2025-11-25 | Local ten-tool discovery/calls, auth errors and outputs | Host-specific UI validation |
| Hermes 0.21.5+7355.ge36a818 | Isolated live HTTPS connection and ten-tool discovery on 31 October; actual catalog manifest parser passes | Browser OAuth and complete publishing conversation |
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

## Repository and release status

The application/backend repository remains private. The three reviewed MyReach
integration/API/docs repositories are public. Each export's SOURCE.json records
its exact source snapshot and dirty state; export updates and production
rollouts are separate. Neither packaging nor this document pushes repositories,
creates hosted reviewer data, hosts proofs, or submits listings.
