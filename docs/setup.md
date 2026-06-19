# Setup

## 1. 导入 n8n workflow JSON

在 n8n 中进入 workflow 列表，选择 **Import from File**，分别导入 `workflows/ai-news-collector.workflow.template.json` 和 `workflows/feishu-ai-news-agent.workflow.template.json`。

## 2. 重新配置 n8n credentials

模板中的凭据已经被清空。导入后请逐个打开 DeepSeek/OpenAI、飞书节点和 HTTP Request 节点，重新选择你自己的 n8n credentials。

## 3. 配置飞书应用权限

在飞书开放平台创建自建应用，配置 App ID、App Secret，并按实际使用范围开通多维表格、日历、消息或机器人相关权限。权限变更后记得发布应用版本或重新安装应用。

## 4. 配置飞书多维表格参数

在飞书多维表格中确认 base app token、table id、view id 和字段名称。将 workflow 中的占位符替换为你自己的值，并确认字段类型与节点 body 中的数据结构匹配。

## 5. 配置模型 API Key

在 n8n credentials 中配置 DeepSeek、OpenAI 或其他模型服务 API Key。不要把真实 API Key 写入 workflow JSON 或提交到 Git。

## 6. 测试运行

先手动执行新闻收集 workflow，确认可以读取 RSS、生成摘要并写入测试表。再手动执行 AI Agent workflow，确认它能查询表格、查询日历并生成飞书卡片内容。

## 7. 发布和激活 workflow

测试通过后，检查 Schedule Trigger 的时区和触发时间。确认无误后再打开 workflow 的 Active 开关。

## 常见问题

### 为什么导入后凭据失效？

这是正常现象。模板已经删除 n8n credentials id 和 name，导入后必须重新绑定你自己的凭据。

### 为什么飞书节点报 403？

常见原因是飞书应用权限不足、应用未发布、未安装到目标租户、多维表格未授权给应用，或 app token/table id 填写错误。

### 为什么 HTTP Request 报 authorization 错误？

请检查 Webhook URL、Authorization header、机器人签名、token 或飞书应用访问令牌是否配置正确。不要直接在仓库中保存真实值。

### 为什么 Schedule Trigger 测试能跑但定时不跑？

请检查 workflow 是否已激活、n8n 服务是否持续运行、服务器时区是否正确，以及 n8n 的队列或 worker 是否正常。
