# XIAN.APP Agent Submission Guide

This repository accepts product submissions from humans and AI agents.

If you are an AI coding agent, follow this file exactly when submitting a new product to XIAN.APP.

## Goal

Create **one new product folder** under:

```text
apps/<slug>/
```

Do not directly edit `data/apps.json`. It is a generated catalog snapshot.

## Required structure

```text
apps/<slug>/
├── app.json
└── images/
    ├── cover.webp
    ├── 01.webp
    └── 02.webp
```

Images are optional except `cover`, which is strongly recommended.

`<slug>` must:

- use lowercase ASCII letters, numbers, and hyphens only;
- be stable and human-readable;
- normally be based on the product name;
- not contain spaces or Chinese characters.

Example: `my-awesome-agent`.

## app.json format

Use this exact shape:

```json
{
  "schema_version": "1.0",
  "name": "Product name",
  "tagline": "One concise sentence describing the product",
  "description": "A factual introduction explaining what it does, who it is for, and its main capabilities.",
  "website_url": "https://example.com",
  "open_source_url": "https://github.com/owner/repo",
  "creator": {
    "name": "Creator name",
    "url": "https://example.com/creator"
  },
  "categories": ["dev-tools"],
  "images": {
    "cover": "images/cover.webp",
    "screenshots": [
      "images/01.webp",
      "images/02.webp"
    ]
  },
  "submitted_via": "github"
}
```

### Field rules

- `schema_version`: always `"1.0"` for now.
- `name`: official product/project name.
- `tagline`: concise; do not use exaggerated marketing claims.
- `description`: factual, preferably 80–500 Chinese characters or equivalent.
- `website_url`: product homepage, demo, store page, or repository URL.
- `open_source_url`: GitHub/GitLab source URL, or `null` if not open source.
- `creator.name`: public creator/team name.
- `creator.url`: creator homepage/social profile, or `null`.
- `categories`: use slugs from `data/categories.json`. Do not invent a category unless necessary.
- `images.cover`: repository-relative path to the cover image, or an HTTPS URL.
- `images.screenshots`: 0–4 repository-relative image paths or HTTPS URLs.
- `submitted_via`: use `"github"` for repository submissions.

Do **not** add internal XIAN.APP IDs, approval status, email addresses, access tokens, API keys, phone numbers, or other private information.

## Image requirements

Repository-hosted images are welcome because they make a Pull Request self-contained and easy to import into XIAN.APP.

Preferred:

- WebP
- PNG/JPEG accepted when conversion is impractical
- cover: landscape, ideally 4:3 or 16:10
- maximum 4 screenshots
- each image should preferably be under 800 KB
- each image must be under 1.5 MB
- avoid animated GIFs and videos
- no unrelated promotional assets

XIAN.APP may copy accepted images to its own CDN/R2 storage during import. The repository copy is the submission source, not necessarily the final production URL.

## Before opening the Pull Request

Check all of the following:

1. Only one new `apps/<slug>/` folder is added for one product submission.
2. `app.json` is valid JSON.
3. Required fields are present.
4. Category slugs exist in `data/categories.json`.
5. Website/source links are valid HTTPS URLs where possible.
6. Image paths exactly match committed files.
7. No secrets or private user information are included.
8. Do not edit generated files such as `data/apps.json`.

## Pull Request title

Use:

```text
submit: <Product Name>
```

## Pull Request body

Include:

```markdown
## Product
- Name: <Product Name>
- Website: <URL>
- Source: <URL or N/A>

## Submission
- [x] app.json follows the XIAN.APP schema
- [x] links were checked
- [x] images are included or externally accessible
- [x] no private information or secrets are included
```

After review and merge, XIAN.APP can automatically import the product and mirror the images to its production CDN.
