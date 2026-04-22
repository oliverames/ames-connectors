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

## Why this exists

MCP connectors behave more like integrations than writing skills. They carry authentication requirements, runtime launch configs, upstream source snapshots, and npm package references. Keeping them in a dedicated marketplace makes the boundary clearer: `ames-claude` stays focused on skills and workflows, `ames-connectors` handles service integrations. That split also means connector version bumps don't churn the skills marketplace, and each connector can be installed, reviewed, and authorized independently on the host that needs it.

## Quick start

### Claude Code (official, supported)

**Declarative install.** Add to `~/.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "ames-connectors": {
      "source": { "source": "github", "repo": "oliverames/ames-connectors" },
      "autoUpdate": true
    }
  },
  "enabledPlugins": {
    "ames-ynab@ames-connectors": true
  }
}
```

Restart Claude Code. The marketplace registers, the selected plugins install, and `autoUpdate` keeps them current on each launch. Swap in whichever connectors you want from the table below.

**Interactive install.** Or run:

```
/plugin marketplace add oliverames/ames-connectors
/plugin install ames-ynab@ames-connectors
```

Each connector reads its credentials from environment variables at launch. See the per-connector READMEs for the exact variables required.

### Codex (experimental)

```
codex marketplace add https://github.com/oliverames/ames-connectors
```

Then install individual plugins through Codex's plugin UI or CLI.

> **Heads-up:** Codex's marketplace commands are still stabilizing. Verify exact syntax with `codex --help` before scripting. File an issue if any Codex manifest in this repo falls out of spec.

## Available connectors

| Plugin | Service | Category | Runtime package | Upstream repository |
|--------|---------|----------|-----------------|---------------------|
| [`ames-meta`](plugins/ames-meta/) | Meta Business Suite | marketing | `@oliverames/meta-mcp-server` | [`meta-mcp-server`](https://github.com/oliverames/meta-mcp-server) |
| [`ames-ynab`](plugins/ames-ynab/) | YNAB | finance | `@oliverames/ynab-mcp-server` | [`ynab-mcp-server`](https://github.com/oliverames/ynab-mcp-server) |
| [`ames-sprout`](plugins/ames-sprout/) | Sprout Social | marketing | `@oliverames/sprout-mcp-server` | [`sprout-mcp-server`](https://github.com/oliverames/sprout-mcp-server) |
| [`ames-lytho`](plugins/ames-lytho/) | Lytho Workflow | productivity | `@oliverames/lytho-mcp-server` | [`lytho-mcp-server`](https://github.com/oliverames/lytho-mcp-server) |
| [`ames-imagerelay`](plugins/ames-imagerelay/) | Image Relay | productivity | `imagerelay-mcp-server` | [`imagerelay-mcp-server`](https://github.com/oliverames/imagerelay-mcp-server) |
| [`ames-unifi`](plugins/ames-unifi/) | UniFi Network | developer-tools | `ames-unifi-mcp` | [`ames-unifi-mcp`](https://github.com/oliverames/ames-unifi-mcp) |

## Marketplace layout

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

## Architecture

The repo carries two parallel manifest namespaces under one plugin tree, the same pattern as `ames-claude`:

| Host | Marketplace manifest | Per-plugin manifest | MCP config |
|------|----------------------|---------------------|-----------|
| Claude Code | `.claude-plugin/marketplace.json` | `.claude-plugin/plugin.json` | flat `.mcp.json` at plugin root |
| Codex (experimental) | `.agents/plugins/marketplace.json` | `.codex-plugin/plugin.json` | wrapped `.codex-plugin/mcp.json` |

`.claude-plugin/plugin.json` is the single source of truth. Metadata — `version`, `author`, `homepage`, `repository`, `license`, `keywords`, `category` — propagates into the generated marketplace entry at `./sync` time.

## Development

### Bumping a connector

1. Edit `plugins/<plugin-name>/.claude-plugin/plugin.json` — bump the `version` and update any affected metadata (description, keywords, category).
2. Run `./sync` from the repo root.
   - The Claude-side version propagates to `.codex-plugin/plugin.json`.
   - Both `marketplace.json` files regenerate with the enriched metadata.
   - `.mcp.json` is re-wrapped into `.codex-plugin/mcp.json` for Codex.
3. Commit and push. Installed clients pick up the new version on their next marketplace refresh.

### Refreshing a connector's source snapshot

Update the connector's upstream repository first, publish the npm package, then run the matching plugin's `sync-sources` script here. Marketplace entries continue to point at `./plugins/<plugin-name>` so Claude Code and Codex resolve the bundle from this repository.

```bash
cd plugins/ames-ynab
./sync-sources
```

### Adding a new connector

1. Create `plugins/<plugin-name>/` with both `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json`.
2. Add `.mcp.json` (Claude shape) at the plugin root.
3. Add a `sync-sources` script and an `update-sources.json` pointing at the upstream repository.
4. Run `./sync` — the marketplace manifests regenerate automatically. No hand-editing required.

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
