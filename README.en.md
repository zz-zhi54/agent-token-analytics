# Agent Token Analytics

[简体中文](README.md)

A standalone HTML dashboard for analyzing token usage and cost across Agent tools. It currently supports Pi and DSH, with room for Codex and other tools.

## Features

- Reads Pi JSONL sessions from `~/.pi/agent/sessions` and DSH JSONL / `.jsonl.zstd` sessions from `~/.dsh/sessions` locally in the browser
- Chinese / English interface switching with the last choice remembered
- Daily and monthly reports for Input, Output, Cache Read, Cache Write, and Total Tokens
- Quick queries for all data, 1 day, 3 days, 7 days, 30 days, and 90 days
- Breakdown by provider channel and model
- Session and conversation inspection, including assistant messages, tool calls, compaction, and branch summaries
- No npm dependency and no build step

## Run

No npm, build step, or local server is required. Open `index.html` directly.

Choose the `~/.pi/agent/sessions` or `~/.dsh/sessions` directory in the page and click **Calculate**. All data is processed locally in the browser and is never uploaded. DSH's default `.jsonl.zstd` files are decoded by the page's loaded Zstandard decoder; when DSH sessions are detected, the page loads its pricing catalog from `models.dev`.

## Accounting rules

```text
Total Tokens = DSH totalTokens when valid; otherwise input + output + cacheRead + cacheWrite
```

Cost is read first from the persisted `usage.cost.total`. When DSH has no persisted cost, the page estimates it from the `models.dev` provider/model price and the four token buckets (USD per million tokens, including long-context tiers). Unmatched models are reported and shown as 0 cost. DSH assistant messages and retry-only attempts use `inputTokens`, `outputTokens`, `cacheReadTokens`, `cacheWriteTokens`, and `totalTokens`; only the last usage chunk in an attempt is counted.

The page loads the MIT-licensed `fzstd` decoder from jsDelivr solely to decompress DSH `.jsonl.zstd` files locally in the browser.

The UI is styled with daisyUI and loaded from CDN; npm is not required.
