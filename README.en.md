# Pi Token Analytics

[简体中文](README.md)

A standalone HTML dashboard for analyzing Pi session token usage and cost.

## Features

- Reads JSONL session files from `~/.pi/agent/sessions` locally in the browser
- Chinese / English interface switching with the last choice remembered
- Daily and monthly reports for Input, Output, Cache Read, Cache Write, and Total Tokens
- Quick queries for all data, 1 day, 3 days, 7 days, 30 days, and 90 days
- Breakdown by provider channel and model
- Session and conversation inspection, including assistant messages, tool calls, compaction, and branch summaries
- No npm dependency and no build step

## Run

No npm, build step, or local server is required. Open `index.html` directly.

Choose the `~/.pi/agent/sessions` directory in the page and click **Calculate**. All data is processed locally in the browser and is never uploaded.

## Accounting rules

```text
Total Tokens = input + output + cacheRead + cacheWrite
```

Cost is read directly from `usage.cost.total`. Usage saved in tool results, context compaction, and branch summaries is included in overall totals, but is not mixed into the provider/model assistant breakdown.

The UI is styled with daisyUI and loaded from CDN; npm is not required.
