# Skills for Fabric — Claude Edition

A Claude Code / Cowork plugin marketplace of skills, agents, and MCP servers for working with **Microsoft Fabric** and **Power BI**.

This is a repackaging of Microsoft's [`microsoft/skills-for-fabric`](https://github.com/microsoft/skills-for-fabric) (originally built for GitHub Copilot CLI) so that it installs cleanly through Claude's marketplace flows. All skill, agent, and reference content is Microsoft's; only the packaging was changed. See [`REPACKAGE-FOR-CLAUDE.md`](./REPACKAGE-FOR-CLAUDE.md) for the exact diff.

## What's inside

The marketplace is named `fabric-collection` and ships five plugins:

| Plugin | Skills | Agents | MCP server | Use it for |
| --- | --- | --- | --- | --- |
| `fabric-skills` | 31 | 4 | FabricIQ (HTTP) | The complete bundle — everything below in one install |
| `fabric-authoring` | 12 | 3 | — | Building Fabric solutions: SDKs, APIs, automation, CI/CD |
| `fabric-consumption` | 12 | 4 | FabricIQ (HTTP) | Interactive work: querying, exploring, and monitoring |
| `fabric-operations` | 5 | 3 | — | Diagnosing Fabric performance and health |
| `powerbi-authoring` | 6 | — | powerbi-modeling-mcp (stdio) | Power BI development: semantic models, PBIP/PBIR, reports |

Skills cover SQL warehouse/database, Spark, Eventhouse/KQL, Eventstream, Activator, Dataflows, semantic-model authoring and consumption, FabricIQ, medallion architecture, and migrations (Databricks, Synapse, HDInsight, pipelines).

Install `fabric-skills` for the full set, or pick a focused plugin if you only need one area.

## Install

**Requirement:** for the personal "Add marketplace" flow, this repo must be **public** — Cowork's sync fetches it anonymously, and private repos fail.

### Cowork (Claude Desktop)
Directory → Plugins → **Add marketplace** → paste `your-user/your-repo` → **Sync**, then install the plugins you want.

### Claude Code (CLI)
```
/plugin marketplace add your-user/your-repo
/plugin install fabric-skills@fabric-collection
```
Or install a focused plugin, e.g. `/plugin install powerbi-authoring@fabric-collection`.

Verify with `/plugin list`.

## MCP servers & authentication

Three plugins ship MCP servers that connect Claude to live Fabric / Power BI data:

- **FabricIQ** (`fabric-skills`, `fabric-consumption`) — HTTP server at the Fabric AI hub endpoint. Used to discover artifacts, inspect semantic-model schemas, and run DAX. Gated behind Microsoft 365 sign-in; you'll authenticate on first use.
- **powerbi-modeling-mcp** (`powerbi-authoring`) — runs locally via `npx @microsoft/powerbi-modeling-mcp`. Requires Node.js.

Once connected, you can ask data questions against your semantic models directly (e.g. querying your marketing semantic model), and Claude will generate and run the DAX for you.

## Maintaining this fork

The packaging changes are scriptable, so when Microsoft updates the upstream repo you can re-apply them against the newer version rather than hand-editing. If anything in the upstream layout changes, re-run `claude plugin validate .` before pushing.

## Attribution & license

Original work © Microsoft, licensed under MIT (see [`LICENSE`](./LICENSE)). This repackaging preserves that license and makes no changes to the skill/agent content.
