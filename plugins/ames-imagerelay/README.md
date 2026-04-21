# ames-imagerelay

Image Relay MCP connector for digital asset management, files, folders, collections, products, metadata, upload links, and webhooks.

## Runtime

This plugin starts the upstream npm package with `npx`:

```bash
npx -y imagerelay-mcp-server@latest
```

## Upstream Source

- Repository: https://github.com/oliverames/imagerelay-mcp-server
- Package: `imagerelay-mcp-server`
- Snapshot: `sources/imagerelay-mcp-server/`

Run `./sync-sources` from this plugin directory to refresh the snapshot from the upstream GitHub repository declared in `update-sources.json`.

## Environment

| Variable | Notes |
|----------|-------|
| `IMAGERELAY_API_KEY` | See upstream README for requirement and fallback behavior. |
| `IMAGERELAY_SUBDOMAIN` | See upstream README for requirement and fallback behavior. |
