<h1 align="center">Ames Connectors</h1>

<p align="center">
  <strong>A Claude Code and Codex marketplace for Oliver Ames' custom MCP connector plugins.</strong>
</p>

<p align="center">
  <code>6 connector plugins</code> &bull;
  <code>upstream source snapshots</code> &bull;
  <code>dual-host marketplace</code>
</p>

<p align="center">
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-f5a542?style=flat-square" alt="License">
  </a>
  <a href="https://www.buymeacoffee.com/oliverames">
    <img src="https://img.shields.io/badge/Buy_Me_a_Coffee-support-f5a542?style=flat-square&logo=buy-me-a-coffee&logoColor=white" alt="Buy Me a Coffee">
  </a>
</p>

---

Ames Connectors keeps Oliver's first-party MCP connector plugins separate from the broader `ames-claude` skills marketplace. Each connector lives in its own plugin bundle so it can be installed, reviewed, and maintained independently in Claude Code and Codex.

## Why This Exists

MCP connectors behave more like integrations than writing skills. They carry authentication requirements, runtime launch configs, upstream source snapshots, and npm package references. Keeping them in a dedicated marketplace makes the boundary clearer: `ames-claude` can stay focused on skills and workflows, while `ames-connectors` handles service integrations.

## Available Connectors

| Plugin | Service | Runtime package | Upstream repository |
|--------|---------|-----------------|---------------------|
| `ames-meta` | Meta Business Suite | `@oliverames/meta-mcp-server` | [`meta-mcp-server`](https://github.com/oliverames/meta-mcp-server) |
| `ames-ynab` | YNAB | `@oliverames/ynab-mcp-server` | [`ynab-mcp-server`](https://github.com/oliverames/ynab-mcp-server) |
| `ames-sprout` | Sprout Social | `@oliverames/sprout-mcp-server` | [`sprout-mcp-server`](https://github.com/oliverames/sprout-mcp-server) |
| `ames-lytho` | Lytho Workflow | `@oliverames/lytho-mcp-server` | [`lytho-mcp-server`](https://github.com/oliverames/lytho-mcp-server) |
| `ames-imagerelay` | Image Relay | `imagerelay-mcp-server` | [`imagerelay-mcp-server`](https://github.com/oliverames/imagerelay-mcp-server) |
| `ames-unifi` | UniFi Network | `ames-unifi-mcp` | [`ames-unifi-mcp`](https://github.com/oliverames/ames-unifi-mcp) |

## Marketplace Layout

```text
.claude-plugin/marketplace.json
.agents/plugins/marketplace.json
plugins/
  ames-meta/
    .claude-plugin/plugin.json
    .codex-plugin/plugin.json
    .codex-plugin/mcp.json
    .mcp.json
    update-sources.json
    sync-sources
    sources/meta-mcp-server/
  ames-ynab/
    .claude-plugin/plugin.json
    .codex-plugin/plugin.json
    .codex-plugin/mcp.json
    .mcp.json
    update-sources.json
    sync-sources
    sources/ynab-mcp-server/
  ames-sprout/
    .claude-plugin/plugin.json
    .codex-plugin/plugin.json
    .codex-plugin/mcp.json
    .mcp.json
    update-sources.json
    sync-sources
    sources/sprout-mcp-server/
  ames-lytho/
    .claude-plugin/plugin.json
    .codex-plugin/plugin.json
    .codex-plugin/mcp.json
    .mcp.json
    update-sources.json
    sync-sources
    sources/lytho-mcp-server/
  ames-imagerelay/
    .claude-plugin/plugin.json
    .codex-plugin/plugin.json
    .codex-plugin/mcp.json
    .mcp.json
    update-sources.json
    sync-sources
    sources/imagerelay-mcp-server/
  ames-unifi/
    .claude-plugin/plugin.json
    .codex-plugin/plugin.json
    .codex-plugin/mcp.json
    .mcp.json
    update-sources.json
    sync-sources
    sources/ames-unifi-mcp/
```

Each plugin includes:

- `.claude-plugin/plugin.json` for Claude Code
- `.codex-plugin/plugin.json` for Codex
- `.mcp.json` for Claude Code's flat MCP runtime launch config
- `.codex-plugin/mcp.json` for Codex's wrapped `{ "mcpServers": ... }` runtime launch config
- `update-sources.json` pointing at the upstream GitHub repository
- `sync-sources` to refresh `sources/` from the upstream repository

## Development

Update each connector in its upstream repository first, publish the npm package, then run the matching plugin's `sync-sources` script here. The marketplace entries should continue to point at `./plugins/<plugin-name>` so Claude Code and Codex can resolve the bundle from this repository.

---

<p align="center">
  <a href="https://www.buymeacoffee.com/oliverames">
    <img src="https://img.shields.io/badge/Buy_Me_a_Coffee-support-f5a542?style=for-the-badge&logo=buy-me-a-coffee&logoColor=white" alt="Buy Me a Coffee">
  </a>
</p>

<p align="center">
  <sub>
    Built by <a href="https://ames.consulting">Oliver Ames</a> in Vermont
    &bull; <a href="https://github.com/oliverames">GitHub</a>
    &bull; <a href="https://linkedin.com/in/oliverames">LinkedIn</a>
    &bull; <a href="https://bsky.app/profile/oliverames.bsky.social">Bluesky</a>
  </sub>
</p>
