# Frontpage for Cursor

This is the held 0.9.0 candidate for the combined Frontpage MCP release. It
uses the same hosted service baseline as the Claude and ChatGPT/Codex
candidates. The existing public 0.3.3 package and marketplace review remain
separate; a candidate build does not publish an update.

Connect an existing Frontpage account to inspect website source, edit allowed
text files, check previews, and use People and email with separate consent.
Manage websites through the MCP connection with expanded consent, or through Frontpage. This package installs no local server,
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
Publishing and explicit source deletion require expanded Read and manage websites consent and the safeguards below. Billing and team management remain outside this connection.

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
credential changes are excluded. Native Booking uses the separate guidance below. Cancel and pause do
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

## Website management update

The six named website actions use expanded Read and manage websites consent. Existing grants stay unchanged until reauthorization. Read current site status for the publication version; publish only the exact reviewed ready build. Unpublish and article deletion require Admin. Redirect removal also requires existing Manage site settings consent. Source deletion and restore build previews without publishing. Normal client approval, roles, plan restrictions, current revisions and retry receipts apply. See https://frontpage.host/developers/mcp. This package update does not claim a new marketplace review or approval.


Publication tools affect the configured custom domain. A public Frontpage
subdomain continues to serve its preview under the existing visibility setting;
unpublish does not hide it. Sites without a custom domain return
NO_PUBLISHED_SURFACE. Changing subdomain visibility stays in the existing
Frontpage browser flow. Status reports the publication surface and whether a
custom domain is configured; a saved source revision is not a privacy change.


## Publisher and directory availability

Frontpage is the product. Rostra Labs, Inc. publishes this package; support is
support@frontpage.host. The direct server has 177 native tools after renewed Business consent for
Booking; earlier grants retain 138. OpenAI uses 273 named tools, or 234 without
Booking, for the same permitted operations. Marketplace
review and public publication are separate from this package release and direct
MCP setup. Use the current advertised schemas and your approved permissions.
Native Booking follows its existing rollout and renewed Business consent.
Unattended website-agent execution remains excluded.

The direct server also offers `frontpage_capture_screenshot` and
`frontpage_get_screenshot` with existing read access, protected PNG delivery
and continuation. See the MCP guide for capture limits and client coverage.
Directory approval and the published bundle remain separate from server updates.

## Booking

The direct server provides all 39 current native Booking actions as
`frontpage_booking_<action>`, for example `frontpage_booking_booking_create`.
Use `frontpage_get_module_docs` with `key: "booking"`, then Booking `status`.
Booking follows the existing native site/provider rollout. A plan or connection
alone does not enable it. No retired form engine is used.

Reconnect and approve Business read or read/manage to include Booking. Earlier
Business grants do not gain access. General People lookup still requires CRM
consent; native reservation changes may create a contact and send their normal
Booking notifications. Act only on the user's instruction.

Admins manage settings, resources and types. Editors and Admins manage bookings
and manual blocks. Viewers can use the restricted catalogs, read availability
and manage their own hours and authorized calendars. Generic source/business
write flags do not replace these native per-action checks.

Keep the complete native value, numeric `expectedRevision` and stable
`requestKey` after an uncertain write. Booking uses native receipts, not the
generic MCP `operationId` wrapper. First settings/own-hours saves may use revision
zero. `booking_withdraw` cancels the whole reservation; `booking_decline` rejects
a pending reschedule while keeping its confirmed booking.

Native data is in `data`, or versioned JSON `content` when large. The transient
retry flag is `replayed` on the result envelope. Native `nextCursor` goes in
`query.before`; text continuation uses `textOffset` and `expectedTextVersion`.
Restart if the result changes. Accepted effects do not prove inbox delivery.

Use `connect_request` for the existing authenticated human setup handoff. Never
ask for calendar credentials or a private feed URL in chat. External events
share busy times only; `event_open` returns owner-authenticated navigation, not
event contents. Account sign-in may still need calendar selection. Dismissing a
setup request does not connect a calendar.

Package publication and directory approval are separate. Use only tools
advertised by the current connection; a direct-server change does not prove
marketplace approval.

## Appointment start times

Appointment types use `value.startIntervalMinutes:null` for Automatic (match the current `durationMinutes`), or 5/10/15/20/30/45/60 for a fixed interval. Use the existing `frontpage_booking_type_save`; include the complete value, current revision and stable request key. Omit the field on updates to keep it. Starts align to midnight in the business time zone; buffers/conflicts remove starts without shifting them. New bookings and rescheduling use the current type rule. Stays are unchanged. Read availability and use its exact returned slot; do not calculate times in client code.
