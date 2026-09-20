# Adspirer for Hermes Agent

Create, analyze, and optimize paid-media campaigns from Hermes Agent. This portable Agent Plugins
v1 package connects Hermes to Adspirer's hosted MCP service and includes workflow skills for Google
Ads, Meta Ads, TikTok Ads, LinkedIn Ads, Amazon Ads, and ChatGPT Ads.

## Install

After the plugin is accepted into the Hermes catalog:

```bash
hermes plugins install adspirer --no-enable
hermes plugins enable adspirer
hermes mcp login adspirer
```

Until then, install directly from the official Adspirer repository:

```bash
hermes plugins install Adspirer/adspirer-hermes-plugin --no-enable
hermes plugins enable adspirer
hermes mcp login adspirer
```

Complete the browser-based Adspirer sign-in, then start a new Hermes session or run
`/reload-mcp`. Connect or reconnect advertising accounts at
[adspirer.ai/connections](https://adspirer.ai/connections).

## Try it

Open a brand or project directory and ask Hermes:

- "Set up this folder as my Adspirer brand workspace."
- "Review the last 30 days across every connected ad platform."
- "Find wasted spend and show me the changes you recommend."
- "Create a Google Search campaign for this landing page with a $50 daily budget."
- "Write three Meta ad variants in the brand voice from BRAND.md."

For first-time setup, load the bundled `adspirer-setup` skill. Hermes exposes portable skills under
a namespaced installed-plugin identifier; use `skills_list` to find the full qualified name.

## Safety contract

Adspirer manages advertising accounts that can spend real money. The bundled skills require the
agent to:

- inspect the live account before proposing a write;
- show the exact budget and request explicit approval before spending or moving money;
- create new campaigns paused;
- verify every create or update by reading it back; and
- prefer reversible actions and confirm destructive operations.

Authentication and advertising-platform authorization remain scoped to the user's Adspirer
account. This repository contains no access tokens, API keys, ad-platform credentials, or customer
data.

## Included components

- One Streamable HTTP MCP server: `https://mcp.adspirer.com/mcp`
- Fourteen advertising and campaign-management skills
- OAuth 2.1 authorization with PKCE and dynamic client registration
- No local executable, bootstrap script, hook, native tool, or self-updater

The package follows the published
[Agent Plugins v1 specification](https://agent-plugins.org/specification). Hermes discovers the
root `plugin.json`, `mcp.json`, and immediate child directories under `skills/`.

## Included skills

| Skill | Purpose |
| --- | --- |
| `adspirer-agent` | Safety contract and routing for paid-media work |
| `adspirer-setup` | Connect Adspirer and build `BRAND.md` and `STRATEGY.md` |
| `adspirer-mcp` | MCP tool discovery, router calls, account IDs, quotas, and budget units |
| `adspirer-launch` | Plan and create paused campaigns |
| `adspirer-performance-review` | Cross-platform performance reporting and diagnosis |
| `adspirer-optimize` | Wasted-spend analysis and approval-gated optimization |
| `adspirer-creative` | Platform-aware ad-copy and creative workflows |
| `adspirer-google-ads` | Google Ads campaign guidance |
| `adspirer-meta-ads` | Meta Ads campaign guidance |
| `adspirer-tiktok-ads` | TikTok Ads campaign guidance |
| `adspirer-linkedin-ads` | LinkedIn Ads campaign guidance |
| `adspirer-amazon-ads` | Amazon Ads campaign guidance |
| `adspirer-chatgpt-ads` | ChatGPT Ads campaign guidance |
| `adspirer-docs` | Adspirer product, plan, connection, and troubleshooting documentation |

## Authentication

The plugin intentionally stores no credentials in `mcp.json`. When the hosted server returns an
authorization challenge, Hermes discovers Adspirer's OAuth metadata and manages the browser login,
PKCE exchange, refresh tokens, and local token storage. Reauthorize at any time with:

```bash
hermes mcp login adspirer
```

## Scheduled reviews

Hermes can run recurring advertising reviews through its `cronjob` tool. Attach the relevant
Adspirer skill and use a project work directory so scheduled runs can read `BRAND.md` and
`STRATEGY.md`. A scheduled run consumes Adspirer tool calls like an interactive session; weekly is
the recommended default for performance reviews.

## Development

Validate the package with the same admission command used by the Hermes catalog:

```bash
hermes plugins validate .
```

Before releasing, test installation from a clean Hermes profile, complete
`hermes mcp login adspirer`, confirm all fourteen skills load, and run at least one read-only MCP
call.

## Support and security

- Website: [adspirer.com](https://www.adspirer.com)
- Documentation: [adspirer.com/docs](https://www.adspirer.com/docs)
- Issues: [GitHub Issues](https://github.com/Adspirer/adspirer-hermes-plugin/issues)
- Security reports: [SECURITY.md](SECURITY.md)

Licensed under the [MIT License](LICENSE).
