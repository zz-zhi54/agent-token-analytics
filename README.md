# Pi Token Analytics

[English](README.en.md)

一个纯 HTML 的 Pi 会话 Token 使用情况分析页面。

## 功能

- 在浏览器本地读取 `~/.pi/agent/sessions` 下的 JSONL 会话文件
- 支持中文 / English 界面切换，并记住上次选择
- 按天、按月统计 Input、Output、Cache Read、Cache Write 和总 Token
- 支持全部、1 天、3 天、7 天、30 天、90 天快速查询
- 按渠道 / 模型展示四类 Token、调用次数和费用
- 查看 session 中的用户消息、Assistant 回复、工具调用和摘要

## 运行

项目不需要 npm、构建步骤或本地服务器，直接打开 `index.html` 即可。

在页面中选择 `~/.pi/agent/sessions` 目录，再点击“开始计算”。数据只在浏览器本地处理，不会上传。

## 统计口径

```text
总 Token = input + output + cacheRead + cacheWrite
```

费用直接使用 Pi 会话中保存的 `usage.cost.total`。工具结果、上下文压缩和分支摘要中保存的 usage 会计入总体统计，但不会混入渠道 / 模型的 Assistant 明细。
