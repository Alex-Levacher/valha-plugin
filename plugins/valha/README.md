# Valha plugin beta

Valha turns AI work into durable pages and lets assistants reuse trusted, permissioned knowledge.
This public repository distributes the official beta plugin for Codex and Claude Code. The hosted
OAuth MCP server remains operated at `https://valha.link/mcp`; this repository contains no Valha
server code, credentials, or customer data.

## Codex

```bash
codex plugin marketplace add Alex-Levacher/valha-plugin
codex plugin add valha@valha
```

Authenticate the `valha` MCP server when prompted, then start a new task so Codex loads the plugin
skills.

## Claude Code

```bash
claude plugin marketplace add Alex-Levacher/valha-plugin
claude plugin install valha@valha
```

Authenticate the Valha MCP server when prompted, then start a new session so Claude Code loads the
plugin skills.

## ChatGPT developer beta

ChatGPT does not install this repository during the beta. Enable Developer mode under **Settings →
Security and login**, add a custom plugin, and use `https://valha.link/mcp` as the connection URL.
Developer mode availability depends on the account and workspace policy. After Valha tool metadata
changes, open the connection, select **Refresh**, and start a new conversation.

The permanent installation guide is available at [valha.link/connect](https://valha.link/connect).

## Updates

Beta releases use `0.x` versions. Upgrade the marketplace before starting a new task or session:

```bash
codex plugin marketplace upgrade valha
```

Claude Code users can update the installed marketplace and plugin through the plugin manager. See
[CHANGELOG.md](./CHANGELOG.md) for contract changes.

## Security and terms

Report vulnerabilities privately as described in [SECURITY.md](./SECURITY.md). Valha's
[Privacy Policy](https://valha.link/privacy) and [Terms](https://valha.link/terms) apply to the hosted
service. This distribution package is not open source; see [LICENSE](./LICENSE).
