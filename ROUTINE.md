# Daily news routine prompt

This is the prompt the scheduled Claude routine runs each morning. It researches,
selects the best items, updates `news.json`, and pushes to `main` (which auto-deploys
on Vercel). Keep it hands-off: the routine commits directly to `main`.

---

You are curating my personal AI-engineering news digest in this repo.

**Goal:** add 1–5 genuinely useful items for a working developer focused on AI
engineering and harness/agent engineering. Quality over quantity — if there is
only one thing worth my time today, add only one. Skip hype, funding rounds, and
generic "company announced X" PR unless it changes how I'd build something.

**What counts as worthy:**
- New/updated models, APIs, SDKs, or pricing that change practical engineering decisions
- Agent/harness tooling, eval frameworks, context-management techniques
- Notable open-source releases, benchmarks, or post-mortems with real lessons
- Concrete how-to / pattern writeups I could apply this week

**Steps:**
1. Use web search to find what's new in the last ~24–48h. Prefer primary sources
   (vendor blogs, docs, GitHub releases) over aggregators.
2. For each item, verify the link resolves and the claim is accurate.
3. De-dupe against existing entries in `news.json` (match on `url` and `title`).
4. Prepend new items to the `items` array. Set `updated` to today's date (YYYY-MM-DD).
5. Each item must follow this schema:
   ```json
   {
     "id": "YYYY-MM-DD-short-slug",
     "date": "YYYY-MM-DD",
     "title": "Concise, specific headline",
     "summary": "2–3 sentences: what it is and why it matters to me as a developer.",
     "url": "https://primary-source",
     "source": "Publisher or repo",
     "tags": ["models", "harness", "agents", "evals", "..."]
   }
   ```
6. Validate that `news.json` is still valid JSON.
7. Commit directly to `main` with message `news: digest for YYYY-MM-DD` and push.
   Vercel auto-deploys from `main`.

If nothing is worthy today, make no commit and stop.
