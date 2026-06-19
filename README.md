# AI 新闻报通

一个基于 n8n、飞书多维表格和大模型的 AI 新闻收集与每日简报工作流模板。项目包含两个脱敏后的 n8n workflow：一个负责收集和整理 AI 新闻，一个负责结合飞书数据与 AI Agent 生成并推送简报。

## 功能说明

- 定时读取 AI 新闻来源并整理为结构化记录。
- 使用大模型对新闻内容做摘要和格式化。
- 写入飞书多维表格，供后续查询和复用。
- AI Agent 可查询新闻记录与飞书日程，生成面向“老师”的每日简报。
- 通过 HTTP Request 推送飞书卡片消息。

## 项目结构

```text
.
├─ README.md
├─ .gitignore
├─ .env.example
├─ workflows/
│  ├─ ai-news-collector.workflow.template.json
│  └─ feishu-ai-news-agent.workflow.template.json
├─ docs/
│  ├─ setup.md
│  └─ security-checklist.md
├─ examples/
│  └─ feishu-card-output-example.md
├─ prompts/
│  └─ agent-prompt.md
└─ backups/
   └─ original/
```

## 使用方法

1. 复制 `.env.example` 中的变量名，在自己的 n8n 或部署环境中配置真实值。
2. 将 `workflows/` 下的两个 `*.template.json` 文件分别导入 n8n。
3. 在 n8n 中重新绑定 DeepSeek/OpenAI 等模型服务凭据。
4. 在 n8n 中重新绑定飞书应用凭据，并替换飞书多维表格参数。
5. 按需启用 Schedule Trigger，先手动测试，再激活 workflow。

## n8n 导入方式

进入 n8n 后选择 **Import from File**，导入：

- `workflows/ai-news-collector.workflow.template.json`
- `workflows/feishu-ai-news-agent.workflow.template.json`

导入后凭据会失效，这是脱敏模板的预期行为。请在每个需要凭据的节点中重新选择或创建自己的 n8n credentials。

## 需要自行配置的凭据

- 模型服务 API Key，例如 OpenAI 或 DeepSeek。
- 飞书自建应用的 App ID 和 App Secret。
- 飞书多维表格 app token、table id、view id。
- 飞书机器人或 Webhook URL。
- n8n 自身的 `N8N_ENCRYPTION_KEY` 和部署参数。

## 飞书配置说明

请在飞书开放平台创建自建应用，并按需开通多维表格、日历和消息相关权限。配置完成后，在 n8n 中创建飞书凭据，并将 workflow 中的占位符替换为自己的飞书多维表格参数。

## 环境变量说明

本仓库只提供 `.env.example`，不要提交真实 `.env`。实际部署时请在 n8n、Docker、服务器环境变量或密钥管理服务中配置真实值。

## 安全注意事项

- 不要提交真实 API Key、token、Webhook URL 或 Cookie。
- 不要提交 n8n 的 `database.sqlite`、`credentials.json` 或本地 `.n8n/` 目录。
- 不建议把 `backups/original/` 上传到 GitHub，它只用于本地留档。
- 上传前请逐项检查 `docs/security-checklist.md`。

## 免责声明

本项目仅作为 n8n workflow 模板和自动化示例。请自行确认新闻来源、模型输出、飞书权限和数据合规要求。由使用者自行承担部署、运行和公开分享所产生的风险。
