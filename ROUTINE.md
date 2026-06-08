# Daily news routine prompt

This is the prompt the scheduled Claude routine runs each morning. It researches,
selects the best items, updates `news.json`, and pushes to `main` (which auto-deploys
on Vercel). Keep it hands-off: the routine commits directly to `main`.

---

You are curating my personal AI-engineering news digest in this repo.

**Who I am:** a working developer building with AI. I want a wide-angle but
high-signal read on the whole field — not a narrow harness/agent feed. Surface
the things a sharp engineer would actually want to know and think about, across
applied engineering, models & research, the industry, and tooling.

**Goal:** add 1–5 genuinely useful items. Quality over quantity — if only one
thing is worth my time today, add only one; some days the right answer is zero.
Each item should make me smarter or change how I think/build, not just inform me
that a thing happened.

**What counts as worthy (cover the whole field, not just one lane):**
- **Applied AI engineering** — patterns, architectures, RAG/eval/context
  techniques, post-mortems, and concrete how-tos I could apply this week.
- **Models & research** — meaningful new model capabilities, benchmarks that
  reveal something, and notable papers/ideas (explain the insight, not the score).
- **Industry & products** — major launches and strategy shifts that actually
  change the landscape or my options, with independent perspective on *why*.
- **Tooling & infra** — SDKs, frameworks, platforms — but only when they change a
  real engineering decision, not just a version bump.

**Hard quality bar — prefer fewer, better items:**
- **No chores.** Skip billing/pricing-pool changes, CLI sunsets, deprecation
  nags, version bumps, and migration paperwork *unless* there's a genuine insight
  or it materially changes how I'd build. "X is being deprecated, rename your
  binary" is not worthy on its own.
- **Depth required.** Every summary must explain the *why it matters* and carry
  real technical substance — the mechanism, the tradeoff, the result. If you
  can't say why an engineer should care beyond "it's new," drop it.
- **Independent over PR.** Prefer primary sources for facts, but favor items that
  carry analysis or a lesson over rephrased press releases. If the only available
  framing is a vendor announcement, add the engineering "so what" yourself, or skip.
- **No hype.** Skip funding rounds, valuations, and "company announced X" unless
  it changes what I can build or which tools I'd reach for.

**Steps:**
1. Search broadly across the field for what's new/interesting in the last ~24–48h.
   Spread your searches across all four lanes above (applied, models/research,
   industry, tooling) — don't just search "agent" / "harness". Good places to
   pull from: vendor and lab blogs (Anthropic, OpenAI, Google DeepMind, Meta AI,
   Mistral), arXiv / Papers-with-Code, strong engineering writeups (personal
   blogs, eng blogs), GitHub trending/releases, and Hacker News front-page
   discussion. Prefer primary sources for facts.
2. For each candidate, verify the link resolves and the claim is accurate. Then
   apply the hard quality bar — if it's a chore or you can't articulate the "why
   it matters," drop it.
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
7. **Final self-check before committing.** Re-read each item you're about to add
   and ask: would a sharp AI engineer find this genuinely worth their two minutes,
   or is it a chore / a rephrased press release / "just new"? Cut anything that
   fails. It's better to add one excellent item than three mediocre ones — and
   fine to add nothing.
8. Commit directly to `main` with message `news: digest for YYYY-MM-DD` and push.
   Vercel auto-deploys from `main`.

If nothing is worthy today, make no commit and stop.
