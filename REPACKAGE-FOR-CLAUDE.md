# Repackaged for Claude Code / Cowork

This fork of `microsoft/skills-for-fabric` has been adjusted so it syncs through
Claude's marketplace flows (Cowork "Add marketplace" and the Claude Code CLI).
The original repo targets GitHub Copilot CLI and fails Claude's stricter sync.

## What changed
- `.claude-plugin/marketplace.json` rewritten: added a top-level `description`,
  trimmed each plugin entry to Claude's schema (name, source, description, version),
  and dropped the deprecated `skills-for-fabric` alias entry.
- Added `.claude-plugin/plugin.json` to each of the 5 plugins (was missing — this
  was the main reason the Cowork sync failed).
- Added `.mcp.json` at the plugin root for plugins that ship MCP servers
  (fabric-skills, fabric-consumption -> FabricIQ HTTP; powerbi-authoring ->
  powerbi-modeling-mcp). MCP config lives in `.mcp.json`, not inline in
  plugin.json (inline mcpServers is currently dropped by Claude Code).
- Renamed agent files `*.agent.md` -> `*.md` so Claude discovers them.

Skills/agents/references content is unchanged. Validated with
`claude plugin validate .` (passes).

## Deploy
1. Push this directory to a **public** GitHub repo of your own.
   (Public is required for Cowork's "Add marketplace" personal flow to sync;
   private plugin sources fail the anonymous server-side fetch.)
2. In Cowork: Directory > Plugins > Add marketplace > paste `your-user/your-repo` > Sync.
   Or in Claude Code CLI: `/plugin marketplace add your-user/your-repo`
   then `/plugin install fabric-skills@fabric-collection`.
3. The FabricIQ / Power BI MCP servers are M365-auth-gated; you'll sign in on first use.

Change `owner` in marketplace.json to your own name/URL if you like.
