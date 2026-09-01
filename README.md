# XIAN.APP Public Catalog

仙点（[XIAN.APP](https://xian.app)）的公开产品目录与 GitHub 投稿入口。

这里既提供 XIAN.APP 已收录产品的机器可读数据，也接受开发者和 AI Agent 通过 Pull Request 提交新产品。

> **Website:** https://xian.app  
> 本仓库不包含站点源码、后台数据、登录信息或用户隐私数据。

## 两种数据

| 路径 | 用途 |
| --- | --- |
| `apps/<slug>/app.json` | 一个产品一份投稿数据，适合人工或 Agent 提 PR |
| `apps/<slug>/images/` | 投稿时附带的封面和截图 |
| `data/apps.json` | XIAN.APP 已公开产品的机器可读聚合快照 |
| `data/categories.json` | 当前公开分类字典 |
| `schema/submission.schema.json` | GitHub 投稿格式 Schema |
| `schema/catalog.schema.json` | 聚合目录 Schema |
| `AGENTS.md` | 给 Codex、Claude Code、Cursor 等 Agent 的投稿协议 |
| `SUBMIT.md` | 给人的投稿说明 |

当前公开快照：**18 个产品**。

## 提交你的产品

新产品不要直接修改 `data/apps.json`。

请新建：

```text
apps/my-product/
├── app.json
└── images/
    ├── cover.webp
    ├── 01.webp
    └── 02.webp
```

然后发起 Pull Request：

```text
submit: My Product
```

完整规则见 [`SUBMIT.md`](./SUBMIT.md)。

如果你正在使用 AI Agent，可以直接告诉它：

> Read AGENTS.md and submit this product to XIAN.APP following the repository rules.

## 图片策略

**GitHub 投稿允许并推荐把图片一起提交。**

这样每个 PR 本身就是一份完整、可追溯的产品资料，XIAN.APP 在导入时不需要依赖临时第三方图床。

为了避免仓库长期被二进制资源撑大：

- 优先 WebP；
- 最多 1 张封面 + 4 张截图；
- 单张建议小于 800 KB，最大 1.5 MB；
- 产品被 XIAN.APP 导入后，生产环境图片可以复制到 Cloudflare R2/CDN；
- GitHub 中的图片是投稿来源，不建议让网站长期直接使用 GitHub Raw 作为生产图床。

对于已经由 XIAN.APP 收录并同步到 `data/apps.json` 的旧产品，图片 URL 仍可能直接指向现有 R2/CDN。

## 推荐同步流程

```text
开发者 / Agent
      ↓
Pull Request
      ↓
人工审核并 Merge
      ↓
GitHub merge webhook / Action
      ↓
XIAN.APP Import API
      ↓
校验 app.json
      ↓
复制图片到 R2
      ↓
写入 Supabase
      ↓
刷新 data/apps.json
```

这样 **Merge 本身就可以代表“审核通过”**。站点只需要处理被合并到 `main` 的 `apps/**/app.json`，不用扫描所有 PR，也不用频繁全量同步。

## 公开字段

公开目录只保留产品展示所需信息，例如：

- 产品名称、简介、描述；
- 官网和开源地址；
- 创作者公开名称；
- 分类；
- 封面和截图；
- XIAN.APP 产品页；
- 创建/更新时间。

不会公开邮箱、登录信息、内部用户 ID、审核后台字段、API Key 或其他隐私数据。

## 使用公开目录

```js
const catalog = await fetch(
  "https://raw.githubusercontent.com/xtxo/xian.app/main/data/apps.json"
).then((res) => res.json());

console.log(catalog.count, catalog.apps);
```

---

**XIAN.APP · 仙点** — 发现 Vibe Coding 的灵感与作品。
