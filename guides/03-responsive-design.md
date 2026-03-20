# 响应式设计

> 让 AI 生成在所有设备上都好看的布局，从移动优先开始。

## 移动优先策略

核心原则：**先写手机端样式，再用断点向上扩展。**

```html
<!-- 正确：移动优先 -->
<div class="px-4 sm:px-6 lg:px-8">
  <h1 class="text-2xl sm:text-3xl lg:text-4xl">标题</h1>
</div>

<!-- 错误：桌面优先再缩小 -->
<div class="px-8 md:px-6 sm:px-4">  <!-- 反了！ -->
```

**告诉 AI 的提示词：**

```
始终使用移动优先的响应式设计。先写无断点前缀的基础样式（手机端），
然后用 sm:、md:、lg: 前缀逐步增强到大屏幕。
```

## 断点策略

### Tailwind 默认断点

| 断点 | 宽度 | 典型设备 |
|------|------|----------|
| 默认 | 0px+ | 手机竖屏 |
| `sm` | 640px+ | 手机横屏、小平板 |
| `md` | 768px+ | 平板竖屏 |
| `lg` | 1024px+ | 平板横屏、小笔记本 |
| `xl` | 1280px+ | 笔记本、桌面显示器 |
| `2xl` | 1536px+ | 大屏显示器 |

### 实际使用中只需关注三个

- **默认**（手机）：单列布局
- **`md`**（平板）：两列布局
- **`lg`**（桌面）：完整多列布局

## 常用响应式模式

### 堆叠转并排

```html
<!-- 手机：垂直堆叠 / 平板+：水平排列 -->
<div class="flex flex-col gap-4 md:flex-row">
  <div class="md:w-1/2">左侧内容</div>
  <div class="md:w-1/2">右侧内容</div>
</div>
```

### 可折叠侧边栏

```html
<div class="flex min-h-screen">
  <!-- 侧边栏：手机隐藏，桌面显示 -->
  <aside class="hidden lg:flex lg:w-64 lg:flex-col bg-gray-900">
    <!-- 导航内容 -->
  </aside>
  <!-- 主区域：始终显示 -->
  <main class="flex-1 px-4 py-6 lg:px-8">
    <!-- 手机端汉堡菜单按钮 -->
    <button class="lg:hidden mb-4 rounded-lg p-2 text-gray-500 hover:bg-gray-100">
      <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
          d="M4 6h16M4 12h16M4 18h16" />
      </svg>
    </button>
    <!-- 页面内容 -->
  </main>
</div>
```

### 自适应网格

```html
<!-- 手机 1 列 / 平板 2 列 / 桌面 3 列 / 大屏 4 列 -->
<div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
  <div class="rounded-xl bg-white p-4 shadow-sm ring-1 ring-gray-200">卡片 1</div>
  <div class="rounded-xl bg-white p-4 shadow-sm ring-1 ring-gray-200">卡片 2</div>
  <div class="rounded-xl bg-white p-4 shadow-sm ring-1 ring-gray-200">卡片 3</div>
  <div class="rounded-xl bg-white p-4 shadow-sm ring-1 ring-gray-200">卡片 4</div>
</div>
```

### 响应式表格

```html
<!-- 小屏幕水平滚动 -->
<div class="overflow-x-auto">
  <table class="min-w-full divide-y divide-gray-200">
    <!-- 表格内容 -->
  </table>
</div>

<!-- 或者：小屏幕切换为卡片布局 -->
<div class="hidden md:block">
  <!-- 桌面端表格 -->
</div>
<div class="space-y-4 md:hidden">
  <!-- 移动端卡片列表 -->
</div>
```

## 触摸目标和移动 UX

### 最小触摸区域

按钮和可点击区域至少 44x44px：

```html
<!-- 正确：足够大的触摸目标 -->
<button class="min-h-[44px] min-w-[44px] px-4 py-3">点击</button>

<!-- 图标按钮也要确保触摸区域够大 -->
<button class="flex h-11 w-11 items-center justify-center rounded-full hover:bg-gray-100">
  <svg class="h-5 w-5" ...></svg>
</button>
```

### 移动端输入优化

```html
<!-- 使用正确的 input type 触发合适的虚拟键盘 -->
<input type="email" inputmode="email" />     <!-- 邮箱键盘 -->
<input type="tel" inputmode="tel" />          <!-- 数字键盘 -->
<input type="url" inputmode="url" />          <!-- URL 键盘 -->
<input type="number" inputmode="decimal" />   <!-- 数字键盘带小数点 -->
```

### 安全区域适配

```html
<!-- 适配刘海屏和底部横条 -->
<div class="pb-safe">
  <nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200
    px-4 pb-[env(safe-area-inset-bottom)]">
    <!-- 底部导航 -->
  </nav>
</div>
```

## 提示 AI 生成响应式布局

放入 `CLAUDE.md`：

```markdown
## 响应式设计规则
- 始终移动优先：基础样式为手机端，sm/md/lg 递增
- 手机：单列，px-4 水平留白
- 平板（md）：可用双列，px-6
- 桌面（lg）：多列布局，max-w-7xl 居中，px-8
- 所有可点击元素最小 44x44px
- 表格在小屏幕要可横向滚动
- 导航在手机端折叠为汉堡菜单
```
