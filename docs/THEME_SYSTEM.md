# Astro 主题系统设计方案

## 目录结构 



```
notion-astro/
├── src/
│   ├── themes/              # 主题目录
│   │   ├── simple/         # simple 主题
│   │   │   ├── styles/    # 主题样式
│   │   │   ├── components/# 主题组件
│   │   │   └── config.ts  # 主题配置
│   │   └── next/          # next 主题
│   │       ├── styles/
│   │       ├── components/
│   │       └── config.ts
│   └── layouts/
│       └── ThemeLayout.astro # 主题布局组件
├── lib/
│   └── theme/
│       ├── context.ts      # 主题上下文
│       └── utils.ts        # 主题工具函数
└── astro.config.mjs
```

## 核心实现

1. **主题提供者组件**
```astro:src/layouts/ThemeLayout.astro
---
import { getTheme } from '../lib/theme/utils';
const { theme = getTheme() } = Astro.props;

// 动态导入主题样式
const themeStyles = await import(`../themes/${theme}/styles/index.css`);
---

<div class={`theme-${theme}`} data-theme={theme}>
  <slot />
</div>

<style is:global>
  @import url('../themes/${theme}/styles/index.css');
</style>

<script>
  // 客户端主题切换逻辑
  const themeToggle = document.getElementById('theme-toggle');
  if (themeToggle) {
    themeToggle.addEventListener('change', (e) => {
      const theme = e.target.value;
      document.documentElement.dataset.theme = theme;
      localStorage.setItem('theme', theme);
      window.location.reload(); // 重新加载以应用新主题
    });
  }
</script>
```

2. **主题配置文件**
```typescript:src/themes/simple/config.ts
export default {
  name: 'simple',
  label: '简约主题',
  colors: {
    primary: '#0070f3',
    background: '#ffffff',
    text: '#000000'
  },
  fonts: {
    body: 'system-ui, sans-serif',
    heading: 'Georgia, serif'
  }
}
```

3. **主题切换组件**
```astro:src/components/ThemeSwitcher.astro
---
import { getAvailableThemes, getCurrentTheme } from '../lib/theme/utils';

const themes = await getAvailableThemes();
const currentTheme = getCurrentTheme();
---

<select id="theme-toggle" class="theme-toggle">
  {themes.map(theme => (
    <option value={theme.name} selected={theme.name === currentTheme}>
      {theme.label}
    </option>
  ))}
</select>

<style>
  .theme-toggle {
    padding: 0.5rem;
    border-radius: 0.25rem;
    border: 1px solid var(--border-color);
  }
</style>
```

4. **主题工具函数**
```typescript:src/lib/theme/utils.ts
import fs from 'node:fs';
import path from 'node:path';

// 获取可用主题列表
export async function getAvailableThemes() {
  const themesDir = path.join(process.cwd(), 'src/themes');
  const themes = fs.readdirSync(themesDir)
    .filter(file => fs.statSync(path.join(themesDir, file)).isDirectory())
    .map(async themeName => {
      const config = await import(`../themes/${themeName}/config.ts`);
      return {
        name: themeName,
        ...config.default
      };
    });
  
  return Promise.all(themes);
}

// 获取当前主题
export function getCurrentTheme() {
  if (typeof localStorage !== 'undefined') {
    return localStorage.getItem('theme') || 'simple';
  }
  return 'simple';
}

// 设置主题
export function setTheme(theme: string) {
  if (typeof localStorage !== 'undefined') {
    localStorage.setItem('theme', theme);
    document.documentElement.dataset.theme = theme;
  }
}
```

5. **使用示例**
```astro:src/pages/index.astro
---
import ThemeLayout from '../layouts/ThemeLayout.astro';
import ThemeSwitcher from '../components/ThemeSwitcher.astro';
---

<ThemeLayout>
  <header>
    <ThemeSwitcher />
  </header>
  <main>
    <h1>Welcome to my blog</h1>
    <!-- 其他内容 -->
  </main>
</ThemeLayout>
```

## 主题开发指南

1. **创建新主题**
- 在 `src/themes` 下创建新目录
- 复制基础主题结构
- 修改主题配置和样式

2. **主题结构要求**
```
theme-name/
├── styles/
│   ├── index.css     # 主样式入口
│   ├── variables.css # 主题变量
│   └── layout.css    # 布局样式
├── components/       # 主题特定组件
└── config.ts        # 主题配置
```

3. **样式规范**
- 使用 CSS 变量定义主题颜色
- 遵循命名空间规范
- 避免样式冲突

## 注意事项

1. **性能优化**
- 按需加载主题资源
- 优化主题切换过程
- 缓存主题资源

2. **兼容性处理**
- 提供默认主题回退
- 处理主题切换过渡
- 支持无 JS 降级

3. **开发建议**
- 使用 CSS 变量
- 保持主题结构一致
- 提供完整的主题配置
```

这个方案的优势在于：

1. **灵活性**：可以轻松添加新主题
2. **性能**：主题资源按需加载
3. **可维护性**：主题结构清晰，易于管理
4. **用户体验**：支持实时主题切换
5. **开发友好**：提供清晰的主题开发规范

需要我详细解释某个部分吗？
