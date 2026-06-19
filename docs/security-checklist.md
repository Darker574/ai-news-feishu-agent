# Security Checklist

上传 GitHub 前请逐项人工确认：

- [ ] 已删除或清空所有 `credentials`。
- [ ] 已删除 `pinData`。
- [ ] 已删除或替换真实 token。
- [ ] 已删除或替换真实 webhook。
- [ ] 已删除真实个人日程。
- [ ] 已删除真实 API Key。
- [ ] 没有上传 `.env`。
- [ ] 没有上传 n8n `database.sqlite`。
- [ ] 没有上传 `credentials.json`。
- [ ] 没有上传 `backups/original/`。
- [ ] `workflows/` 中只包含脱敏后的 template JSON。
- [ ] README、docs 和 examples 中没有真实个人数据。
