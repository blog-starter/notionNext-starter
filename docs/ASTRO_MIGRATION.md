# NotionNext-starter Astro 迁移指南

## 目录
- [项目概述](#项目概述)
- [迁移原因](#迁移原因)
- [架构对比](#架构对比)
- [迁移步骤](#迁移步骤)
- [部署方案](#部署方案)
- [注意事项](#注意事项)

## 项目概述

NotionNext-starter 是一个基于 Notion API 的博客系统，目前使用 Next.js 开发。主要特点：
- 多主题支持
- Notion 作为 CMS
- 自动部署能力
- 国际化支持

## 迁移原因

### 性能优化
- 默认零 JavaScript 输出
- 更小的打包体积
- 更快的首屏加载

### 开发体验
- 更简单的配置
- 更快的开发服务器
- 内置 Markdown 支持

### 部署优化
- 纯静态输出
- 更低的服务器要求
- 更好的缓存策略

## 架构对比

### 当前架构 (Next.js)
```
notionNext-starter/
├── lib/                    # 核心库文件
│   ├── notion/            # Notion API 相关
│   ├── theme/             # 主题系统
│   └── utils/             # 工具函数
├── themes/                 # 主题文件
├── pages/                 # Next.js 页面
├── components/            # 通用组件
├── public/                # 静态资源
└── blog.config.js         # 博客配置文件
```

### 迁移后架构 (Astro)
```
notion-astro/
├── src/
│   ├── components/     # 通用组件
│   ├── layouts/       # Astro 布局文件
│   ├── pages/         # 页面路由
│   ├── styles/        # 全局样式
│   └── themes/        # 主题文件
├── lib/               # 核心库文件
│   ├── notion/       # Notion API 相关
│   └── utils/        # 工具函数
├── public/           # 静态资源
└── astro.config.mjs  # Astro 配置
```

## 迁移步骤

### 1. 项目初始化
```bash
# 创建新的 Astro 项目
npm create astro@latest notion-astro
cd notion-astro

# 安装依赖
npm install @astrojs/react @astrojs/tailwind notion-client
```

### 2. 配置 Astro
```javascript
// astro.config.mjs
import { defineConfig } from 'astro/config';
import react from '@astrojs/react';
import tailwind from '@astrojs/tailwind';

export default defineConfig({
  integrations: [react(), tailwind()],
  output: 'static',
  build: {
    assets: 'assets'
  }
});
```

### 3. 主题系统迁移

```astro
// src/layouts/ThemeProvider.astro
---
const { theme = 'simple' } = Astro.props;
---

<div class={`theme-${theme}`}>
  <slot />
</div>

<style is:global>
  @import `../themes/${theme}/styles/index.css`;
</style>
```

### 4. Notion 集成

```typescript
// lib/notion/index.ts
import { NotionAPI } from 'notion-client'

export class NotionService {
  private api: NotionAPI

  constructor() {
    this.api = new NotionAPI()
  }

  async getPage(pageId: string) {
    return await this.api.getPage(pageId)
  }
}
```

### 5. 路由迁移

```astro
// src/pages/index.astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import { NotionService } from '../lib/notion';

const notion = new NotionService();
const posts = await notion.getPosts();
---

<BaseLayout>
  <main>
    {posts.map(post => (
      <article>
        <h2>{post.title}</h2>
        <p>{post.excerpt}</p>
      </article>
    ))}
  </main>
</BaseLayout>
```

## 部署方案

### Vercel 部署
```yaml
# vercel.json
{
  "buildCommand": "astro build",
  "outputDirectory": "dist",
  "framework": "astro"
}
```

### Netlify 部署
```toml
# netlify.toml
[build]
  command = "astro build"
  publish = "dist"
```

### 环境变量配置
```env
NOTION_PAGE_ID=xxx
PUBLIC_THEME=simple
PUBLIC_LANG=zh-CN
```

## 注意事项

### 1. 数据获取策略
- 构建时获取 Notion 数据
- 使用增量构建更新内容
- 配置合理的缓存策略

### 2. 主题兼容性
- 保持主题文件结构
- 迁移现有样式
- 处理动态样式加载

### 3. 性能优化
- 图片优化
- 组件按需加载
- 资源预加载

### 4. SEO 优化
- 生成静态 meta 标签
- 自动生成 sitemap
- 优化 robots.txt

## 迁移收益

### 1. 性能提升
- 更快的首屏加载
- 更小的资源体积
- 更好的 SEO 表现

### 2. 开发体验
- 更简单的配置
- 更快的构建速度
- 更好的类型支持

### 3. 维护成本
- 更少的运行时依赖
- 更简单的部署流程
- 更低的服务器要求

## 后续规划

### 1. 功能增强
- [ ] 评论系统集成
- [ ] 搜索功能优化
- [ ] 自定义主题支持

### 2. 性能优化
- [ ] 图片处理优化
- [ ] 字体加载优化
- [ ] 缓存策略优化

### 3. 开发体验
- [ ] 开发工具完善
- [ ] 文档更新
- [ ] 示例完善

## 参考资源

- [Astro 官方文档](https://docs.astro.build)
- [Notion API 文档](https://developers.notion.com)
- [NotionNext-starter 文档](https://docs.tangly1024.com) 