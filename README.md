## 🚀 NotionNext-starter 部署

[README in English](./README_EN.md) | [中文文档]

### 准备工作

在开始部署之前，你需要：

1. 复制 Notion 数据库模板：
   - 访问[示例数据库](https://frosted-click-152.notion.site/176bb0eef86a80cc97e4c52b4a24c81f?v=176bb0eef86a817babb4000c29720602)
   - 点击右上角的 "Duplicate" 按钮复制到你自己的工作区
   - 等待数据库复制完成

2. 获取 NOTION_PAGE_ID：
   - 在你复制的数据库页面中，点击右上角的 "Share" 按钮
   - 点击 "Publish" 将页面设为公开访问
   - 复制页面链接，格式如：`https://xxx.notion.site/Blog-02ab3b8678004aa69e9e415905ef32a5`
   - 提取链接中最后一段 32 位字符串，即为 NOTION_PAGE_ID：`02ab3b8678004aa69e9e415905ef32a5`

> **注意**：必须将 Notion 页面设为公开访问，否则部署后无法正常获取内容

### 部署方式

NotionNext-starter 支持多个部署平台，你可以选择以下任一平台进行部署：

#### Vercel 部署

##### 方式一：一键部署到 Vercel（手动更新）
[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/blog-starter/notionNext-starter&repository-name=my-notion-blog&env=NOTION_PAGE_ID)

> - 点击上方按钮，跳转至 Vercel 进行一键部署。部署时需要绑定 GitHub 账号，并填写 `NOTION_PAGE_ID` 环境变量
> - 采用一键部署时，当 Notion 内容更新后，需要手动在 Vercel 面板触发重新部署才能更新网站内容

##### 方式二：自动部署（推荐）
需要配置 GitHub Actions 实现自动部署，详见 [Vercel 部署指南](./docs/VERCEL.md)。

> **自动部署优势**：
> - ✨ 每天早 8 点和晚 8 点自动更新部署（UTC 0:00 和 12:00）
> - ✨ 自动部署 main 分支的更新
> - ✨ 自动为 Pull Request 创建预览部署
> - ✨ 自动在 PR 和提交中添加部署状态评论

#### Netlify 部署

##### 方式一：一键部署到 Netlify（手动更新）
[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/blog-starter/notionNext-starter)

> - 点击上方按钮，跳转至 Netlify 进行一键部署。部署时需要绑定 GitHub 账号，并填写 `NOTION_PAGE_ID` 环境变量
> - 采用一键部署时，当 Notion 内容更新后，需要手动在 Netlify 面板触发重新部署才能更新网站内容

##### 方式二：自动部署（推荐）
需要先完成一键部署以获取 NETLIFY_SITE_ID，然后配置 GitHub Actions 实现自动部署，详见 [Netlify 部署指南](./docs/NETLIFY.md)。

### 环境变量说明

所有部署方式都需要设置以下基础环境变量：

```bash
NOTION_PAGE_ID         # 你的 Notion 页面 ID (必需)
                      # 获取方式：打开 Notion 页面，点击 Share，设置为 Public，复制页面链接中的 ID
                      # 例如：https://www.notion.so/xxx/Your-Page-Title-02ab3b8678004aa69e9e415905ef32a5
                      #      其中 02ab3b8678004aa69e9e415905ef32a5 就是页面 ID
                      # 多语言支持：用逗号分隔多个页面 ID，例如：
                      # 02ab3b8678004aa69e9e415905ef32a5,en:7c1d570661754c8fbc568e00a01fd70e

NEXT_PUBLIC_THEME      # 主题，默认 'simple'
                      # 支持的主题可在 themes 文件夹下找到

NEXT_PUBLIC_LANG       # 语言，默认 'zh-CN'
                      # 支持 'zh-CN'(简体中文) 和 'en-US'(英文)

NEXT_PUBLIC_AUTHOR     # 作者名称
                      # 显示在网站页脚和文章作者信息中

NEXT_PUBLIC_LINK       # 网站地址
                      # 例如：https://your-blog.vercel.app
```

> 提示：如果不配置可选的环境变量，将使用 blog.config.js 中的默认值。建议至少配置必需的环境变量。

[fork]: https://github.com/blog-starter/notionNext-starter/fork
[pr]: https://github.com/blog-starter/notionNext-starter/compare