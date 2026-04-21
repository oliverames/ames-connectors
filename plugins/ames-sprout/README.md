# ames-sprout

Sprout Social MCP connector for analytics, inbox messages, social listening, publishing, media uploads, and support cases.

## Runtime

This plugin starts the upstream npm package with `npx`:

```bash
npx -y @oliverames/sprout-mcp-server@latest
```

## Upstream Source

- Repository: https://github.com/oliverames/sprout-mcp-server
- Package: `@oliverames/sprout-mcp-server`
- Snapshot: `sources/sprout-mcp-server/`

Run `./sync-sources` from this plugin directory to refresh the snapshot from the upstream GitHub repository declared in `update-sources.json`.

## Environment

| Variable | Notes |
|----------|-------|
| `SPROUT_API_TOKEN` | See upstream README for requirement and fallback behavior. |
| `SPROUT_CLIENT_ID` | See upstream README for requirement and fallback behavior. |
| `SPROUT_CLIENT_SECRET` | See upstream README for requirement and fallback behavior. |
| `SPROUT_ORG_ID` | See upstream README for requirement and fallback behavior. |
