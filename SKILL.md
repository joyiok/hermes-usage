---
name: hermes-usage
description: "Use when checking Hermes LLM token usage per session."
version: 1.0.0
---

# Checking Hermes token usage

Token usage per session is recorded in `$HERMES_HOME/state.db`:
`session_model_usage` holds per-model rows, `sessions` holds per-session totals.

## Command (read-only, never locks the live DB)

```bash
hermes-usage                 # current session (most recently active)
hermes-usage --session ID    # one session
hermes-usage --all           # totals across all sessions
hermes-usage --list          # list sessions with usage
```

Install `hermes-usage` (same repo) somewhere on PATH. Resolve home via
`$HERMES_HOME`, never hardcode `~/.hermes` (profiles differ).

## Notes

- Numbers update after each completed API call; the in-flight turn is not counted yet.
- `cost_status` is usually `unknown` and costs 0 — providers here don't report pricing; token counts are the reliable signal.
- `cache_read_tokens` dominates long sessions (prompt caching is working when this is large relative to `input_tokens`).
