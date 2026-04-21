# ames-ynab

YNAB MCP connector for budgets, transactions, categories, scheduled transactions, accounts, months, payees, and budget review workflows.

## Runtime

This plugin starts the upstream npm package with `npx`:

```bash
npx -y @oliverames/ynab-mcp-server@latest
```

## Upstream Source

- Repository: https://github.com/oliverames/ynab-mcp-server
- Package: `@oliverames/ynab-mcp-server`
- Snapshot: `sources/ynab-mcp-server/`

Run `./sync-sources` from this plugin directory to refresh the snapshot from the upstream GitHub repository declared in `update-sources.json`.

## Environment

| Variable | Notes |
|----------|-------|
| `YNAB_API_TOKEN` | See upstream README for requirement and fallback behavior. |
| `YNAB_BUDGET_ID` | See upstream README for requirement and fallback behavior. |
| `YNAB_OP_PATH` | See upstream README for requirement and fallback behavior. |
