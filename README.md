# Magister Marketing

Run your marketing from your AI assistant. This plugin connects Claude, Cursor,
and Grok Build to your Magister Marketing workspace and adds five skills that
show the assistant how to use it well. Ask what to work on next, how your site,
search, ads and social are doing, whether AI assistants recommend your brand, or
to draft and schedule this week's posts, and the assistant answers from your
own brand data in Magister instead of generic advice.

## What you can do

- **Work your marketing plan.** Find the highest-priority task, read its brief,
  record progress, and add, edit or reprioritize work.
- **See how your marketing is performing.** Ask about traffic, conversions,
  search queries and rankings, ad spend, and social and store results from the
  Google Analytics, Search Console, Google Ads, social, store and CRM accounts
  you connected to Magister, and what changed and why.
- **Track your AI visibility.** See how ChatGPT, Claude, Gemini, Perplexity and
  Google AI Overviews mention and rank your brand on the prompts your buyers ask,
  compare models over time, and open an interactive report in the chat.
- **Draft, schedule and publish social posts** in your brand voice, and read
  post and follower analytics and the best times to post.
- **Review paid ads and create campaigns safely.** Read Google Ads, Meta Ads and
  TikTok Ads performance, and create Meta, TikTok or Google Ads Search campaigns
  that are always created paused.
- **Use the tools your team connected to Magister,** one purpose-built tool per
  job: CRM and support (HubSpot, Pipedrive, Attio, folk, Zoho CRM, Intercom),
  email and SMS marketing (Klaviyo, Mailchimp, Kit, Resend and others), product
  and web analytics, Google Workspace, Notion, site and design tools, and social
  schedulers.

## What you need

A Magister Marketing account with MCP access and a brand set up in it, from
[magistermarketing.com](https://magistermarketing.com). What you can see and do
depends on your role, the services you connected to Magister, the permissions
you grant when you sign in, and your plan's usage budget.

## Install

- **Claude** (claude.ai, Cowork and Claude Code): install Magister Marketing
  from the Claude plugin directory once the listing is published; a submission
  does not mean an approved listing. To try this package before then, run
  `claude --plugin-dir /absolute/path/to/this/package`. Magister is also
  available in Claude as a connector on its own, without this plugin.
- **Cursor**: install this repository as an Agent Plugin, or use the Cursor
  Marketplace listing once approved.
- **Grok Build**: install the plugin from its marketplace listing once approved.
- **Grok chat**: add `https://mcp.magistermarketing.com/mcp/catalog` as a
  custom MCP connector.

The first time the assistant uses Magister, your browser opens Magister's
sign-in. Choose the organization and the permissions to grant. No API key goes
in these files.

## What stays in Magister

- **Changes that go live wait for your approval.** Drafts and record edits run
  directly. Publishing, sending, scheduling, and other changes that reach your
  audience or your connected services wait for your own approval.
- **No ad spend and no checkout.** Campaigns are created paused, and running
  campaigns can be paused. Turning a campaign on, starting a paid plan, and
  adding a priced brand are done in Magister.
- **Each AI app gets the tools its provider's rules allow.** Magister runs one
  MCP server for every app. Claude is not offered Magister's two general image
  generators, under Anthropic's directory rules. ChatGPT and Codex are not
  offered its Google Maps research and influencer discovery tools, under OpenAI's
  rules. A tool an app is not offered answers with a link to do that job in
  Magister. Connecting your own outside MCP servers to Magister needs Magister
  added by its own URL, `https://mcp.magistermarketing.com/mcp`, rather than
  through a directory listing or this plugin.
- **Magister enforces the rules on its server.** Its scopes, roles, budgets and
  confirmation gates apply whatever a local description says. Irreversible,
  external, send, and destructive effects are identified by each tool's
  metadata.

Magister provides workflow tools. It does not serve advertisements or sponsored
content inside the assistant.

## Skills

`skills/` holds five skills, plain Markdown read by the assistant: the marketing
plan, analytics, AI visibility, paid advertising, and social publishing. Each
names only tools Magister's server offers, and none contains commands or code.

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
- Every manifest points at the same HTTPS server; Claude's manifest selects its
  `/mcp/anthropic` address, which holds every connection to Anthropic's rules.
- Tool permissions and confirmation requirements are enforced by Magister's
  server; changing a local description cannot widen access.

This third-party plugin is authored and maintained by Magister Marketing. It is
not authored, controlled, verified, or endorsed by Cursor, Anysphere, xAI,
Anthropic, or OpenAI.

## For maintainers: one package, four hosts

Each host reads a different manifest and ignores the rest. `plugin.json` and
`mcp.json` are Agent Plugins 1.0.0 for Cursor. `.mcp.json` is read by Grok
Build and auto-discovered by Claude Code. `.claude-plugin/plugin.json` is Claude
Code's and Cowork's manifest; it declares the same `magister` server with the
`https://mcp.magistermarketing.com/mcp/anthropic` address, which replaces the
shared `/mcp/catalog` definition for Claude. All three addresses reach the same
server; the tools a connection is offered follow its app's rules, as described
under "What stays in Magister".

## License

The package files are available under the [MIT License](./LICENSE). The hosted
Magister service remains governed by Magister's Terms of Service.
