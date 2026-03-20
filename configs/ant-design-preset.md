# Ant Design 主题配置指南

> 配置 Ant Design 主题并引导 AI 遵循 Ant Design 规范。

## 安装

```bash
# React 项目
npm install antd @ant-design/icons

# 按需导入（Ant Design 5.x 默认支持 Tree Shaking）
# 无需额外配置 babel-plugin-import
```

## 主题配置（v5 ConfigProvider）

### 基础主题

```tsx
// src/App.tsx
import { ConfigProvider } from 'antd';
import zhCN from 'antd/locale/zh_CN';

const theme = {
  token: {
    // --- 品牌色 ---
    colorPrimary: '#2563eb',
    colorSuccess: '#16a34a',
    colorWarning: '#d97706',
    colorError: '#dc2626',
    colorInfo: '#2563eb',

    // --- 字体 ---
    fontFamily: '"PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif',
    fontSize: 14,

    // --- 圆角 ---
    borderRadius: 8,
    borderRadiusLG: 12,
    borderRadiusSM: 6,

    // --- 间距 ---
    marginXS: 8,
    marginSM: 12,
    margin: 16,
    marginLG: 24,

    // --- 阴影 ---
    boxShadow: '0 1px 2px 0 rgb(0 0 0 / 0.05)',
    boxShadowSecondary: '0 4px 12px 0 rgb(0 0 0 / 0.08)',
  },
  components: {
    Button: {
      controlHeight: 40,
      paddingContentHorizontal: 20,
    },
    Input: {
      controlHeight: 40,
    },
    Card: {
      paddingLG: 24,
    },
  },
};

function App() {
  return (
    <ConfigProvider theme={theme} locale={zhCN}>
      <YourApp />
    </ConfigProvider>
  );
}
```

### 暗色主题

```tsx
import { theme as antTheme } from 'antd';

<ConfigProvider theme={{
  algorithm: antTheme.darkAlgorithm,
  token: {
    colorPrimary: '#3b82f6',
  },
}}>
  <App />
</ConfigProvider>
```

## 常用组件模式

### 表格页面

```tsx
import { Table, Button, Input, Space, Tag } from 'antd';
import { SearchOutlined, PlusOutlined } from '@ant-design/icons';

function UserTable() {
  const columns = [
    { title: '姓名', dataIndex: 'name', key: 'name' },
    {
      title: '状态',
      dataIndex: 'status',
      key: 'status',
      render: (status) => (
        <Tag color={status === 'active' ? 'green' : 'default'}>
          {status === 'active' ? '活跃' : '停用'}
        </Tag>
      ),
    },
    {
      title: '操作',
      key: 'action',
      render: () => (
        <Space>
          <Button type="link" size="small">编辑</Button>
          <Button type="link" size="small" danger>删除</Button>
        </Space>
      ),
    },
  ];

  return (
    <div>
      <div style={{ marginBottom: 16, display: 'flex', justifyContent: 'space-between' }}>
        <Input prefix={<SearchOutlined />} placeholder="搜索用户" style={{ width: 240 }} />
        <Button type="primary" icon={<PlusOutlined />}>新增用户</Button>
      </div>
      <Table columns={columns} dataSource={data} />
    </div>
  );
}
```

### 表单页面

```tsx
import { Form, Input, Select, Button, Card, message } from 'antd';

function CreateForm() {
  const [form] = Form.useForm();

  const onFinish = (values) => {
    console.log(values);
    message.success('创建成功');
  };

  return (
    <Card title="创建项目">
      <Form form={form} layout="vertical" onFinish={onFinish} style={{ maxWidth: 600 }}>
        <Form.Item label="项目名称" name="name"
          rules={[{ required: true, message: '请输入项目名称' }]}>
          <Input placeholder="请输入项目名称" />
        </Form.Item>
        <Form.Item label="项目类型" name="type"
          rules={[{ required: true, message: '请选择项目类型' }]}>
          <Select placeholder="请选择">
            <Select.Option value="web">Web 应用</Select.Option>
            <Select.Option value="mobile">移动应用</Select.Option>
          </Select>
        </Form.Item>
        <Form.Item label="描述" name="description">
          <Input.TextArea rows={4} placeholder="请输入项目描述" />
        </Form.Item>
        <Form.Item>
          <Space>
            <Button type="primary" htmlType="submit">创建</Button>
            <Button onClick={() => form.resetFields()}>重置</Button>
          </Space>
        </Form.Item>
      </Form>
    </Card>
  );
}
```

## 告诉 AI 的 CLAUDE.md 模板

```markdown
## UI 框架：Ant Design 5.x

### 组件使用规则
- 所有 UI 使用 antd 组件，不要用原生 HTML 替代
- 按钮：Button（type: primary / default / text / link / dashed）
- 表单：Form + Form.Item，验证用 rules
- 表格：Table + columns 定义
- 弹窗：Modal / Drawer
- 提示：message.success/error/warning
- 图标：从 @ant-design/icons 导入
- 布局：用 antd 的 Layout / Row / Col / Space / Flex

### 样式规则
- 不要在 antd 组件上覆盖 Tailwind 类（会冲突）
- 定制样式通过 ConfigProvider theme token
- 间距用 antd 的 Space 组件或 style.marginBottom
- 主题色：#2563eb

### 国际化
- 中文语言包已配置（zhCN）
- 日期组件自动中文化
```
