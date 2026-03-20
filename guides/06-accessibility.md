# 无障碍设计

> 让 AI 生成的代码对所有用户友好，包括使用屏幕阅读器和键盘的用户。

## WCAG 开发者必知

### 四大原则

1. **可感知**：信息必须能被用户感知（文本替代、字幕）
2. **可操作**：界面可通过键盘和辅助技术操作
3. **可理解**：信息和操作是可理解的
4. **健壮性**：内容可被多种工具正确解析

### AA 级最低要求

- 正文对比度 >= 4.5:1
- 大文本对比度 >= 3:1
- 所有功能可通过键盘完成
- 表单输入有关联的标签
- 图片有替代文本

## ARIA 标签和角色

### 常用 ARIA 属性

```html
<!-- 按钮：图标按钮需要 aria-label -->
<button aria-label="关闭弹窗" class="p-2 rounded-full hover:bg-gray-100">
  <svg class="h-5 w-5"><!-- X 图标 --></svg>
</button>

<!-- 导航：用 aria-label 区分多个 nav -->
<nav aria-label="主导航">...</nav>
<nav aria-label="面包屑">...</nav>

<!-- 弹窗：role + aria-modal + aria-labelledby -->
<div role="dialog" aria-modal="true" aria-labelledby="dialog-title">
  <h2 id="dialog-title">确认操作</h2>
</div>

<!-- 状态提示：aria-live 让屏幕阅读器播报变化 -->
<div aria-live="polite" class="sr-only">已保存成功</div>

<!-- 展开/折叠 -->
<button aria-expanded="false" aria-controls="menu-content">菜单</button>
<div id="menu-content" hidden>...</div>
```

### Before vs After

```html
<!-- 之前：屏幕阅读器不知道这是什么 -->
<div onclick="closeModal()" class="cursor-pointer">X</div>

<!-- 之后：语义化、可访问 -->
<button aria-label="关闭" onclick="closeModal()"
  class="flex h-8 w-8 items-center justify-center rounded-full hover:bg-gray-100">
  <svg class="h-4 w-4" aria-hidden="true"><!-- X icon --></svg>
</button>
```

## 键盘导航

### 焦点管理

```html
<!-- 可见的焦点环 -->
<button class="rounded-lg bg-blue-600 px-4 py-2 text-white
  focus-visible:outline focus-visible:outline-2
  focus-visible:outline-offset-2 focus-visible:outline-blue-600">
  操作
</button>

<!-- 跳过导航链接（放在 body 开头） -->
<a href="#main-content"
  class="sr-only focus:not-sr-only focus:absolute focus:z-50
  focus:rounded-lg focus:bg-blue-600 focus:px-4 focus:py-2 focus:text-white">
  跳到主内容
</a>
```

### 键盘交互规范

| 组件 | 按键 | 行为 |
|------|------|------|
| 按钮 | Enter / Space | 触发操作 |
| 链接 | Enter | 跳转 |
| 弹窗 | Escape | 关闭 |
| Tab 选项卡 | 方向键 | 切换 |
| 下拉菜单 | 方向键 | 上下移动 |
| 下拉菜单 | Escape | 关闭 |

### Tab 顺序

```html
<!-- 使用 tabindex 管理焦点顺序 -->
<div tabindex="0">可获得焦点的自定义元素</div>
<div tabindex="-1">只能通过 JS focus() 获得焦点</div>
<!-- 永远不要用 tabindex > 0 -->
```

## 屏幕阅读器友好

### 视觉隐藏但可读

```html
<!-- Tailwind 的 sr-only：视觉隐藏但屏幕阅读器可读 -->
<label for="search" class="sr-only">搜索</label>
<input id="search" type="search" placeholder="搜索..." />

<!-- 装饰性图标对屏幕阅读器隐藏 -->
<svg aria-hidden="true" class="h-5 w-5">...</svg>

<!-- 有意义的图片提供替代文本 -->
<img src="chart.png" alt="2024年销售趋势图，Q4 同比增长 23%" />

<!-- 纯装饰图片 -->
<img src="decoration.svg" alt="" role="presentation" />
```

### 表单无障碍

```html
<!-- 每个输入都需要关联 label -->
<div>
  <label for="name" class="block text-sm font-medium text-gray-700">姓名</label>
  <input id="name" type="text" required aria-required="true"
    class="mt-1 block w-full rounded-lg border-gray-300" />
</div>

<!-- 错误信息关联到输入框 -->
<div>
  <label for="email" class="block text-sm font-medium text-gray-700">邮箱</label>
  <input id="email" type="email" aria-invalid="true" aria-describedby="email-err"
    class="mt-1 block w-full rounded-lg border-red-300" />
  <p id="email-err" role="alert" class="mt-1 text-sm text-red-600">
    请输入有效的邮箱地址
  </p>
</div>
```

## 颜色对比度

### 检查工具

- Chrome DevTools: Inspect > 查看对比度
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- Figma 插件：Stark

### 安全的颜色搭配

| 文本颜色 | 背景 | 对比度 | 通过？ |
|----------|------|--------|--------|
| `gray-900` | `white` | 15.4:1 | AA + AAA |
| `gray-600` | `white` | 5.7:1 | AA |
| `gray-500` | `white` | 4.6:1 | AA（勉强） |
| `gray-400` | `white` | 3.0:1 | 仅大文本 |
| `white` | `blue-600` | 6.3:1 | AA + AAA |

## 提示 AI 写无障碍代码

```markdown
## 无障碍要求
- 所有图片有 alt 文本（装饰性图片用 alt=""）
- 所有表单 input 有关联的 label
- 按钮有描述性文本或 aria-label
- 弹窗有 role="dialog" 和 aria-labelledby
- 使用语义化 HTML（nav, main, header, footer, section）
- 焦点样式可见（focus-visible:outline）
- 颜色对比度满足 WCAG AA
```
