---
name: yocrow
description: >-
  Use the Yocrow MCP tools find_actions, run_read_action and run_write_action to
  work with the user's connected providers such as GitHub, Linear, Notion, Neon,
  Supabase, PostHog, Datadog and Resend.
license: MIT
---

# Yocrow

1. `find_actions` finds actions.
2. `run_read_action` runs `[read]` actions.
3. `run_write_action` runs `[write]` and `[destructive]` actions.

- Names like `linear_save_issue` are stable across turns and sessions. Reuse a name you already know and skip `find_actions`.
- Search every provider you need in one `find_actions` call with `searches`, one entry per provider.
- Batch independent calls with `calls` only when they touch at least 2 providers. Never mix reads and writes in one batch. Run dependent calls in order.
- Run writes only for changes the user asked for.
- Yocrow shows no prompts. If the user declines a write in the editor, do not retry.
- Never ask for tokens, passwords or Companion Keys in chat.
- `provider not connected` means the user must run `yocrow connect <provider>`.
- If nothing works, ask the user to run `yocrow status` and, if needed, `yocrow login`.
