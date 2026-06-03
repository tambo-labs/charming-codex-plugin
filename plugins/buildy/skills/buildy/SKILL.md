---
name: buildy
description: Create, update, inspect, or troubleshoot Buildy-hosted interactive web apps, or connect Codex to Buildy.
---

# Buildy

## Overview

Use this skill when the user asks to create an app with Buildy, edit an existing Buildy app, connect Buildy MCP, or inspect Buildy-generated app source.

Buildy has two authoring paths:

- MCP tools: prefer this path when Buildy tools such as `create_app`, `update_app`, `list_apps`, or `get_app` are available.
- HTTP API: use only when Buildy MCP tools are not available and the agent has outbound HTTP access.

## MCP Workflow

When Buildy MCP tools are available, build with the tools directly. Do not use `curl`, `fetch`, shell HTTP calls, or the raw HTTP API for app creation.

1. Read the starter guide at `https://buildy.so/build-mcp.md`.
2. Read the design guide at `https://buildy.so/design.md` before writing UI code.
3. Create the first version with `create_app({ module, ui, styles? })`.
4. Give the user the returned URL and `app_id`.
5. Offer one concrete next iteration, then call `update_app` only after the user agrees.
6. If the user hits a Buildy limitation, call `submit_feedback({ app_id, text })` instead of silently working around it.

Generated app code must follow the Buildy contract:

- `module` is one ES module with a static `manifest` export and a default object exposing `fetch(request, env, ctx)`.
- `ui` is one inline JavaScript program that populates `#app`.
- UI code calls the backend through `window.buildy.api(manifest.id)` or `window.buildy.app(manifest.id)`.
- Do not manage tokens in UI code; credentials attach automatically.
- No Node APIs, DOM APIs in the backend, outbound app `fetch`, external UI scripts, native form submit, `alert`, `confirm`, or `prompt`.

## HTTP Fallback

When Buildy MCP tools are not available, follow `https://buildy.so/start.md` and then `https://buildy.so/build-http.md`. Prefer MCP setup first if the user asked for a connector or if the client can install the MCP server.

For Codex CLI MCP setup, the documented config is:

```toml
[mcp_servers.buildy]
url = "https://app.buildy.so/mcp"
```

## Output Expectations

When creating or updating an app, end with the app URL, the `app_id`, what changed, and the next practical iteration.
