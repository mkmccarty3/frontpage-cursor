# Frontpage for Cursor

Connect an existing Frontpage account to inspect website source, edit allowed
text files, check previews, and use People and email with separate consent.
Publish websites through Frontpage. This package installs no local server,
hooks, commands, API keys or background tasks.

## Connect

Install the Frontpage package from the Cursor Marketplace when its listing is
published. Until then, use Cursor's custom MCP setup with the contents of
`mcp.json` in this package. The fixed public client ID is not a secret; do not
add a client secret or an API key.

For direct setup, add the `frontpage` entry from `mcp.json` to your project's
`.cursor/mcp.json`, or to your user MCP settings. In Cursor, open Customize,
find the Frontpage MCP server, and connect. For Cursor CLI, run
`agent mcp enable frontpage`, then `agent mcp login frontpage` from that project.
Complete your normal Frontpage login and consent in the browser.

Choose all current/future eligible sites or selected sites, then read-only or
read/edit source access. People and email default to none and need separate
approval. Your current site role and Scale/Internal eligibility apply on every
request. Installing this package grants no account or site access.

The service uses Streamable HTTP at https://app.frontpage.host/api/mcp.
The native callback is http://localhost:8787/callback; Cursor's hosted callback
is https://www.cursor.com/agents/mcp/oauth/callback. Only those exact callbacks
are registered for this public PKCE client. The actual client acceptance record
determines which Cursor surfaces have been tested; do not infer hosted-agent
acceptance from the CLI test.

## Working safely

Read site context and source before editing. Keep the observed revision and
reuse the exact operation ID and payload on an uncertain retry. A saved source
revision is not a ready preview: check that exact revision before reporting it.
Production publication, source deletion, billing and team management remain
outside this connection.

For People/email, read the MCP operation guide first. Management permission
can send email or activate automation on your explicit instruction; existing
sender, consent, role and delivery checks still apply. Do not treat source
permission as CRM permission.

Disconnect in Frontpage Workspace → Developers → Connected Apps. Removing the
local configuration or signing out alone does not revoke an OAuth grant.

Setup and support: https://frontpage.host/developers/mcp.
People: https://frontpage.host/developers/people.
Email: https://frontpage.host/developers/mail.
Privacy: https://app.frontpage.host/connections/privacy.
Terms: https://frontpage.host/terms.
Support: support@frontpage.host.

The MIT license covers this package only. It does not license Frontpage's
hosted service, private backend or trademarks. The icon is Frontpage's current
purple mark, reused from the official brand asset without redrawing it.
