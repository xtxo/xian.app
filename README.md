# XIAN.APP Public Catalog

仙点（[XIAN.APP](https://xian.app)）公开应用数据镜像。

这个仓库只同步已经在 XIAN.APP 审核通过并公开展示的应用信息，方便开发者、Agent、脚本和第三方项目直接读取。

> **Source of truth:** https://xian.app  
> 本仓库是公开数据镜像，不包含站点源码、后台数据或用户隐私信息。

## 数据

| 文件 | 说明 |
| --- | --- |
| `data/apps.json` | 已审核公开应用的完整机器可读快照 |
| `data/categories.json` | XIAN.APP 当前公开分类字典 |
| `schema/catalog.schema.json` | `apps.json` 的 JSON Schema |

当前快照：**18 个公开应用**  
首次同步：**2026-09-01**

## 公开字段

每个应用只保留公开展示所需的信息：

- `id`：XIAN.APP 应用 ID
- `name` / `tagline` / `description`
- `website_url` / `open_source_url`
- `xian_url`：XIAN.APP 详情页
- `creator.name` / `creator.avatar_url`
- `categories`
- `cover_image` / `screenshots`
- `created_at` / `updated_at`

不会同步邮箱、登录信息、审核信息、后台配置、内部账号关联字段等数据。

## 图片策略

图片不复制到 Git 仓库中。`apps.json` 只保存现有公开图片 URL，主要指向 XIAN.APP 的 Cloudflare R2 公共资源。

这样可以避免仓库被大量二进制图片撑大，也方便站点继续统一管理图片压缩、替换和 CDN。

## 同步策略

XIAN.APP / Supabase 仍然是主数据源。这个仓库只做公开快照：

1. 应用在 XIAN.APP 提交并审核通过；
2. 从数据库导出公开字段；
3. 更新 `data/apps.json` 和分类数据；
4. 不公开任何仅后台可见的数据。

后续可以增加 GitHub Actions，把同步过程自动化。生成文件如果由自动同步维护，直接手工修改可能会在下一次同步时被覆盖。

## 使用

直接读取 `data/apps.json` 即可构建导航、搜索、统计、Agent 数据源或其他衍生项目。

```js
const catalog = await fetch(
  "https://raw.githubusercontent.com/xtxo/xian.app/main/data/apps.json"
).then((res) => res.json());

console.log(catalog.count, catalog.apps);
```

---

**XIAN.APP · 仙点** — 发现 Vibe Coding 的灵感与作品。
