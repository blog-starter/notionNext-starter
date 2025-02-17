## 🚀 Deploy NotionNext-starter

[中文文档](./README.md) | README in English

### Prerequisites

Before deployment, you need to:

1. Copy the Notion database template:
   - Visit the [example database](https://frosted-click-152.notion.site/176bb0eef86a80cc97e4c52b4a24c81f?v=176bb0eef86a817babb4000c29720602)
   - Click the "Duplicate" button in the top right corner to copy to your workspace
   - Wait for the database to be copied

2. Get your NOTION_PAGE_ID:
   - In your copied database page, click the "Share" button in the top right
   - Click "Publish" to make the page public
   - Copy the page link, which looks like: `https://xxx.notion.site/Blog-02ab3b8678004aa69e9e415905ef32a5`
   - Extract the last 32-character string from the link as your NOTION_PAGE_ID: `02ab3b8678004aa69e9e415905ef32a5`

> **Note**: The Notion page must be set to public access, otherwise content cannot be retrieved after deployment

### Deployment Methods

NotionNext-starter supports multiple deployment platforms. Choose one of the following:

#### Deploy to Vercel

##### Method 1: One-Click Deployment (Manual Updates)
[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/blog-starter/notionNext-starter&repository-name=my-notion-blog&env=NOTION_PAGE_ID)

> - Click the button above for one-click deployment to Vercel. You'll need to connect your GitHub account and set the `NOTION_PAGE_ID` environment variable
> - With one-click deployment, when Notion content is updated, you need to manually trigger a redeployment in the Vercel dashboard to update the website content

##### Method 2: Automatic Deployment (Recommended)
Configure GitHub Actions for automatic deployment. See the [Vercel Deployment Guide](./docs/VERCEL.md) for details.

> **Automatic Deployment Benefits**:
> - ✨ Automatic updates twice daily at 8 AM and 8 PM (UTC 0:00 and 12:00)
> - ✨ Automatic deployment of main branch updates
> - ✨ Automatic preview deployments for Pull Requests
> - ✨ Automatic deployment status comments on PRs and commits

#### Deploy to Netlify

##### Method 1: One-Click Deployment (Manual Updates)
[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/blog-starter/notionNext-starter)

> - Click the button above for one-click deployment to Netlify. You'll need to connect your GitHub account and set the `NOTION_PAGE_ID` environment variable
> - With one-click deployment, when Notion content is updated, you need to manually trigger a redeployment in the Netlify dashboard to update the website content

##### Method 2: Automatic Deployment (Recommended)
You need to complete one-click deployment first to get NETLIFY_SITE_ID, then configure GitHub Actions for automatic deployment. See the [Netlify Deployment Guide](./docs/NETLIFY.md) for details.

### Environment Variables

All deployment methods require the following basic environment variables:

```bash
NOTION_PAGE_ID         # Your Notion page ID (Required)
                      # How to get: Open your Notion page, click Share, set to Public, copy the ID from the page URL
                      # Example: https://www.notion.so/xxx/Your-Page-Title-02ab3b8678004aa69e9e415905ef32a5
                      #          where 02ab3b8678004aa69e9e415905ef32a5 is the page ID
                      # Multi-language support: Separate multiple page IDs with commas, e.g.:
                      # 02ab3b8678004aa69e9e415905ef32a5,en:7c1d570661754c8fbc568e00a01fd70e

NEXT_PUBLIC_THEME      # Theme, default 'simple'
                      # Available themes can be found in the themes folder

NEXT_PUBLIC_LANG       # Language, default 'zh-CN'
                      # Supports 'zh-CN'(Simplified Chinese) and 'en-US'(English)

NEXT_PUBLIC_AUTHOR     # Author name
                      # Displayed in website footer and article author information

NEXT_PUBLIC_LINK       # Website URL
                      # Example: https://your-blog.vercel.app
```

> Note: If optional environment variables are not configured, default values from blog.config.js will be used. It's recommended to at least configure the required variables.

[fork]: https://github.com/blog-starter/notionNext-starter/fork
[pr]: https://github.com/blog-starter/notionNext-starter/compare


