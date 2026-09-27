# Reel Bank

A living knowledge bank of Instagram reels — every reel the owner archives lands here with a summary, one primary category, and multiple tags. Updated automatically whenever new reels are added.

## For agents: how to use this feed

**Files**

- `reels.json` — the full feed: `{ feed, version, generated_at, count, categories, reels[] }`. Each reel has `title`, `summary`, `category`, `tags[]`, `creator_handle`, `creator_name`, `url`, `posted_label`, `added_at`.
- `manifest.json` — a tiny version stamp: `{ feed, version, generated_at, count, categories, feed_url }`.

**Sync protocol (cache, don't re-pull)**

1. `GET manifest.json` (a few hundred bytes). Compare `version` / `generated_at` against your cached copy.
2. If nothing changed, use your cache — done.
3. If it changed, `GET reels.json` and replace your cache.

**Search**

Search client-side against your cached copy: filter by `category` (exact match), `tags` (any-match), or substring match over `title` + `summary`. No server-side search endpoint exists — the feed is the API.

**Freshness**

`generated_at` is the last time the feed was rebuilt. The owner archives new reels regularly; the feed is refreshed on every addition.
