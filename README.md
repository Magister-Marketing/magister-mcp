# Magister Marketing MCP

This portable plugin connects Cursor, Grok Build, Claude Code, and Cowork to
Magister Marketing's hosted, review-safe MCP endpoint, plus five Markdown skills
that show the assistant how to use it well. It adds no local executable, hook, or
credential. The installed client connects directly over Streamable HTTP and asks
the user to authorize Magister through OAuth.

Three manifest formats sit side by side because each host reads a different one
and ignores the rest: `plugin.json` and `mcp.json` are Agent Plugins 1.0.0 for
Cursor, `.claude-plugin/plugin.json` is Claude Code's manifest, and `.mcp.json`
carries the single server definition that both Grok Build and Claude Code read.

Magister lets an authorized marketing team inspect projects, brand profiles,
plans, audits, AI visibility, assets, social performance, and advertising data.
It can also propose and create confirmed AI-visibility tracking sets, then run
retry-safe measurement rounds with stable idempotency keys. Completed visibility
reports include readable terminal output and interactive charts in MCP
Apps-compatible hosts.
Its separately scoped tools can also run metered research and audits, query the
connected Google Ads, Analytics and Search Console accounts read-only, write text
assets and website drafts, draft and schedule social posts, and manage paused-first
ad campaigns. It can create Meta, TikTok, and Google Ads Search campaigns only
through their atomic paused-create flow and can pause running campaigns; it cannot
activate campaigns or begin ad spend. It works with the services a team connected
to Magister through one purpose-built tool per job: CRM and support (HubSpot,
Pipedrive, Attio, folk, Zoho CRM, Intercom), prospecting, email and SMS
marketing (Klaviyo, Mailchimp, Kit, Resend and others), product and web
analytics, Google Workspace, Notion, site and design tools (Vercel, GitLab,
Builder.io, Framer, Canva, Formspree), and social schedulers. Drafts and record
edits run directly; publishing, sending, scheduling, and other changes that go
live wait for the user's own approval. Irreversible, external, send, and
destructive effects are identified by each tool's metadata;
Magister enforces its scopes, roles, and documented immediate-confirmation gates
server-side.

Shared marketing context includes confirmed preferences, observed style, measured
lessons and source coverage. Agents record explicit preferences and creative
feedback through tools; Magister cannot read their other conversations automatically.

## Skills

`skills/` holds five skills, plain Markdown read by the assistant: analytics,
AI visibility, the marketing plan, paid advertising, and social publishing. Each
names only tools this endpoint serves, and none contains commands or code.

## Install

The package is designed for publication from
`https://github.com/Magister-Marketing/magister-mcp`.

- Cursor: install the public repository as an Agent Plugin or use the Cursor
  Marketplace listing after approval. Cursor reads `plugin.json` and `mcp.json`.
- Grok Build: install the plugin from its marketplace listing after approval.
  Grok reads `.mcp.json`.
- Claude Code and Cowork: install from the Claude plugin directory after
  approval, or add this repository as a plugin marketplace directly. Claude Code
  reads `.claude-plugin/plugin.json` and auto-discovers the server from
  `.mcp.json`. Magister is also available in Claude as a connector on its own,
  without this plugin, through the Claude connector directory.
- Grok chat: add `https://mcp.magistermarketing.com/mcp/catalog` as a custom MCP
  connector. xAI does not currently document a self-serve public catalog
  submission route for Grok chat.

On first use, complete the Magister OAuth flow in the browser and select the
organization and permissions to grant. No API key belongs in these files.

`https://mcp.magistermarketing.com/mcp` and `/mcp/catalog` serve the same tools;
they differ only in the OAuth resource a token is bound to, and the packages use
`/mcp/catalog`, the listed address. The endpoint assumes an existing Magister
account and entitlement and does not create paid projects or initiate
subscription checkout. It provides workflow tools and
does not serve advertisements or sponsored content inside the client.

## Network and data disclosure

The plugin itself directly contacts only these Magister-owned origins:

- `https://mcp.magistermarketing.com` for MCP transport and OAuth discovery.
- `https://magistermarketing.com` for browser-based consent, connection pages,
  documentation, support, privacy, and account management.

After authorization, tool calls can send the user's request and selected
Magister project data to Magister. Responses can contain project, brand, plan,
audit, asset, analytics, content, social, and advertising information. A user can
also authorize tools that create or change Magister data or initiate actions on
services they connected to Magister. Third-party credentials remain encrypted on
Magister's servers and are not placed in the plugin, returned to the client, or
stored on the user's machine by this package.

Magister may call a connected provider server-side only when the user has linked
that service and invokes a relevant tool. Connector activity follows Magister's
[Privacy Policy](https://magistermarketing.com/privacy),
[Terms of Service](https://magistermarketing.com/terms), and documented account
deletion and retention controls. Support is available at
[magistermarketing.com/support](https://magistermarketing.com/support).

## Security

- OAuth credentials and provider tokens are never committed to this package.
- There are no commands, subprocesses, hooks, or executable files.
- Both MCP configuration files pin the same HTTPS endpoint, and the Claude Code
  manifest declares no server of its own, so there is one endpoint to review.
- Tool permissions and confirmation requirements are enforced by Magister's
  server; changing a local description cannot widen access.

This third-party plugin is authored and maintained by Magister Marketing. It is
not authored, controlled, verified, or endorsed by Cursor, Anysphere, xAI,
Anthropic, or OpenAI.

## License

The package files are available under the [MIT License](./LICENSE). The hosted
Magister service remains governed by Magister's Terms of Service.
