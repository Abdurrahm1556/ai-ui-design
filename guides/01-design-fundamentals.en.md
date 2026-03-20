# Design Fundamentals

> Help AI understand your design system, starting with the three pillars: color, typography, and spacing.

## Color Theory

### Building Accessible Palettes

Don't let AI pick random colors. Provide a semantic color scheme:

```
Primary:   #2563EB (blue-600)  — main actions, links
Success:   #16A34A (green-600) — success states
Warning:   #D97706 (amber-600) — attention needed
Danger:    #DC2626 (red-600)   — destructive actions, errors
Neutral:   #6B7280 (gray-500)  — body text, borders, secondary info
```

### Contrast Requirements

| Element | Min Contrast | Example |
|---------|-------------|---------|
| Body text | 4.5:1 | `text-gray-900` on `bg-white` |
| Large headings | 3:1 | `text-gray-700` on `bg-white` |
| UI components | 3:1 | `border-gray-300` on `bg-white` |

**Prompt for AI:**

```
All text must meet WCAG AA contrast requirements. Use gray-900 for body text,
gray-600 for secondary text, gray-400 for placeholders. Never use pure black #000.
```

## Typography

### Modular Scale (1.25 ratio)

```css
/* Recommended type scale */
--text-xs:   0.75rem;   /* 12px — captions */
--text-sm:   0.875rem;  /* 14px — secondary text */
--text-base: 1rem;      /* 16px — body */
--text-lg:   1.25rem;   /* 20px — subheadings */
--text-xl:   1.563rem;  /* 25px — section titles */
--text-2xl:  1.953rem;  /* 31px — page titles */
--text-3xl:  2.441rem;  /* 39px — hero headings */
```

### Line Height Rules

- Body (16px): `line-height: 1.6` (25.6px)
- Headings (24px+): `line-height: 1.2`
- Compact UI (buttons, labels): `line-height: 1`

### Font Pairing

```
Body:  Inter, system-ui, sans-serif
Code:  "JetBrains Mono", "Fira Code", monospace
```

## Spacing System

### 4px / 8px Grid

All spacing should be multiples of 4px. Tailwind defaults follow this system:

```
4px  = p-1   — icon padding
8px  = p-2   — tight element gaps
12px = p-3   — button padding
16px = p-4   — card padding
24px = p-6   — section gaps
32px = p-8   — large section gaps
48px = p-12  — page area spacing
64px = p-16  — page-level large spacing
```

### Before vs After

```html
<!-- Before: arbitrary spacing -->
<div style="padding: 13px 17px; margin-bottom: 11px;">
  <h3 style="margin-bottom: 7px;">Title</h3>
  <p style="margin-bottom: 9px;">Content</p>
</div>

<!-- After: following 4px grid -->
<div class="p-4 mb-3">
  <h3 class="mb-2 text-lg font-semibold">Title</h3>
  <p class="mb-2 text-gray-600">Content</p>
</div>
```

## Visual Hierarchy

### Four Ways to Establish Hierarchy

1. **Size**: Headings large, body medium, captions small
2. **Color weight**: Primary `gray-900`, secondary `gray-600`, tertiary `gray-400`
3. **Font weight**: Headings `font-bold`, body `font-normal`, captions `font-light`
4. **Whitespace**: More breathing room around important content

### Layout Principles

```html
<!-- Standard content area: max-width + centered + horizontal padding -->
<main class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
  <!-- Separate sections with py-12 or py-16 -->
  <section class="py-12">
    <h2 class="text-2xl font-bold text-gray-900">Section Title</h2>
    <p class="mt-4 text-lg text-gray-600">Section description text</p>
  </section>
</main>
```

## Telling AI About Your Design System

Add the following to your project's `CLAUDE.md` or system prompt:

```markdown
## Design Spec
- Colors: blue-600 primary, gray-900 body, gray-600 secondary text
- Fonts: Inter for text, JetBrains Mono for code
- Spacing: strict 4px grid (Tailwind default spacing)
- Border radius: small components rounded-md, cards rounded-lg, pills rounded-full
- Shadows: cards shadow-sm, hover shadow-md, modals shadow-xl
- All text must meet WCAG AA contrast requirements
```
