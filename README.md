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


## Business permissions

This release adds separate optional business read/manage permissions for
analytics, usage, forms/inbox, Store, Support and task/routine records. Source
and People/email permissions stay separate. Existing grants gain nothing;
reconnect and explicitly select the business access you want. Both choices
start off. Your current role and each site's eligible plan still apply.

Management can change the running catalog/form settings and send Support
replies, guidance or retries on your instruction. Payments stays read-only.
Website task start/retry, routine create/edit/run/resume, financial/account/
credential changes and unfinished Booking are excluded. Cancel and pause do
not start work. Public setup and limits: https://frontpage.host/developers/mcp.

Client packages contain only settings and guidance. They use the same hosted
MCP/OAuth services; no CLI, customer editor or internal agent changes are needed.

## Analytics reports

With business:read consent, use `frontpage_analytics_dashboard` for the existing
site-wide UI report and `frontpage_analytics_page_detail` with an exact `path`
for one page. The page report includes views, visitors, sessions, time/scroll,
trends, sources, next pages, audience, frustration, errors and performance.
Use days 1/7/30/90 (default 30), or both from and to. Page filters are device,
country, source, referrer, os and browser; path is a separate field. Retain
readAt, range, filters and version on continuations. Sparse samples remain null.

The existing query, summary, timeseries, funnel and compare tools remain. Filter
type=pageview for view counts. A funnel measures session overlap, not event
order. Raw SQL is unavailable through MCP. UI View all pagination and complete
labeled-click reporting remain separate coverage limits. Shared definitions:
https://frontpage.host/developers/analytics. MCP setup/tool limits:
https://frontpage.host/developers/mcp.
