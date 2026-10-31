# MyReach for OpenClaw

Connect to the hosted MyReach MCP server to inspect a public website, prepare
private page drafts, edit supported profile/link/design/language content,
preview the result and request owner approval. MyReach hosts creator, business
and agent-profile pages; it does not execute agents.

This is a configuration-only compatible plugin bundle. It contains no local
commands, executable plugin code, API keys or application backend source.
The generated package includes MyReach's icon and MIT license.

## Connect

Use a current OpenClaw version with remote HTTP bundle MCP support. Install the
reviewed bundle through OpenClaw's plugin flow, enable it, then connect the
MyReach account when prompted. Select only the pages the assistant needs.
Follow the [OpenClaw MCP instructions](https://docs.openclaw.ai/tools/mcp)
and [compatible bundle reference](https://docs.openclaw.ai/plugins/bundles).

Endpoint: `https://myreach.top/mcp`.

Account actions use OAuth. New anonymous pages stay private and expire after
24 hours unless their intended owner verifies their email and chooses Claim
and publish. Existing-page edits stay in a separate draft until the owner
reviews and approves that revision. Ask for publication status after approval.
Keep preview and approval links private. Commerce, domain purchases, calendar
writes and scheduled publication are outside this connector's scope.

Try: “Prepare a private MyReach page with my name, bio and documentation link.
Ask for my owner email if needed. Show the preview and request my approval.”

## Distribution and testing

- [Official MCP Registry](https://registry.modelcontextprotocol.io/?q=top.myreach%2Fmyreach): listed, version 1.0.1.
- [Hermes catalog submission](https://github.com/NousResearch/hermes-agent/pull/147158): awaiting review.
- ClawHub availability: see the [current directory status](https://myreach.top/ai-agents/mcp#directories).
- Live SDK discovery/capabilities pass. OpenClaw OAuth and the complete
  publishing conversation have not been manually validated.

Guide: https://myreach.top/ai-agents/mcp
Support: hello@myreach.top
Privacy: https://myreach.top/privacy
Terms: https://myreach.top/terms
