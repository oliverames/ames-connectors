# Worklog

## 2026-04-21 (evening) — Metadata enrichment, sync script introduction, README polish

**What changed**: First worklog for ames-connectors since the 2026-04-21 split from ames-claude. Enriched every Claude plugin.json across all 6 connectors (`ames-imagerelay`, `ames-lytho`, `ames-meta`, `ames-sprout`, `ames-unifi`, `ames-ynab`) with `homepage`, `repository`, `license`, and `category` (the existing `keywords` stayed). Introduced a `sync` script at repo root that mirrors the ames-claude pattern: propagates Claude-side version into `.codex-plugin/plugin.json`, wraps flat `.mcp.json` into Codex-shaped `.codex-plugin/mcp.json`, and regenerates both `marketplace.json` files threading the enriched metadata through. Before this, the two `marketplace.json` files were hand-edited — fine for a 6-plugin repo, but every bump risked drift. Patch-bumped every connector (+1 patch on each) and the marketplace `metadata.version` (1.1.0→1.2.0). Polished the README per `/readme-style`: it was missing install instructions entirely, so added a full Quick Start with declarative (settings.json snippet) and interactive (`/plugin install`) paths for both Claude Code and Codex, plus an Architecture section documenting the dual-host manifest pattern, a Development section covering bump/refresh-source/add-connector workflows, and a `category` column on the connectors table. Validated all 26 JSON files in the repo parse cleanly and sync is idempotent.

**Decisions made**:
- **Mirror ames-claude's sync rather than share code.** The two scripts are ~95% identical, differing only in the header string. Deliberate copy — keeps the repos operationally independent so a breaking change to one doesn't cascade. If a third marketplace appears, promote to a shared helper in `~/Developer/Scripts`.
- **Patch bumps across all 6 connectors.** Per plugin version policy (patch = content tweaks), metadata-only enrichment is a patch. No user-facing connector behavior changed.
- **Minor bump for marketplace metadata.version.** 1.1.0→1.2.0 signals the "flat→enriched" metadata boundary to marketplace indexers. Plugin-level patches roll up to a marketplace minor when the content format itself changes.
- **Category assignments follow Codex manifests.** Used the existing `category` values from each plugin's `.codex-plugin/plugin.json`: `marketing` (meta, sprout), `finance` (ynab), `productivity` (lytho, imagerelay), `developer-tools` (unifi). Claude Code's schema doesn't enforce an enum so consistency with Codex was the tiebreaker.
- **README install instructions default to ames-ynab.** First connector in both the `enabledPlugins` example and the interactive install. It's the one Oliver uses most; swapping is a one-line edit for any other connector.

**Left off at**:
- **NEW: Decide whether to extract sync into a shared helper.** Same as the ames-claude worklog: if a third marketplace appears, consolidate. For now the copy-paste is fine and independent.
- **NEW: Add a LICENSE reference check.** Repo has `LICENSE` (MIT) at root; plugin.json files now declare `"license": "MIT"`. Consistent, but confirm this is the intended license for connectors that vendor upstream MCP server code.
- **NEW: Consider per-connector READMEs.** Each plugin has its own directory but no per-connector README. Style guide recommends product-native README styling (Meta-colored for meta, UniFi-styled for unifi, etc.). Would make each plugin's directory feel like a first-class product page.
- **Still open: ames-lytho enablement decision** — published here but not enabled at user level in `~/.claude/settings.json`. Carried from the ames-claude worklog since the plugins moved here.
- **Still open: postpublish hooks in meta/sprout/imagerelay/unifi.** From the ames-claude worklog — those hooks previously called `bump-and-sync` against removed ames-claude entries; confirm they now target this repo correctly or drop them if unused.

**Open questions**:
- Is this repo's `main` branch the only branch, or is there a convention for feature branches on connector work? Prior worklog didn't exist to reference.
- Should `./sync` also run the per-plugin `sync-sources` scripts automatically when the upstream repos have new commits, or should those stay separate (current behavior: sync-sources is manual, per-connector)?

Part of a broader session that also touched ames-claude.

---
