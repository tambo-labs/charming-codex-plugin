# Buildy Codex Plugin

Buildy is an MCP server that generates, hosts, and updates small interactive web apps. This repository publishes the Buildy Codex plugin as a public marketplace source.

## Install

Add this marketplace to Codex:

```sh
codex plugin marketplace add https://github.com/tambo-labs/buildy-codex-plugin.git
```

Then restart Codex, open **Plugins**, choose **Tambo Labs**, install **Buildy**, and start a new thread.

## What It Includes

- A Buildy MCP server config at `https://app.buildy.so/mcp`.
- A `buildy` skill that tells Codex to use the MCP tools first and follow the Buildy app authoring contract.
- Marketplace metadata for the Codex plugin directory.

## Buildy Authoring Flow

When installed, ask Codex to create or update a Buildy app. Codex should use the Buildy MCP tools directly:

- `create_app`
- `update_app`
- `list_apps`
- `get_app`
- `get_app_source`
- `submit_feedback`

For the full app authoring guide, see <https://buildy.so/start.md>.

## Publisher

Published by Tambo.
