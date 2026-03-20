# shadcn/ui Setup Guide

> How to set up shadcn/ui and guide AI to use it correctly.

## What Is shadcn/ui

shadcn/ui is not a traditional component library (not installed via npm). It's a collection of copy-paste component code built on Radix UI + Tailwind CSS, copied directly into your project.

**Core advantage**: Full code ownership, deep customization, no dependency on third-party version upgrades.

## Initialization

```bash
# Create Next.js project (recommended)
npx create-next-app@latest my-app --typescript --tailwind --eslint

# Initialize shadcn/ui
npx shadcn@latest init

# Add components you need
npx shadcn@latest add button
npx shadcn@latest add card
npx shadcn@latest add dialog
npx shadcn@latest add form
npx shadcn@latest add input
npx shadcn@latest add table
npx shadcn@latest add dropdown-menu
npx shadcn@latest add toast
```

## Project Structure

```
src/
├── components/
│   └── ui/           ← shadcn components live here
│       ├── button.tsx
│       ├── card.tsx
│       ├── dialog.tsx
│       └── ...
├── lib/
│   └── utils.ts      ← cn() utility function
└── app/
    └── globals.css    ← CSS variables (theme)
```

## Theme Customization

Edit CSS variables in `globals.css`:

```css
@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --primary: 221.2 83.2% 53.3%;       /* Blue primary */
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96%;
    --destructive: 0 84.2% 60.2%;       /* Red danger */
    --border: 214.3 31.8% 91.4%;
    --radius: 0.5rem;                    /* Global border radius */
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

## Telling AI to Use shadcn/ui

Add to your `CLAUDE.md`:

```markdown
## UI Framework
This project uses shadcn/ui (built on Radix UI + Tailwind CSS).

### Rules
- All UI uses shadcn/ui components (import from @/components/ui/)
- Do not hand-code buttons, dialogs, forms — use installed shadcn components
- Customize styles via CSS variables or className overrides
- Use cn() utility to merge Tailwind classes
- Forms use react-hook-form + zod (shadcn/ui recommended stack)

### Installed Components
button, card, dialog, form, input, label, table,
dropdown-menu, toast, tabs, select, checkbox, badge

### Usage Example
import { Button } from "@/components/ui/button"
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Dialog, DialogContent, DialogTrigger } from "@/components/ui/dialog"
```

## Common Composition Patterns

### Form + Validation

```tsx
import { useForm } from "react-hook-form"
import { zodResolver } from "@hookform/resolvers/zod"
import * as z from "zod"
import { Form, FormControl, FormField, FormItem, FormLabel, FormMessage } from "@/components/ui/form"
import { Input } from "@/components/ui/input"
import { Button } from "@/components/ui/button"

const schema = z.object({
  email: z.string().email("Please enter a valid email"),
  name: z.string().min(2, "Name must be at least 2 characters"),
})

export function MyForm() {
  const form = useForm({ resolver: zodResolver(schema) })

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
        <FormField control={form.control} name="email" render={({ field }) => (
          <FormItem>
            <FormLabel>Email</FormLabel>
            <FormControl><Input placeholder="you@example.com" {...field} /></FormControl>
            <FormMessage />
          </FormItem>
        )} />
        <Button type="submit">Submit</Button>
      </form>
    </Form>
  )
}
```

### Data Table + Sorting

```tsx
import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from "@/components/ui/table"
import { Badge } from "@/components/ui/badge"

<Table>
  <TableHeader>
    <TableRow>
      <TableHead>Name</TableHead>
      <TableHead>Status</TableHead>
      <TableHead className="text-right">Amount</TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    <TableRow>
      <TableCell>Order #001</TableCell>
      <TableCell><Badge variant="default">Completed</Badge></TableCell>
      <TableCell className="text-right">$250.00</TableCell>
    </TableRow>
  </TableBody>
</Table>
```
