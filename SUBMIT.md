# 提交产品到 XIAN.APP

你可以通过 Pull Request 向 **XIAN.APP / 仙点** 提交产品。

这个仓库同时面向人工提交和 AI Agent 提交。使用 Codex、Claude Code、Cursor 等 Agent 时，可以直接让它阅读仓库根目录的 `AGENTS.md` 并按要求完成投稿。

## 最简单的提交方式

为你的产品新建一个独立目录：

```text
apps/<slug>/
├── app.json
└── images/
    ├── cover.webp
    ├── 01.webp
    └── 02.webp
```

例如：

```text
apps/my-awesome-agent/
├── app.json
└── images/
    ├── cover.webp
    └── 01.webp
```

不要直接修改 `data/apps.json`，它是 XIAN.APP 公开数据的自动生成快照。

## app.json 示例

```json
{
  "schema_version": "1.0",
  "name": "My Awesome Agent",
  "tagline": "一句话说明它解决什么问题",
  "description": "用客观、清楚的语言介绍产品做什么、适合谁使用，以及最主要的功能。",
  "website_url": "https://example.com",
  "open_source_url": "https://github.com/example/project",
  "creator": {
    "name": "Creator Name",
    "url": "https://example.com"
  },
  "categories": ["dev-tools"],
  "images": {
    "cover": "images/cover.webp",
    "screenshots": ["images/01.webp"]
  },
  "submitted_via": "github"
}
```

完整机器可读规则见：`schema/submission.schema.json`。

当前分类 slug 请查看：`data/categories.json`。

## 图片

**建议把图片一起提交。** 这样一个 PR 就包含完整产品资料，XIAN.APP 后台可以直接读取并同步，不依赖第三方图床。

建议：

- 优先 WebP；
- 封面建议横图，4:3 或 16:10；
- 最多 4 张截图；
- 单张建议小于 800 KB；
- 单张不得超过 1.5 MB；
- 不提交 GIF、视频或大量无关素材。

产品被收录后，XIAN.APP 可以把图片复制到自己的 Cloudflare R2/CDN。GitHub 中的图片主要作为**投稿原始材料和可追溯记录**，站点不必长期依赖 GitHub Raw 做生产图床。

## 为什么每个产品一个目录

这样做有几个好处：

- 每个 PR 基本只动一个目录，冲突非常少；
- 图片、文字、链接天然绑定在一起；
- Agent 很容易自动生成；
- XIAN.APP 可以监听 `apps/**/app.json`，只导入新增或变化的产品；
- 不需要每次重新解析一个越来越大的总 JSON 文件。

## Pull Request

PR 标题请使用：

```text
submit: 产品名称
```

审核通过并合并后，XIAN.APP 会以仓库中的产品目录作为导入来源。

如果你使用 AI Agent，可以直接告诉它：

> Read AGENTS.md and submit this product to XIAN.APP following the repository rules.
