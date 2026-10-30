# Compatibility evidence — 30 October 2026

Latest local run: `npm run check`, `npm run build:server`, `npm run test:mcp`,
`npm run package:mcp`, and
`MYREACH_TEST_DATABASE_URL=postgres://myreach:myreach-local-only@127.0.0.1:54330/myreach_test BASE=http://127.0.0.1:8799 npm run test:mcp:browser` passed on 30 October 2026. The browser run used a temporary Node server and the isolated `myreach_test` database. It did not contact production or a marketplace.

| Surface | Verified locally | Remaining |
|---|---|---|
| Official TypeScript SDK client 2.4.0 | Ten titled tools with annotations over HTTP; anonymous draft, browser preview/claim, OAuth PKCE consent, approved update, status | Hosted client review |
| Legacy MCP 2025-11-25 | Ten-tool discovery/calls, auth errors and outputs | Host-specific UI validation |
| Hermes 0.21.5+7355.ge36a818 | Isolated HERMES_HOME; HTTP connection and nine tools discovered (earlier candidate; ten-tool rerun pending) | Hermes OAuth and full publishing conversation |
| Codex CLI 0.153.4 | Configuration/package prepared | Interactive client connection and OAuth |
| Claude Code | Configuration prepared | Interactive client connection and OAuth |
| Cursor | Strict portable package prepared and schema-checked | Interactive client validation |
| ChatGPT / hosted Claude | Submission materials prepared | Approved reachable HTTPS endpoint and host review |

Previously run: `HERMES_HOME=/tmp/myreach-hermes-local hermes mcp test myreach_local`.
The test profile is separate from the user's Hermes configuration.

The browser probe verifies mobile-first as the default, lone row/card centering
across five desktop layouts, owner-selected wide desktop preservation, mobile
approval, two-process Postgres publication, restart persistence, and physical
expiry cleanup without resetting quotas.

No marketplace approval or publication claimed. Protocol success is not
substituted for hosted ChatGPT/Claude/Cursor/Codex conversation testing.
