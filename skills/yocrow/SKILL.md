---
name: yocrow
description: >-
  Use the Yocrow MCP server to work with the user's connected providers, such as
  GitHub, Linear, Notion, Neon, Supabase, PostHog, Datadog and Resend. Use when a
  task needs data or actions from one of those services, when the tools
  discover_actions, inspect_action or run_action are available, or when the user
  mentions Yocrow, yocrow connect or a provider that is not responding.
license: MIT
---

# Yocrow

Yocrow connects you to the official MCP servers of the providers the user has
connected on their device. Instead of every provider's full tool list, you see
three tools. Use them in order.

## Workflow

1. **Find the action with `discover_actions`.** Pass a short plain-language
   `query` that describes the task, such as `"search pull requests"` or
   `"create a Linear issue"`. The query can be up to 256 characters. Results are
   ranked by how well the action name and summary match, and each result has an
   `action_ref`, the provider in `source_id`, the action `name`, a short
   `summary` and a `classification` of `read`, `write` or `destructive`.
2. **Read the details with `inspect_action`.** Pass the chosen `action_ref`. The
   response contains the full description and the `input_schema` for the
   action. Always inspect before running, because summaries are shortened and
   schemas differ between providers.
3. **Run it with `run_action`.** Pass the same `action_ref` and an `arguments`
   object that matches the `input_schema` exactly.

## Rules

- Do not guess action names or references. Always get them from
  `discover_actions` in the current session. References expire, so discover
  again if a reference is rejected.
- Prefer `read` actions when they answer the question. Use `write` or
  `destructive` actions only when the user asked for that change.
- Write and destructive actions may show the user an approval prompt in their
  editor. Wait for the result. If the response contains
  `"code": "confirmation_required"`, tell the user the action needs their
  approval and do not retry it in a loop.
- If the user declines an action, do not run it again with the same arguments.
- Never ask the user to paste a provider token, password or Companion Key into
  the chat. Credentials are entered only in the user's own terminal.
- Discovery returns a limited number of results, with at most three from any
  one provider. If the right action is missing, rephrase the query with the
  provider name or a more specific verb.

## When something is not available

- **No results for a provider.** The provider is probably not connected. Ask
  the user to run `yocrow connect <provider>` in their terminal, for example
  `yocrow connect github`, and then try again.
- **`source_errors` in the discovery result.** That provider could not list its
  actions. Continue with other providers and tell the user which one failed.
- **"The selected local Yocrow action is unavailable".** The input did not match
  the schema, the reference expired or the provider refused the call. Inspect the
  action again, correct the arguments once, and if it still fails, report it to
  the user instead of retrying.
- **Nothing works at all.** Ask the user to run `yocrow status` in their
  terminal. If the device is not signed in, they need to run `yocrow login` with
  a Companion Key from the Yocrow dashboard. Do not run these commands yourself,
  because they need the user's protected terminal input.
