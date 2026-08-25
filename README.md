# Magister Marketing MCP

This portable Agent Plugin connects Cursor and Grok Build to Magister Marketing's
hosted, review-safe MCP endpoint. It adds no local executable, hook, skill, or
credential. The installed client connects directly over Streamable HTTP and asks
the user to authorize Magister through OAuth.

Magister lets an authorized marketing team inspect projects, brand profiles,
plans, audits, AI visibility, assets, social performance, and advertising data.
It can also propose and create confirmed AI-visibility tracking sets, then run
retry-safe measurement rounds with stable idempotency keys. Completed visibility
reports include readable terminal output and interactive charts in MCP
Apps-compatible hosts.
Its separately scoped tools can also run metered research and audits, create
assets and drafts, publish approved content, schedule social posts, and manage
paused-first ad campaigns. The catalog can create Meta and TikTok campaigns only
through their atomic paused-create flow and can pause running campaigns; it cannot
activate campaigns or begin ad spend. Irreversible,
external, send, and destructive effects are identified by each tool's metadata;
Magister enforces its scopes, roles, and documented immediate-confirmation gates
server-side.

## Install

The package is designed for publication from
`https://github.com/Magister-Marketing/magister-mcp`.

- Cursor: install the public repository as an Agent Plugin or use the Cursor
  Marketplace listing after approval. Cursor reads `plugin.json` and `mcp.json`.
- Grok Build: install the plugin from its marketplace listing after approval.
  Grok reads `.mcp.json`.
- Grok chat: add `https://mcp.magistermarketing.com/mcp/catalog` as a custom MCP
  connector. xAI does not currently document a self-serve public catalog
  submission route for Grok chat.

On first use, complete the Magister OAuth flow in the browser and select the
organization and permissions to grant. No API key belongs in these files.

For the complete custom-client surface, Magister customers may manually connect
`https://mcp.magistermarketing.com/mcp`. Public marketplace packages deliberately
use the narrower `/mcp/catalog` surface reviewed for broad distribution. The
catalog assumes an existing Magister account and entitlement and does not create
paid projects or initiate subscription checkout. It provides workflow tools and
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
- Both MCP configuration files pin the same HTTPS endpoint.
- Tool permissions and confirmation requirements are enforced by Magister's
  server; changing a local description cannot widen access.

This third-party plugin is authored and maintained by Magister Marketing. It is
not authored, controlled, verified, or endorsed by Cursor, Anysphere, xAI,
Anthropic, or OpenAI.

## License

The package files are available under the [MIT License](./LICENSE). The hosted
Magister service remains governed by Magister's Terms of Service.
