# ames-meta

Meta Business Suite MCP connector for Facebook Pages, Instagram, Threads, Ads Manager, Commerce, Conversions API, and related Graph API workflows.

## Runtime

This plugin starts the upstream npm package with `npx`:

```bash
npx -y @oliverames/meta-mcp-server@latest
```

## Upstream Source

- Repository: https://github.com/oliverames/meta-mcp-server
- Package: `@oliverames/meta-mcp-server`
- Snapshot: `sources/meta-mcp-server/`

Run `./sync-sources` from this plugin directory to refresh the snapshot from the upstream GitHub repository declared in `update-sources.json`.

## Environment

| Variable | Notes |
|----------|-------|
| `META_ACCESS_TOKEN` | See upstream README for requirement and fallback behavior. |
| `THREADS_ACCESS_TOKEN` | See upstream README for requirement and fallback behavior. |
