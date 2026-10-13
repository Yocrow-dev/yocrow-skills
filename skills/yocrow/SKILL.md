---
name: yocrow
description: >-
  Use the Yocrow MCP tools discover_actions, inspect_action and run_action to
  work with the user's connected providers such as GitHub, Linear, Notion, Neon,
  Supabase, PostHog, Datadog and Resend.
license: MIT
---

# Yocrow

1. `discover_actions` with a short task `query`, for example `"search pull requests"`.
2. `inspect_action` with the chosen `action_ref` to read its `input_schema`.
3. `run_action` with that `action_ref` and `arguments` matching the schema.

- Get every `action_ref` from discovery in this session. Discover again if one is rejected.
- Prefer `read` actions. Use `write` or `destructive` only for changes the user asked for.
- On `confirmation_required` or a declined prompt, tell the user and do not retry.
- Never ask for tokens, passwords or Companion Keys in chat.
- No results for a provider means it is not connected. Ask the user to run `yocrow connect <provider>`.
- If nothing works, ask the user to run `yocrow status` and, if needed, `yocrow login`.
