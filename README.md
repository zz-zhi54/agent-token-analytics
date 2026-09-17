# Agent Token Analytics

[English](README.en.md)

一个纯 HTML 的 Agent 工具会话 Token 使用情况分析页面。当前支持 Pi 与 DSH，并可继续扩展 Codex 等工具。

## 功能

- 在浏览器本地读取 `~/.pi/agent/sessions` 下的 Pi JSONL，以及 `~/.dsh/sessions` 下的 DSH JSONL / `.jsonl.zstd` 会话文件
- 支持中文 / English 界面切换，并记住上次选择
- 按天、按月统计 Input、Output、Cache Read、Cache Write 和总 Token
- 支持全部、1 天、3 天、7 天、30 天、90 天快速查询
- 按渠道 / 模型展示四类 Token、调用次数和费用
- 查看 session 中的用户消息、Assistant 回复、工具调用和摘要

## 运行

项目不需要 npm、构建步骤或本地服务器，直接打开 `index.html` 即可。

在页面中选择 `~/.pi/agent/sessions` 或 `~/.dsh/sessions` 目录，再点击“开始计算”。数据只在浏览器本地处理，不会上传。DSH 默认的 `.jsonl.zstd` 使用页面加载的 Zstandard 解码器读取；检测到 DSH 会话时会从 `models.dev` 加载价格目录。

## 统计口径

```text
总 Token = DSH 提供有效 totalTokens 时使用它，否则为 input + output + cacheRead + cacheWrite
```

费用优先使用会话中保存的 `usage.cost.total`；DSH 没有持久费用时，根据 `models.dev` 的 provider/model 价格和四类 Token 估算（价格单位为 USD / 百万 Token，并处理长上下文价格层级）。DSH 的 `assistant/message` 和 `assistant/attempt` 使用 `inputTokens`、`outputTokens`、`cacheReadTokens`、`cacheWriteTokens` 与 `totalTokens` 字段，重试 attempt 只读取最后一条 usage。无法匹配价格的模型会提示，费用显示为 0。

页面从 jsDelivr 加载 MIT 许可的 `fzstd`，仅用于在浏览器本地解压 DSH 的 `.jsonl.zstd` 文件。
