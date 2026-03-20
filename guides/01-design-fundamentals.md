# 设计基础

> 让 AI 理解你的设计系统，从配色、字体、间距三大基石开始。

## 配色理论

### 构建可访问的调色板

不要让 AI 随便选颜色。提供一套语义化的配色方案：

```
主色（Primary）:   #2563EB (blue-600)  — 主要操作、链接
成功（Success）:    #16A34A (green-600) — 成功状态
警告（Warning）:    #D97706 (amber-600) — 需要注意
危险（Danger）:     #DC2626 (red-600)   — 破坏性操作、错误
中性（Neutral）:    #6B7280 (gray-500)  — 正文、边框、次要信息
```

### 对比度要求

| 元素 | 最低对比度 | 示例 |
|------|-----------|------|
| 正文文本 | 4.5:1 | `text-gray-900` on `bg-white` |
| 大号标题 | 3:1 | `text-gray-700` on `bg-white` |
| UI 组件 | 3:1 | `border-gray-300` on `bg-white` |

**告诉 AI 的提示词：**

```
所有文本必须满足 WCAG AA 对比度要求。正文使用 gray-900，次要文本使用 gray-600，
占位符使用 gray-400。不要使用纯黑 #000。
```

## 字体系统

### 模块化字体比例（1.25 倍）

```css
/* 推荐的字体大小层级 */
--text-xs:   0.75rem;   /* 12px — 辅助信息 */
--text-sm:   0.875rem;  /* 14px — 次要文本 */
--text-base: 1rem;      /* 16px — 正文 */
--text-lg:   1.25rem;   /* 20px — 小标题 */
--text-xl:   1.563rem;  /* 25px — 段落标题 */
--text-2xl:  1.953rem;  /* 31px — 页面标题 */
--text-3xl:  2.441rem;  /* 39px — Hero 标题 */
```

### 行高规则

- 正文（16px）: `line-height: 1.6`（25.6px）
- 标题（24px+）: `line-height: 1.2`
- 紧凑 UI（按钮、标签）: `line-height: 1`

### 字体搭配

```
中文正文: "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif
英文正文: Inter, system-ui, sans-serif
代码字体: "JetBrains Mono", "Fira Code", monospace
```

## 间距系统

### 4px / 8px 网格

所有间距都是 4px 的倍数。Tailwind 默认就是这套体系：

```
4px  = p-1   — 图标内边距
8px  = p-2   — 紧凑元素间距
12px = p-3   — 按钮内边距
16px = p-4   — 卡片内边距
24px = p-6   — 区块间距
32px = p-8   — 大区块间距
48px = p-12  — 页面区域间距
64px = p-16  — 页面级大间距
```

### Before vs After

```html
<!-- 之前：间距随意 -->
<div style="padding: 13px 17px; margin-bottom: 11px;">
  <h3 style="margin-bottom: 7px;">标题</h3>
  <p style="margin-bottom: 9px;">内容</p>
</div>

<!-- 之后：遵循 4px 网格 -->
<div class="p-4 mb-3">
  <h3 class="mb-2 text-lg font-semibold">标题</h3>
  <p class="mb-2 text-gray-600">内容</p>
</div>
```

## 视觉层次

### 建立层次的四种手段

1. **大小**：标题大、正文中、辅助小
2. **颜色深浅**：主要信息 `gray-900`，次要 `gray-600`，辅助 `gray-400`
3. **字重**：标题 `font-bold`，正文 `font-normal`，辅助 `font-light`
4. **空间**：重要内容周围留更多空白

### 布局原则

```html
<!-- 标准内容区域：最大宽度 + 居中 + 水平留白 -->
<main class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
  <!-- 区块之间用 py-12 或 py-16 分隔 -->
  <section class="py-12">
    <h2 class="text-2xl font-bold text-gray-900">区块标题</h2>
    <p class="mt-4 text-lg text-gray-600">区块描述文本</p>
  </section>
</main>
```

## 告诉 AI 你的设计系统

把以下内容放入项目的 `CLAUDE.md` 或系统提示词中：

```markdown
## 设计规范
- 配色：blue-600 主色，gray-900 正文，gray-600 次要文本
- 字体：Inter 英文，系统默认中文，JetBrains Mono 代码
- 间距：严格遵循 4px 网格（Tailwind 默认间距）
- 圆角：小组件 rounded-md，卡片 rounded-lg，全圆 rounded-full
- 阴影：卡片 shadow-sm，悬浮 shadow-md，弹窗 shadow-xl
- 所有文本满足 WCAG AA 对比度要求
```
