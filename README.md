<p align="center">
  <img src="docs/assets/zurenze-banner.svg" alt="祖仁泽热点：看懂 AI 变化，发现值得讲的内容。" width="100%">
</p>

<p align="center">
  <a href="https://github.com/zurenze1">祖仁泽 · zurenze1</a> ·
  <a href="README.en.md">English</a> ·
  <a href="docs/deploy.md">部署说明</a> ·
  <a href="LICENSE">MIT License</a>
</p>

## 少看几条，多懂一点

这是祖仁泽的个人 AI 热点站。关注有实际影响的 AI 动态，保留原始来源和推荐理由，帮助判断一条消息是否值得阅读、尝试或继续讲述。

我关心的是：工具能不能真的用起来，工作方式发生了什么变化，一条消息能不能带来有内容的创作角度。热度是线索，信息价值才是筛选方向。

本项目基于 [AIHOT 开源框架](https://github.com/KKKKhazix/AIHOT) 定制，采集、精选、事件归组和日报引擎来自上游。个人站名、Z 字标、蓝白与深色配色、首页介绍和作者署名属于这个个人版本。

## 这个版本改了什么

| 位置 | 个人版本 |
| --- | --- |
| 网站名称 | 祖仁泽热点 |
| 作者署名 | 祖仁泽 / 祖老大 |
| 首页 | 看懂 AI 变化，发现值得讲的内容 |
| 品牌 | 原创 Z 字标，蓝白配色，保留深色模式 |
| 日报配置 | 每天北京时间 09:00 |
| GitHub | [zurenze1/zurenze-hot](https://github.com/zurenze1/zurenze-hot) |

**当前是完成品牌定制的源码版本。** 日报时间是配置，实际采集、成刊和网站访问需在部署后验证。此仓库不会自动获得原站的运营数据，也不自带完整的抖音、小红书或播客采集适配。当前 Codex 聊天中的每日推送由另一个已配置的定时任务负责。

## 可以做什么

- 从 RSS、网页、JSON 接口等信源收集 AI 动态。
- 用模型预筛、两次评分、生成中文摘要与推荐理由。
- 将同一事件的多篇报道归组，减少重复阅读。
- 生成日报、周报和月报，提供网站、RSS、API 与 MCP 访问。
- 在后台管理信源、模型和预算。

## 本地运行

需要 Node.js 24.11 以上、Docker Compose，以及一个 OpenAI 兼容的模型 API Key。

```bash
git clone https://github.com/zurenze1/zurenze-hot.git
cd zurenze-hot
node scripts/init-env.ts --llm-key <你的模型 API Key>
docker compose up -d --build
```

打开 `http://localhost:3000`；后台地址为 `/admin`。管理员密码保存在本机 `.env` 中，不要提交到 GitHub。启用模型前设置合适的预算。

不用 Docker、配置域名、模型服务或备份，请按 [部署说明](docs/deploy.md) 操作。

## 修改自己的内容

| 文件 | 用途 |
| --- | --- |
| [site/site.ts](site/site.ts) | 站名、作者、页面文案和出刊时间 |
| [site/brand/](site/brand/) | 图标与字标 |
| [industry/sources.json](industry/sources.json) | 示范信源 |
| [industry/prompts/](industry/prompts/) | 精选与写作标准 |
| [industry/selection.ts](industry/selection.ts) | 入选门槛 |
| [docs/customize.md](docs/customize.md) | 完整定制指南 |

原始框架说明保存在 [README.upstream.md](README.upstream.md)，方便后续对照和更新。

## 验证

```bash
npm ci
npm run typecheck
npm run build -w @aihot/web
node --test apps/web/tests/*.test.ts
npm run test:standalone
```

数据库测试需要 PostgreSQL，使用以 `_test` 或 `_ci` 结尾的专用测试库；完整启动后再运行 `node scripts/smoke.ts --base http://localhost:3000`。具体约定见 [AGENTS.md](AGENTS.md)。

## 来源与许可

感谢数字生命卡兹克和 [AIHOT](https://github.com/KKKKhazix/AIHOT) 的开源贡献。保留原始 [MIT 许可证](LICENSE) 与 [第三方许可说明](NOTICE)。本站使用自己的名称和图标；引用新闻的原文版权归各来源所有。
