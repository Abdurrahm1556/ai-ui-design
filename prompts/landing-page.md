# 落地页提示词模板

> 复制到 CLAUDE.md 或直接发给 AI，生成专业的落地页各模块。

## Hero 区域

### 提示词

```
创建一个现代 Hero 区域，要求：
- 左侧：大标题（text-4xl lg:text-6xl font-bold）+ 副标题（text-xl text-gray-600）+ 两个 CTA 按钮（主要 + 次要）
- 右侧：产品截图或插画占位区域
- 使用 Tailwind CSS，移动优先
- 手机端上下堆叠，桌面端左右排列
- 背景使用浅色渐变或纯白
```

### 参考结构

```html
<section class="relative overflow-hidden bg-white">
  <div class="mx-auto max-w-7xl px-4 py-16 sm:px-6 lg:px-8 lg:py-24">
    <div class="flex flex-col items-center gap-12 lg:flex-row">
      <!-- 文案区 -->
      <div class="flex-1 text-center lg:text-left">
        <h1 class="text-4xl font-bold tracking-tight text-gray-900 sm:text-5xl lg:text-6xl">
          让你的产品<br />
          <span class="text-blue-600">脱颖而出</span>
        </h1>
        <p class="mt-6 text-lg text-gray-600 max-w-xl">
          一句话描述产品核心价值，解决用户什么问题。
        </p>
        <div class="mt-8 flex flex-col gap-3 sm:flex-row sm:justify-center lg:justify-start">
          <a href="#" class="rounded-lg bg-blue-600 px-6 py-3 text-sm font-semibold
            text-white shadow-sm hover:bg-blue-700 transition-colors">
            免费开始
          </a>
          <a href="#" class="rounded-lg px-6 py-3 text-sm font-semibold text-gray-700
            ring-1 ring-gray-300 hover:bg-gray-50 transition-colors">
            查看演示
          </a>
        </div>
      </div>
      <!-- 视觉区 -->
      <div class="flex-1">
        <div class="aspect-[4/3] rounded-2xl bg-gray-100 shadow-xl"></div>
      </div>
    </div>
  </div>
</section>
```

## 功能展示网格

### 提示词

```
创建 3 列功能展示区域：
- 标题 + 描述段落居中
- 下方 3 列网格（手机 1 列，平板 2 列，桌面 3 列）
- 每个功能卡片：图标 + 标题 + 简述
- 使用 Tailwind，背景 gray-50，卡片白色带 shadow-sm
```

### 参考结构

```html
<section class="bg-gray-50 py-16 lg:py-24">
  <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
    <div class="text-center">
      <h2 class="text-3xl font-bold text-gray-900">核心功能</h2>
      <p class="mt-4 text-lg text-gray-600">三个关键优势，简洁有力</p>
    </div>
    <div class="mt-12 grid grid-cols-1 gap-8 sm:grid-cols-2 lg:grid-cols-3">
      <div class="rounded-xl bg-white p-6 shadow-sm">
        <div class="flex h-10 w-10 items-center justify-center rounded-lg bg-blue-100">
          <svg class="h-5 w-5 text-blue-600"><!-- icon --></svg>
        </div>
        <h3 class="mt-4 text-lg font-semibold text-gray-900">功能名称</h3>
        <p class="mt-2 text-sm text-gray-600">功能描述，两行左右最佳。</p>
      </div>
      <!-- 重复 2 个卡片 -->
    </div>
  </div>
</section>
```

## 定价表

### 提示词

```
创建定价卡片区域，3 个方案并排：
- 基础版、专业版（推荐，高亮显示）、企业版
- 每个卡片：方案名、价格、功能列表、CTA 按钮
- 推荐方案用 ring-2 ring-blue-600 + "推荐"标签
- 手机端垂直堆叠，桌面端 3 列
```

## CTA 区域

### 提示词

```
创建页面底部 CTA 区域：
- 深色背景（bg-gray-900）或渐变背景
- 居中大标题 + 描述 + 明显的 CTA 按钮
- 简洁有力，最多两行描述
```

### 参考结构

```html
<section class="bg-gray-900 py-16 lg:py-24">
  <div class="mx-auto max-w-4xl px-4 text-center sm:px-6 lg:px-8">
    <h2 class="text-3xl font-bold text-white sm:text-4xl">
      准备好开始了吗？
    </h2>
    <p class="mt-4 text-lg text-gray-300">
      免费试用 14 天，无需信用卡。
    </p>
    <a href="#" class="mt-8 inline-block rounded-lg bg-blue-600 px-8 py-3
      text-sm font-semibold text-white shadow-sm hover:bg-blue-700 transition-colors">
      立即开始
    </a>
  </div>
</section>
```

## 页脚

### 提示词

```
创建网站页脚：
- 4 列链接区域（产品、资源、公司、法律）
- 底部：版权信息 + 社交媒体图标
- 手机端 2 列，桌面端 4 列
- 背景 gray-900，文字 gray-400
```
