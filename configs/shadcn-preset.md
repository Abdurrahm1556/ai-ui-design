# shadcn/ui 配置指南

> 如何设置 shadcn/ui 并引导 AI 正确使用它。

## 什么是 shadcn/ui

shadcn/ui 不是传统的组件库（不通过 npm install 安装）。它是一套可复制粘贴的组件代码，基于 Radix UI + Tailwind CSS，直接复制到你的项目中。

**核心优势**：完全控制代码、可深度定制、不依赖第三方版本升级。

## 初始化

```bash
# 创建 Next.js 项目（推荐）
npx create-next-app@latest my-app --typescript --tailwind --eslint

# 初始化 shadcn/ui
npx shadcn@latest init

# 安装需要的组件
npx shadcn@latest add button
npx shadcn@latest add card
npx shadcn@latest add dialog
npx shadcn@latest add form
npx shadcn@latest add input
npx shadcn@latest add table
npx shadcn@latest add dropdown-menu
npx shadcn@latest add toast
```

## 项目结构

```
src/
├── components/
│   └── ui/           ← shadcn 组件在这里
│       ├── button.tsx
│       ├── card.tsx
│       ├── dialog.tsx
│       └── ...
├── lib/
│   └── utils.ts      ← cn() 工具函数
└── app/
    └── globals.css    ← CSS 变量（主题色）
```

## 主题定制

编辑 `globals.css` 中的 CSS 变量：

```css
@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --primary: 221.2 83.2% 53.3%;       /* 蓝色主色 */
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96%;
    --destructive: 0 84.2% 60.2%;       /* 红色危险 */
    --border: 214.3 31.8% 91.4%;
    --radius: 0.5rem;                    /* 全局圆角 */
  }
  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
    --primary: 217.2 91.2% 59.8%;
    --primary-foreground: 222.2 47.4% 11.2%;
    --border: 217.2 32.6% 17.5%;
  }
}
```

## 告诉 AI 使用 shadcn/ui

放入 `CLAUDE.md`：

```markdown
## UI 框架
本项目使用 shadcn/ui（基于 Radix UI + Tailwind CSS）。

### 规则
- 所有 UI 使用 shadcn/ui 组件（从 @/components/ui/ 导入）
- 不要手写按钮、弹窗、表单等基础组件，使用已安装的 shadcn 组件
- 样式定制通过修改 CSS 变量或传入 className 覆盖
- 使用 cn() 工具函数合并 Tailwind 类名
- 表单使用 react-hook-form + zod（shadcn/ui 官方推荐）

### 已安装的组件
button, card, dialog, form, input, label, table,
dropdown-menu, toast, tabs, select, checkbox, badge

### 用法示例
import { Button } from "@/components/ui/button"
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Dialog, DialogContent, DialogTrigger } from "@/components/ui/dialog"
```

## 常用组合模式

### 表单 + 验证

```tsx
import { useForm } from "react-hook-form"
import { zodResolver } from "@hookform/resolvers/zod"
import * as z from "zod"
import { Form, FormControl, FormField, FormItem, FormLabel, FormMessage } from "@/components/ui/form"
import { Input } from "@/components/ui/input"
import { Button } from "@/components/ui/button"

const schema = z.object({
  email: z.string().email("请输入有效的邮箱"),
  name: z.string().min(2, "姓名至少 2 个字符"),
})

export function MyForm() {
  const form = useForm({ resolver: zodResolver(schema) })

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
        <FormField control={form.control} name="email" render={({ field }) => (
          <FormItem>
            <FormLabel>邮箱</FormLabel>
            <FormControl><Input placeholder="you@example.com" {...field} /></FormControl>
            <FormMessage />
          </FormItem>
        )} />
        <Button type="submit">提交</Button>
      </form>
    </Form>
  )
}
```

### 数据表格 + 排序

```tsx
import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from "@/components/ui/table"
import { Badge } from "@/components/ui/badge"

<Table>
  <TableHeader>
    <TableRow>
      <TableHead>名称</TableHead>
      <TableHead>状态</TableHead>
      <TableHead className="text-right">金额</TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    <TableRow>
      <TableCell>订单 #001</TableCell>
      <TableCell><Badge variant="default">已完成</Badge></TableCell>
      <TableCell className="text-right">¥250.00</TableCell>
    </TableRow>
  </TableBody>
</Table>
```
