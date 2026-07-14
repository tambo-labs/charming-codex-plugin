---
name: charming
description: Create, update, inspect, or troubleshoot Charming-hosted interactive web apps, or connect Codex to Charming.
---

# Charming

## Overview

Use this skill when the user asks to create an app with Charming, edit an existing Charming app, connect Charming MCP, or inspect Charming-generated app source.

Charming has two authoring paths:

- MCP tools: prefer this path when Charming tools such as `create_app`, `update_app`, `list_apps`, or `get_app` are available.
- HTTP API: use only when Charming MCP tools are not available and the agent has outbound HTTP access.

## MCP Workflow

When Charming MCP tools are available, build with the tools directly. Do not use `curl`, `fetch`, shell HTTP calls, or the raw HTTP API for app creation.

1. Read the starter guide at `https://usecharming.com/build-mcp.md`.
2. Read the design guide at `https://usecharming.com/design.md` before writing UI code.
3. Create the first version with `create_app({ module, ui, styles? })`.
4. Give the user the returned URL and `app_id`.
5. In Codex app sessions with a browser tool available, open the returned URL in Codex's in-app browser when MCP Apps inline UI does not visibly mount in the conversation. Do not claim the app is visible inline unless the host actually rendered it.
6. Offer one concrete next iteration, then call `update_app` only after the user agrees.
7. If the user hits a Charming limitation, call `submit_feedback({ app_id, text })` instead of silently working around it.

Charming exposes 21 tools; connected clients discover them via `tools/list`. The core authoring set is `create_app`, `update_app`, `get_app`, `get_app_source`, `list_apps`, and `delete_app`. Beyond those, `query_app` / `mutate_app` run an app's backend operations without editing code; `upload_asset` stores static assets; `share_app` / `unshare_app` / `list_app_shares`, `set_public` / `unset_public`, and `set_remixable` / `unset_remixable` control access and remixing; `rename_app`, `set_handle`, and `set_starter_prompt` manage URLs and share prompts; `submit_feedback` / `list_feedback` capture app feedback. The full descriptions live in [usecharming.com/llms-full.txt](https://usecharming.com/llms-full.txt) and the [charming-mcp listing](https://github.com/tambo-labs/charming-mcp).

Generated app code must follow the Charming contract:

- `module` is one ES module with a static `manifest` export and a default object exposing `fetch(request, env, ctx)`.
- `ui` is one inline JavaScript program that populates `#app`.
- UI code calls the backend through `window.buildy.api(manifest.id)`.
- Do not manage tokens in UI code; credentials attach automatically.
- No Node APIs, DOM APIs in the backend, outbound app `fetch`, external UI scripts, native form submit, `alert`, `confirm`, or `prompt`.

## HTTP Fallback

When Charming MCP tools are not available, follow `https://usecharming.com/start.md` and then `https://usecharming.com/build-http.md`. Prefer MCP setup first if the user asked for a connector or if the client can install the MCP server.

For Codex CLI MCP setup, the documented config is:

```toml
[mcp_servers.charming]
url = "https://charm.ing/mcp"
```

## Output Expectations

When creating or updating an app, end with the app URL, the `app_id`, what changed, and the next practical iteration.
