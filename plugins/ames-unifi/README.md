# ames-unifi

UniFi Network MCP connector for controller management, clients, devices, firewall, Wi-Fi, VPN, switching, hotspot, and traffic tools.

## Runtime

This plugin starts the upstream npm package with `npx`:

```bash
npx -y ames-unifi-mcp@latest
```

## Upstream Source

- Repository: https://github.com/oliverames/ames-unifi-mcp
- Package: `ames-unifi-mcp`
- Snapshot: `sources/ames-unifi-mcp/`

Run `./sync-sources` from this plugin directory to refresh the snapshot from the upstream GitHub repository declared in `update-sources.json`.

## Environment

| Variable | Notes |
|----------|-------|
| `UNIFI_HOST` | See upstream README for requirement and fallback behavior. |
| `UNIFI_API_KEY` | See upstream README for requirement and fallback behavior. |
| `UNIFI_USERNAME` | See upstream README for requirement and fallback behavior. |
| `UNIFI_PASSWORD` | See upstream README for requirement and fallback behavior. |
| `UNIFI_SITE` | See upstream README for requirement and fallback behavior. |
| `UNIFI_VERIFY_SSL` | See upstream README for requirement and fallback behavior. |
| `UNIFI_TOOL_MODE` | See upstream README for requirement and fallback behavior. |
| `UNIFI_PERMISSION_PROFILE` | See upstream README for requirement and fallback behavior. |
