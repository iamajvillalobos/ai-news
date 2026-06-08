# AI Engineering Daily

A personal, auto-updating news aggregator for AI &amp; harness engineering. Each day a
Claude routine picks 1–5 worthy items, commits them to `main`, and Vercel auto-deploys
the static page.

```
Daily Claude routine ──▶ commit news.json to main ──▶ Vercel auto-deploy ──▶ live site
```

## Files

| File          | Purpose                                                        |
|---------------|---------------------------------------------------------------|
| `index.html`  | Static page; fetches `news.json` and renders it. No build step. |
| `news.json`   | The data. Newest items first; the page groups by date.        |
| `vercel.json` | Vercel config (clean URLs, no-cache header on `news.json`).   |
| `ROUTINE.md`  | The prompt the daily routine runs.                            |

## Run locally

It's just static files:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Deploy to Vercel

1. Push this repo to GitHub.
2. In Vercel: **Add New → Project → import this repo**. Framework preset: **Other**
   (no build command, output dir = root). Deploy.
3. Vercel now redeploys on every push to `main`.

## The daily automation

Set up a scheduled Claude Code routine that runs `ROUTINE.md` each morning. From
Claude Code:

```
/schedule
```

Point it at the prompt in `ROUTINE.md`, daily, committing directly to `main`.
Because Vercel watches `main`, the merge *is* the deploy — fully hands-off.

## Editing by hand

Add or tweak items directly in `news.json` and push. Same schema as in `ROUTINE.md`.
