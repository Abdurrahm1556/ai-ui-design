# Tailwind CSS Patterns

> Utility-first patterns, dark mode, animations, config tips, and anti-patterns to avoid.

## Utility-First Methodology

### Core Idea

Don't write custom CSS. Compose Tailwind utilities. When a combination repeats, extract it into a component, not a CSS class.

```html
<!-- Recommended: direct utility composition -->
<button class="rounded-lg bg-blue-600 px-4 py-2.5 text-sm font-medium text-white
  hover:bg-blue-700 transition-colors">
  Submit
</button>

<!-- Not recommended: custom CSS class -->
<button class="btn-primary">Submit</button>
<style>
.btn-primary { /* bunch of custom styles */ }
</style>
```

## Common Class Combos Cheatsheet

### Centering

```html
<!-- Flex center -->
<div class="flex items-center justify-center">

<!-- Grid center -->
<div class="grid place-items-center">

<!-- Absolute center -->
<div class="absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2">
```

### Text Truncation

```html
<!-- Single line -->
<p class="truncate">Long text here...</p>

<!-- Multi-line clamp (2 lines) -->
<p class="line-clamp-2">Long text here...</p>
```

### Aspect Ratios

```html
<div class="aspect-video">16:9 video container</div>
<div class="aspect-square">Square</div>
<div class="aspect-[4/3]">4:3 ratio</div>
```

### Dividers

```html
<ul class="divide-y divide-gray-200">
  <li class="py-4">Item 1</li>
  <li class="py-4">Item 2</li>
</ul>
```

### Gradient Backgrounds

```html
<div class="bg-gradient-to-r from-blue-600 to-purple-600 text-white p-8 rounded-xl">
  Gradient content
</div>

<!-- Gradient text -->
<h1 class="bg-gradient-to-r from-blue-600 to-purple-600 bg-clip-text text-transparent
  text-4xl font-bold">
  Gradient Text
</h1>
```

## Dark Mode

### Class-Based Strategy

```html
<html class="dark">
  <body class="bg-white text-gray-900 dark:bg-gray-950 dark:text-gray-100">
    <div class="bg-gray-50 dark:bg-gray-900 rounded-xl p-6
      ring-1 ring-gray-200 dark:ring-gray-800">
      <h2 class="text-gray-900 dark:text-white">Title</h2>
      <p class="text-gray-600 dark:text-gray-400">Description</p>
    </div>
  </body>
</html>
```

### Dark Mode Color Mapping

| Purpose | Light | Dark |
|---------|-------|------|
| Page bg | `bg-white` | `dark:bg-gray-950` |
| Card bg | `bg-gray-50` | `dark:bg-gray-900` |
| Primary text | `text-gray-900` | `dark:text-gray-100` |
| Secondary text | `text-gray-600` | `dark:text-gray-400` |
| Borders | `ring-gray-200` | `dark:ring-gray-800` |
| Hover bg | `hover:bg-gray-50` | `dark:hover:bg-gray-800` |

## Animations and Transitions

### Common Transitions

```html
<!-- Color transition (button hover) -->
<button class="bg-blue-600 hover:bg-blue-700 transition-colors duration-150">

<!-- Shadow transition (card hover) -->
<div class="shadow-sm hover:shadow-md transition-shadow duration-200">

<!-- Transform transition (image zoom) -->
<img class="hover:scale-105 transition-transform duration-300">

<!-- Opacity transition (fade) -->
<div class="opacity-0 hover:opacity-100 transition-opacity duration-300">
```

### Entry Animations

```html
<!-- Pulse skeleton loader -->
<div class="animate-pulse rounded-lg bg-gray-200 h-4 w-3/4"></div>

<!-- Spinner -->
<svg class="animate-spin h-5 w-5 text-blue-600">...</svg>

<!-- Bounce indicator -->
<div class="animate-bounce">Scroll down</div>
```

## tailwind.config Design Tokens

```js
// tailwind.config.js — key customizations
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: {
          50:  '#eff6ff',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
        },
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['"JetBrains Mono"', 'monospace'],
      },
      borderRadius: {
        '4xl': '2rem',
      },
    },
  },
  darkMode: 'class',
}
```

## Anti-Patterns

### Don't Do This

```html
<!-- Anti-pattern 1: inline style overrides -->
<div class="p-4" style="padding: 13px;">  <!-- Why? -->

<!-- Anti-pattern 2: !important abuse -->
<div class="!mt-0">  <!-- There's a better way -->

<!-- Anti-pattern 3: repeating 20 classes without extracting a component -->
<!-- When the same 20 classes appear 5 times, extract a React/Vue component -->

<!-- Anti-pattern 4: @apply turning Tailwind back into traditional CSS -->
.btn {
  @apply rounded-lg bg-blue-600 px-4 py-2.5 text-sm font-medium text-white;
  /* Defeats the purpose of utility-first */
}
```

### Do This Instead

```jsx
// Extract into components, not CSS classes
function Button({ children, variant = 'primary' }) {
  const styles = {
    primary: 'bg-blue-600 text-white hover:bg-blue-700',
    secondary: 'bg-white text-gray-700 ring-1 ring-gray-300 hover:bg-gray-50',
  }
  return (
    <button className={`inline-flex items-center rounded-lg px-4 py-2.5
      text-sm font-medium transition-colors ${styles[variant]}`}>
      {children}
    </button>
  )
}
```
