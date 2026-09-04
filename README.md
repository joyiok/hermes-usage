# hermes-usage

Show LLM token usage recorded in the Hermes Agent `state.db` — per model, per session, read-only (never locks the live gateway DB).

## Install

```bash
cp hermes-usage ~/.hermes/bin/   # or anywhere on your PATH
chmod +x ~/.hermes/bin/hermes-usage
```

## Usage

```bash
hermes-usage                 # current session (most recently active)
hermes-usage --session ID    # one session
hermes-usage --all           # totals across all sessions
hermes-usage --list          # list sessions with usage
```

Resolves the database via `$HERMES_HOME` (falls back to `~/.hermes`), so it works across profiles.

## Notes

- Numbers update after each completed API call; the in-flight turn isn't counted yet.
- `cost_status` is usually `unknown` with cost 0 — most providers don't report pricing; token counts are the reliable signal.
- `cache_read_tokens` dominates long sessions (prompt caching working = large cache_read vs input).

## SKILL.md

A Hermes skill definition is included — drop the repo (or just `SKILL.md`) into your skills directory so the agent checks usage with `hermes-usage` whenever relevant.

## License

MIT
