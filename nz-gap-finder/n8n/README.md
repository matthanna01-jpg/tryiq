# NZ Gap Finder — n8n workflow

Runs the same weekly research digest as the Claude Code Routine, but on your
own n8n instance, calling the Claude API directly instead of using a full
Claude Code agent session. Cheaper per run (one API call vs. a multi-tool
agent session) — you pay for Anthropic API usage on your own key instead of
Claude Code credits.

## Import

In n8n: **Workflows → Import from File** → select `nz-gap-finder-workflow.json`.

## What it does

1. **Weekly Schedule** — fires Monday 8am (Pacific/Auckland). Edit the cron
   expression on the trigger node to change cadence.
2. **Claude: Research + Write Digest** — a single call to the Claude API
   (`claude-opus-4-8`) with the native `web_search` tool enabled. Claude
   searches the web itself (up to 15 searches) and writes the full digest in
   one response — no separate search API/key needed.
3. **Extract Report Text** — pulls the markdown out of Claude's response.
4. **Commit Report to GitHub** — pushes `nz-gap-finder/reports/<date>.md` to
   the `claude/nz-market-gap-finder-4tdwxh` branch of `matthanna01-jpg/tryiq`.
5. **Email Me the Digest** — sends the full report to your inbox.

## Credentials to set up in n8n (Settings → Credentials)

| Credential | Type | Used for |
|---|---|---|
| Anthropic API key | **Header Auth** — header name `x-api-key`, value your Anthropic API key | Calling the Claude API |
| GitHub account | **GitHub API** — a PAT with `repo` scope on `matthanna01-jpg/tryiq` | Committing the report |
| SMTP account | **SMTP** (or swap the last node for the Gmail node if you prefer OAuth) | Emailing the digest |

After importing, open each node with a `REPLACE_WITH_...` placeholder and
point it at the credential you created, and set the `fromEmail` on the email
node to whatever address your SMTP account sends as.

## Cost

Each run is one Claude API call with web search — a few cents to low tens of
cents per week depending on how much searching Claude does, billed to your
own Anthropic API key. This replaces the Claude Code Routine, which billed to
Claude Code usage instead.

## Notes / limitations vs. the Claude Code version

- Doesn't read prior weeks' reports before writing a new one (the Claude Code
  Routine did), so it won't explicitly say "promoted to High confidence since
  last week" — it just researches fresh each time. Could be added later with
  a GitHub "Get file" node reading the most recent report first.
- Web search runs server-side inside the one API call (up to 10 automatic
  search rounds); if Claude needs more than that it will stop with output so
  far rather than erroring.
