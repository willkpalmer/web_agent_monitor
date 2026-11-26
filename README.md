# Agent Monitor

A single static page that sorts your Claude Code sessions into three lanes:

| Lane | Claude status bucket |
|---|---|
| **Needs attention** | `BLOCKED` (waiting on you), `REVIEW_READY`, `FAILED` |
| **Running** | `WORKING` |
| **Dormant** | `COMPLETED`, plus archived sessions (hidden behind the *Archived* toggle) |

Clicking a card opens `https://claude.ai/code/<session_id>` in a new tab. Your browser's
existing claude.ai sign-in authenticates it, so the page itself stores no tokens.

## Data

The page reads `sessions.json` next to `index.html` and re-fetches it every 60 seconds.
If that file is missing, it shows `sessions.sample.json` with a banner.

Accepted shapes:

```json
{ "generated_at": "2026-11-26T00:00:00Z", "sessions": [ { "id": "session_…", "title": "…", "session_status": "SESSION_STATUS_IDLE", "status_bucket": "SESSION_STATUS_BUCKET_BLOCKED", "updated_at": "…", "post_turn_summary": { "needs_action": "…", "recent_action": "…" }, "unread": true, "environment_kind": "bridge" } ] }
```

A raw `list_sessions` result (`{"data":[…]}` or `{"ccr":{"data":[…]}}`) also works.

## Publishing on GitHub Pages

Settings → Pages → *Deploy from a branch* → pick the branch and `/ (root)`.

> **Privacy:** a GitHub Pages site is public, even when the repository is private.
> A committed `sessions.json` exposes your session titles and summaries to anyone with the URL.
