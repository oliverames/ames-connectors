<h1 align="center">Ames Connectors</h1>

<p align="center">
  <strong>A Claude Code and Codex marketplace for Oliver Ames' custom MCP connector plugins.</strong>
</p>

<p align="center">
  <code>2 connector plugins</code> &bull;
  <code>MCP server bundles</code> &bull;
  <code>remote-first marketplace</code>
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

Ames Connectors keeps custom MCP connector plugins separate from the broader `ames-claude` skills marketplace. Each connector lives in its own plugin bundle so it can be installed, reviewed, and maintained independently.

## Why This Exists

MCP connectors behave more like integrations than writing skills. They carry authentication requirements, runtime launch configs, source snapshots, and npm package references. Keeping them in a dedicated marketplace makes the boundary clearer: `ames-claude` can stay focused on skills and workflows, while `ames-connectors` handles service integrations.

## Available Connectors

| Plugin | Service | MCP package | Authentication |
|--------|---------|-------------|----------------|
| `ames-lytho` | Lytho Workflow | `@oliverames/lytho-mcp-server` | `LYTHO_CLIENT_ID`, `LYTHO_CLIENT_SECRET`, `LYTHO_TOKEN_URL` |
| `ames-ynab` | YNAB | `@oliverames/ynab-mcp-server` | `YNAB_API_TOKEN` |

## Marketplace Layout

```text
.agents/plugins/marketplace.json
plugins/
  ames-lytho/
    .codex-plugin/plugin.json
    .claude-plugin/plugin.json
    .mcp.json
    sources/lytho-mcp-server/
  ames-ynab/
    .codex-plugin/plugin.json
    .claude-plugin/plugin.json
    .mcp.json
    sources/ynab-mcp-server/
```

Each plugin includes a `.mcp.json` launch definition plus a source snapshot of the connector package. The npm packages remain the runtime entrypoints.

## Development

Update each connector in its source repository first, publish the npm package, then refresh the matching plugin snapshot here. The marketplace entry should continue to point at `./plugins/<plugin-name>` so Codex and Claude Code can resolve the bundle from this repository.

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
