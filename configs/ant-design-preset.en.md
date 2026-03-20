# Ant Design Theme Configuration Guide

> Configure Ant Design theming and guide AI to follow Ant Design conventions.

## Installation

```bash
# React project
npm install antd @ant-design/icons

# Tree-shaking works out of the box with Ant Design 5.x
# No need for babel-plugin-import
```

## Theme Configuration (v5 ConfigProvider)

### Basic Theme

```tsx
// src/App.tsx
import { ConfigProvider } from 'antd';
import enUS from 'antd/locale/en_US';

const theme = {
  token: {
    // --- Brand Colors ---
    colorPrimary: '#2563eb',
    colorSuccess: '#16a34a',
    colorWarning: '#d97706',
    colorError: '#dc2626',
    colorInfo: '#2563eb',

    // --- Typography ---
    fontFamily: 'Inter, system-ui, -apple-system, sans-serif',
    fontSize: 14,

    // --- Border Radius ---
    borderRadius: 8,
    borderRadiusLG: 12,
    borderRadiusSM: 6,

    // --- Spacing ---
    marginXS: 8,
    marginSM: 12,
    margin: 16,
    marginLG: 24,

    // --- Shadows ---
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
    <ConfigProvider theme={theme} locale={enUS}>
      <YourApp />
    </ConfigProvider>
  );
}
```

### Dark Theme

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

## Common Component Patterns

### Table Page

```tsx
import { Table, Button, Input, Space, Tag } from 'antd';
import { SearchOutlined, PlusOutlined } from '@ant-design/icons';

function UserTable() {
  const columns = [
    { title: 'Name', dataIndex: 'name', key: 'name' },
    {
      title: 'Status',
      dataIndex: 'status',
      key: 'status',
      render: (status) => (
        <Tag color={status === 'active' ? 'green' : 'default'}>
          {status === 'active' ? 'Active' : 'Inactive'}
        </Tag>
      ),
    },
    {
      title: 'Actions',
      key: 'action',
      render: () => (
        <Space>
          <Button type="link" size="small">Edit</Button>
          <Button type="link" size="small" danger>Delete</Button>
        </Space>
      ),
    },
  ];

  return (
    <div>
      <div style={{ marginBottom: 16, display: 'flex', justifyContent: 'space-between' }}>
        <Input prefix={<SearchOutlined />} placeholder="Search users" style={{ width: 240 }} />
        <Button type="primary" icon={<PlusOutlined />}>Add User</Button>
      </div>
      <Table columns={columns} dataSource={data} />
    </div>
  );
}
```

### Form Page

```tsx
import { Form, Input, Select, Button, Card, message } from 'antd';

function CreateForm() {
  const [form] = Form.useForm();

  const onFinish = (values) => {
    console.log(values);
    message.success('Created successfully');
  };

  return (
    <Card title="Create Project">
      <Form form={form} layout="vertical" onFinish={onFinish} style={{ maxWidth: 600 }}>
        <Form.Item label="Project Name" name="name"
          rules={[{ required: true, message: 'Please enter project name' }]}>
          <Input placeholder="Enter project name" />
        </Form.Item>
        <Form.Item label="Project Type" name="type"
          rules={[{ required: true, message: 'Please select project type' }]}>
          <Select placeholder="Select type">
            <Select.Option value="web">Web App</Select.Option>
            <Select.Option value="mobile">Mobile App</Select.Option>
          </Select>
        </Form.Item>
        <Form.Item label="Description" name="description">
          <Input.TextArea rows={4} placeholder="Enter project description" />
        </Form.Item>
        <Form.Item>
          <Space>
            <Button type="primary" htmlType="submit">Create</Button>
            <Button onClick={() => form.resetFields()}>Reset</Button>
          </Space>
        </Form.Item>
      </Form>
    </Card>
  );
}
```

## CLAUDE.md Template for AI

```markdown
## UI Framework: Ant Design 5.x

### Component Usage Rules
- All UI uses antd components, never raw HTML replacements
- Buttons: Button (type: primary / default / text / link / dashed)
- Forms: Form + Form.Item, validation via rules
- Tables: Table + columns definition
- Dialogs: Modal / Drawer
- Notifications: message.success/error/warning
- Icons: import from @ant-design/icons
- Layout: use antd Layout / Row / Col / Space / Flex

### Style Rules
- Do not apply Tailwind classes on antd components (conflicts)
- Customize via ConfigProvider theme tokens
- Spacing via antd Space component or style.marginBottom
- Brand color: #2563eb

### i18n
- English locale configured (enUS)
- Date components auto-localized
```
