# AI Opportunity Scout (n8n)

Runs locally in your n8n, twice a day (8am / 6pm by default), checks Hacker News,
arXiv (cs.AI), GitHub Trending, Product Hunt, and r/MachineLearning for anything
recent that matches build/opportunity keywords, and emails you a digest — only
if it actually finds something. No hits, no email.

## Import

1. Open your local n8n → **Workflows** → **Import from File**.
2. Select `ai-opportunity-scout.json`.
3. Open the **Send Digest Email** node and set your SMTP credentials
   (Gmail: use an [app password](https://myaccount.google.com/apppasswords),
   host `smtp.gmail.com`, port `465`, SSL on).
4. Click **Execute Workflow** once to test end-to-end (you may get 0 or 1 emails
   depending on what's currently trending — that's expected).
5. Toggle the workflow **Active** in the top right.

## Tuning

- **Schedule**: edit the `Schedule Trigger` node's cron expression
  (`0 8,18 * * *` = 8am and 6pm daily, server/machine local time).
- **Sources**: add/remove RSS nodes and wire them into the `Merge` chain the
  same way the existing ones are wired.
- **Keywords / strictness**: edit `KEYWORDS` and the `score >= 2` threshold in
  the `Filter & Score` code node. Raise the threshold for fewer, higher-bar
  alerts; lower it to catch more.
- **Lookback window**: `LOOKBACK_HOURS` in `Filter & Score` — currently 14h to
  safely cover the 12h gap between runs without double-reporting old items.

## Notes

- r/MachineLearning's RSS occasionally rate-limits anonymous requests; if that
  node starts failing, add a `User-Agent` header via an HTTP Request node
  instead of RSS Feed Read, or drop it from the merge chain.
- This has no memory between runs, so an item that's still trending 12h later
  can show up twice. If that gets annoying, add a Code/Set node that writes
  seen links to a local file or a small SQLite/Postgres table and filters
  against it.
