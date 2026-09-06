<p align="center">
  <img src="plugins/charming/assets/logo-animated.svg" alt="Charming animated logo" width="160">
</p>

<h1 align="center">Charming Codex Plugin</h1>

Charming is an MCP server that generates, hosts, and updates small interactive web apps. This repository publishes the Charming Codex plugin as a public marketplace source.

## Install

Add this marketplace to Codex:

```sh
codex plugin marketplace add https://github.com/tambo-labs/charming-codex-plugin.git
```

Then restart Codex, open **Plugins**, choose **Tambo Labs**, install **Charming**, and start a new thread.

## What It Includes

- A Charming MCP server config at `https://charm.ing/mcp`.
- A `charming` skill that tells Codex to use the MCP tools first and follow the Charming app authoring contract.
- Marketplace metadata for the Codex plugin directory.

## Charming Authoring Flow

When installed, ask Codex to create or update a Charming app. Codex should use the Charming MCP tools directly:

- `create_app`
- `read_docs`
- `update_app`
- `list_apps`
- `get_app`
- `get_app_source`
- `submit_feedback`

The agent can read the docs through the same MCP connection: `read_docs({})` returns the index, and `read_docs({ path: "build-mcp.md" })` reads the starter guide without a browser. Long pages return `next_offset`; pass it as `offset` with the same path to continue.

For the full app authoring guide, see <https://charm.ing/docs/llms-full.txt>.

## Publisher

Published by Tambo.
