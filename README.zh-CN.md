# NoFable Chat

中文 | [English](README.md)

NoFable Chat 是一个单文件、纯前端的多模型聚合聊天页面。它可以同时调用多行 OpenAI-compatible Chat Completions API，把参考模型的回答交给聚合模型生成最终答案，并可选接入 Firecrawl 做网页搜索。

## 功能

- 多模型并发参考回答
- 聚合模型生成最终答案
- 支持流式输出
- 支持展示或隐藏中间参考层
- 支持推理内容 `reasoning_content` 展示
- 可选 Firecrawl 网页搜索工具
- 本地浏览器保存对话历史
- 中英文界面自动切换

## 使用方式

直接打开 `index.html` 即可使用。部署到 GitHub Pages 后，访问站点首页即可进入应用。

首次使用时，在左侧设置里配置每个模型：

- `baseUrl`：兼容 OpenAI Chat Completions 的接口地址，通常以 `/chat/completions` 结尾
- `apiKey`：对应服务商的 API Key
- `model`：模型名称
- `思考`：用于支持 `reasoning_content` 的推理模型
- `搜索`：允许该模型调用 Firecrawl 搜索工具
- `聚合`：选择最终汇总答案使用的模型

如果只想使用部分模型，可以删除不需要的模型行；发送前每一行都需要填完整。

## GitHub Pages 部署

1. 将 `index.html`、`README.md`、`README.zh-CN.md` 提交到 GitHub 仓库。
2. 进入仓库 `Settings` -> `Pages`。
3. `Build and deployment` 选择 `Deploy from a branch`。
4. 选择发布分支和根目录，例如 `main` / `/ (root)`。
5. 保存后等待 GitHub Pages 生成访问地址。

## 安全说明

仓库中没有硬编码真实 API Key。为了方便刷新页面后继续使用，页面会把用户输入的模型 API Key 和 Firecrawl Key 保存到当前浏览器的 `localStorage`。

由于这是纯前端应用，API Key 会存放在浏览器本地，并由浏览器直接发送到对应模型服务商。任何同源脚本、浏览器扩展、被污染的第三方依赖、XSS 或能访问你浏览器本地数据的人都可能读取这些 Key。多人公开使用或生产环境建议增加后端代理，不要把共享 Key 放在前端。若需要清除 Key，可在页面设置里删除内容后触发保存，或清理该站点的浏览器数据。

页面使用 jsDelivr 加载 `marked` 和 `DOMPurify`，已固定版本并添加 SRI 校验。若需要更严格的供应链控制，可以把这两个依赖下载到仓库本地并改为本地引用。

## 限制

- GitHub Pages 只能托管静态文件，不能隐藏服务端密钥。
- 模型服务商必须允许浏览器跨域调用，否则会遇到 CORS 错误。
- API Key 和对话历史保存在当前浏览器的 `localStorage` 中，不会同步到云端。
- 网页搜索需要用户自己提供 Firecrawl API Key。

## 许可证

发布前请根据你的使用计划补充许可证文件。
