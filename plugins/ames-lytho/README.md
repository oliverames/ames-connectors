# ames-lytho

Lytho Workflow MCP connector for work requests, tasks, proofs, projects, campaigns, files, and preferences through the Lytho Open API.

## Runtime

This plugin starts the upstream npm package with `npx`:

```bash
npx -y @oliverames/lytho-mcp-server@latest
```

## Upstream Source

- Repository: https://github.com/oliverames/lytho-mcp-server
- Package: `@oliverames/lytho-mcp-server`
- Snapshot: `sources/lytho-mcp-server/`

Run `./sync-sources` from this plugin directory to refresh the snapshot from the upstream GitHub repository declared in `update-sources.json`.

## Environment

| Variable | Notes |
|----------|-------|
| `LYTHO_CLIENT_ID` | See upstream README for requirement and fallback behavior. |
| `LYTHO_CLIENT_SECRET` | See upstream README for requirement and fallback behavior. |
| `LYTHO_TOKEN_URL` | See upstream README for requirement and fallback behavior. |
