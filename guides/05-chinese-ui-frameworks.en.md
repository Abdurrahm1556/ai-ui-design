# Chinese UI Frameworks

> Guide AI to correctly use popular Chinese UI frameworks: conventions, theming, and best practices.

## Ant Design (React)

### Component Conventions

Ant Design has its own design language. Tell AI to follow it:

```jsx
// Correct: use Ant Design components and APIs
import { Button, Space, message } from 'antd';

function ActionBar() {
  return (
    <Space>
      <Button type="primary" onClick={() => message.success('Saved')}>
        Save
      </Button>
      <Button>Cancel</Button>
      <Button type="text" danger>Delete</Button>
    </Space>
  );
}
```

```html
<!-- Wrong: hand-coding button styles in an Ant Design project -->
<button class="bg-blue-600 text-white px-4 py-2 rounded">Save</button>
```

### Theme Customization (v5 ConfigProvider)

```jsx
import { ConfigProvider } from 'antd';

<ConfigProvider theme={{
  token: {
    colorPrimary: '#2563eb',
    borderRadius: 8,
    fontFamily: 'Inter, system-ui, sans-serif',
  },
}}>
  <App />
</ConfigProvider>
```

### Prompt for AI

```
This project uses Ant Design 5.x (React). All UI must use antd components.
Do not substitute antd components with raw HTML or Tailwind. Use Form + Form.Item
for forms, Table for tables, Modal for dialogs, message/notification for toasts.
```

## Element Plus (Vue 3)

### Layout Patterns

```vue
<template>
  <el-container>
    <el-aside width="240px">
      <el-menu default-active="1" :router="true">
        <el-menu-item index="/">Home</el-menu-item>
        <el-menu-item index="/users">User Management</el-menu-item>
      </el-menu>
    </el-aside>
    <el-main>
      <!-- Page content -->
    </el-main>
  </el-container>
</template>
```

### Form Validation

```vue
<template>
  <el-form :model="form" :rules="rules" ref="formRef" label-width="100px">
    <el-form-item label="Username" prop="username">
      <el-input v-model="form.username" placeholder="Enter username" />
    </el-form-item>
    <el-form-item label="Email" prop="email">
      <el-input v-model="form.email" placeholder="Enter email" />
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="onSubmit">Submit</el-button>
    </el-form-item>
  </el-form>
</template>

<script setup>
const rules = {
  username: [{ required: true, message: 'Please enter username', trigger: 'blur' }],
  email: [
    { required: true, message: 'Please enter email', trigger: 'blur' },
    { type: 'email', message: 'Please enter a valid email', trigger: 'blur' },
  ],
};
</script>
```

## TDesign (Tencent)

### Design Tokens

```jsx
// TDesign React theme customization
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

### Mobile Adaptation

TDesign provides separate mobile component libraries (`tdesign-mobile-react` / `tdesign-mobile-vue`). Do not mix desktop components into mobile projects.

## Vant (Mobile Vue)

### Mobile-First Patterns

```vue
<template>
  <van-nav-bar title="Product Details" left-arrow @click-left="$router.back()" />

  <van-card
    price="29.90"
    title="Product Name"
    desc="Product description"
    thumb="product.jpg"
  />

  <van-action-bar>
    <van-action-bar-icon icon="chat-o" text="Support" />
    <van-action-bar-icon icon="cart-o" text="Cart" badge="5" />
    <van-action-bar-button type="warning" text="Add to Cart" />
    <van-action-bar-button type="danger" text="Buy Now" />
  </van-action-bar>
</template>
```

### Key Vant Conventions

- Use `vw` adaptation (postcss-px-to-viewport)
- Lists: `van-list` for infinite scroll
- Pull-to-refresh: `van-pull-refresh`
- Popups: `van-popup` instead of custom implementations

## WeChat Mini Program UI

### Native Components

```html
<!-- pages/index/index.wxml -->
<view class="container">
  <view class="card">
    <text class="title">Title</text>
    <text class="desc">Description</text>
  </view>

  <button type="primary" bindtap="handleSubmit">Submit</button>
  <button type="default" bindtap="handleCancel">Cancel</button>
</view>
```

### Using WeUI

```json
// app.json
{
  "useExtendedLib": {
    "weui": true
  }
}
```

```html
<!-- Using WeUI components -->
<mp-cells title="Form">
  <mp-cell>
    <input placeholder="Enter username" />
  </mp-cell>
</mp-cells>
```

## Telling AI Which Framework to Use

Declare it explicitly in your `CLAUDE.md`:

```markdown
## UI Framework
- This project uses [Ant Design 5.x / Element Plus / TDesign / Vant 4]
- All UI must use framework components, no hand-rolled replacements
- Brand color: #2563eb
- Form validation via framework's built-in Form component
- Icons from the framework's companion icon library
- Do not mix components from other UI frameworks
```
