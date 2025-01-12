## 🚀 Deploy NotionNext-starter

[中文文档](./README.md) | README in English

NotionNext-starter supports multiple deployment platforms. You can choose from two deployment methods for each platform:

### Deploy to Vercel

#### Method 1: One-Click Deployment (Manual Updates)
[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/blog-starter/notionNext-starter&repository-name=my-notion-blog&env=NOTION_PAGE_ID)

> - Click the button above for one-click deployment to Vercel. You'll need to connect your GitHub account and set the `NOTION_PAGE_ID` environment variable
> - With one-click deployment, when Notion content is updated, you need to manually trigger a redeployment in the Vercel dashboard to update the website content

#### Method 2: Automatic Deployment (Recommended)
For automatic deployment with GitHub Actions, see the [Vercel Deployment Guide](./docs/VERCEL.md).

> **Automatic Deployment Benefits**:
> - ✨ Automatic updates twice daily at 8 AM and 8 PM (UTC 0:00 and 12:00)
> - ✨ Automatic deployment of main branch updates
> - ✨ Automatic preview deployments for Pull Requests
> - ✨ Automatic deployment status comments on PRs and commits

### Deploy to Netlify

#### Method 1: One-Click Deployment (Manual Updates)
[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/blog-starter/notionNext-starter)

> - Click the button above for one-click deployment to Netlify. You'll need to connect your GitHub account and set the `NOTION_PAGE_ID` environment variable
> - With one-click deployment, when Notion content is updated, you need to manually trigger a redeployment in the Netlify dashboard to update the website content

#### Method 2: Automatic Deployment (Recommended)
You need to complete one-click deployment first to get NETLIFY_SITE_ID, then configure GitHub Actions for automatic deployment. See the [Netlify Deployment Guide](./docs/NETLIFY.md) for details.

> **Automatic Deployment Benefits**:
> - ✨ Automatic updates twice daily at 8 AM and 8 PM (UTC 0:00 and 12:00)
> - ✨ Automatic deployment of main branch updates
> - ✨ Automatic preview deployments for Pull Requests
> - ✨ Automatic deployment status comments on PRs and commits

### Environment Variables

All deployment methods require the following basic environment variables:

```bash
NOTION_PAGE_ID         # Your Notion page ID (Required)
NEXT_PUBLIC_THEME      # Theme, default 'simple'
NEXT_PUBLIC_LANG       # Language, default 'zh-CN'
NEXT_PUBLIC_AUTHOR     # Author name
NEXT_PUBLIC_LINK       # Website URL
```

> Note: If optional environment variables are not configured, default values from blog.config.js will be used. It's recommended to at least configure the required variables.

[fork]: https://github.com/blog-starter/notionNext-starter/fork
[pr]: https://github.com/blog-starter/notionNext-starter/compare


