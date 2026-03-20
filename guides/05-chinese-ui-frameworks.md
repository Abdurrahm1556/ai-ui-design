# 中国 UI 框架

> 引导 AI 正确使用国内主流 UI 框架的组件规范、主题定制和最佳实践。

## Ant Design（React）

### 组件规范

Ant Design 有自己的设计语言，告诉 AI 遵循它：

```jsx
// 正确：使用 Ant Design 组件和 API
import { Button, Space, message } from 'antd';

function ActionBar() {
  return (
    <Space>
      <Button type="primary" onClick={() => message.success('已保存')}>
        保存
      </Button>
      <Button>取消</Button>
      <Button type="text" danger>删除</Button>
    </Space>
  );
}
```

```html
<!-- 错误：在 Ant Design 项目中手写按钮样式 -->
<button class="bg-blue-600 text-white px-4 py-2 rounded">保存</button>
```

### 主题定制（v5 ConfigProvider）

```jsx
import { ConfigProvider } from 'antd';

<ConfigProvider theme={{
  token: {
    colorPrimary: '#2563eb',
    borderRadius: 8,
    fontFamily: '"PingFang SC", "Hiragino Sans GB", sans-serif',
  },
}}>
  <App />
</ConfigProvider>
```

### 告诉 AI 的提示词

```
本项目使用 Ant Design 5.x（React）。所有 UI 必须使用 antd 组件，
不要用原生 HTML 或 Tailwind 替代 antd 组件。表单使用 Form + Form.Item，
表格使用 Table 组件，弹窗使用 Modal，通知使用 message/notification。
```

## Element Plus（Vue 3）

### 布局模式

```vue
<template>
  <el-container>
    <el-aside width="240px">
      <el-menu default-active="1" :router="true">
        <el-menu-item index="/">首页</el-menu-item>
        <el-menu-item index="/users">用户管理</el-menu-item>
      </el-menu>
    </el-aside>
    <el-main>
      <!-- 页面内容 -->
    </el-main>
  </el-container>
</template>
```

### 表单验证

```vue
<template>
  <el-form :model="form" :rules="rules" ref="formRef" label-width="80px">
    <el-form-item label="用户名" prop="username">
      <el-input v-model="form.username" placeholder="请输入用户名" />
    </el-form-item>
    <el-form-item label="邮箱" prop="email">
      <el-input v-model="form.email" placeholder="请输入邮箱" />
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="onSubmit">提交</el-button>
    </el-form-item>
  </el-form>
</template>

<script setup>
const rules = {
  username: [{ required: true, message: '请输入用户名', trigger: 'blur' }],
  email: [
    { required: true, message: '请输入邮箱', trigger: 'blur' },
    { type: 'email', message: '请输入正确的邮箱格式', trigger: 'blur' },
  ],
};
</script>
```

## TDesign（腾讯）

### 设计令牌

```jsx
// TDesign React 主题定制
import { ConfigProvider } from 'tdesign-react';

<ConfigProvider globalConfig={{
  classPrefix: 'td',
}} theme={{
  '--td-brand-color': '#2563eb',
  '--td-border-radius': '8px',
}}>
  <App />
</ConfigProvider>
```

### 移动端适配

TDesign 提供独立的移动端组件库 `tdesign-mobile-react` / `tdesign-mobile-vue`，不要混用桌面端组件。

## Vant（移动端 Vue）

### 移动优先模式

```vue
<template>
  <van-nav-bar title="商品详情" left-arrow @click-left="$router.back()" />

  <van-card
    price="29.90"
    title="商品名称"
    desc="商品描述"
    thumb="product.jpg"
  />

  <van-action-bar>
    <van-action-bar-icon icon="chat-o" text="客服" />
    <van-action-bar-icon icon="cart-o" text="购物车" badge="5" />
    <van-action-bar-button type="warning" text="加入购物车" />
    <van-action-bar-button type="danger" text="立即购买" />
  </van-action-bar>
</template>
```

### Vant 关键约定

- 使用 `vw` 适配方案（postcss-px-to-viewport）
- 列表用 `van-list` 实现无限滚动
- 下拉刷新用 `van-pull-refresh`
- 弹出层用 `van-popup` 而非自己写

## 微信小程序 UI

### 原生组件

```html
<!-- pages/index/index.wxml -->
<view class="container">
  <view class="card">
    <text class="title">标题</text>
    <text class="desc">描述</text>
  </view>

  <button type="primary" bindtap="handleSubmit">提交</button>
  <button type="default" bindtap="handleCancel">取消</button>
</view>
```

### 使用 WeUI

```json
// app.json
{
  "useExtendedLib": {
    "weui": true
  }
}
```

```html
<!-- 使用 WeUI 组件 -->
<mp-cells title="表单">
  <mp-cell>
    <input placeholder="请输入用户名" />
  </mp-cell>
</mp-cells>
```

## 告诉 AI 使用哪个框架

在 `CLAUDE.md` 中明确声明：

```markdown
## UI 框架
- 项目使用 [Ant Design 5.x / Element Plus / TDesign / Vant 4]
- 所有 UI 必须使用该框架的组件，不要手写替代
- 主题色：#2563eb
- 表单验证使用框架自带的 Form 组件
- 图标使用框架配套的图标库
- 不要混用其他 UI 框架的组件
```
