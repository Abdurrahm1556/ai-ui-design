# Accessibility

> Make AI-generated code friendly to all users, including those using screen readers and keyboards.

## WCAG Essentials for Developers

### Four Principles

1. **Perceivable**: Information must be presentable (text alternatives, captions)
2. **Operable**: Interface works via keyboard and assistive technology
3. **Understandable**: Information and operations are comprehensible
4. **Robust**: Content can be parsed by various tools

### AA Minimum Requirements

- Body text contrast >= 4.5:1
- Large text contrast >= 3:1
- All functionality available via keyboard
- Form inputs have associated labels
- Images have alt text

## ARIA Labels and Roles

### Common ARIA Attributes

```html
<!-- Buttons: icon buttons need aria-label -->
<button aria-label="Close dialog" class="p-2 rounded-full hover:bg-gray-100">
  <svg class="h-5 w-5"><!-- X icon --></svg>
</button>

<!-- Navigation: use aria-label to distinguish multiple navs -->
<nav aria-label="Main navigation">...</nav>
<nav aria-label="Breadcrumb">...</nav>

<!-- Dialog: role + aria-modal + aria-labelledby -->
<div role="dialog" aria-modal="true" aria-labelledby="dialog-title">
  <h2 id="dialog-title">Confirm Action</h2>
</div>

<!-- Live regions: aria-live announces changes to screen readers -->
<div aria-live="polite" class="sr-only">Saved successfully</div>

<!-- Expand/collapse -->
<button aria-expanded="false" aria-controls="menu-content">Menu</button>
<div id="menu-content" hidden>...</div>
```

### Before vs After

```html
<!-- Before: screen reader doesn't know what this is -->
<div onclick="closeModal()" class="cursor-pointer">X</div>

<!-- After: semantic, accessible -->
<button aria-label="Close" onclick="closeModal()"
  class="flex h-8 w-8 items-center justify-center rounded-full hover:bg-gray-100">
  <svg class="h-4 w-4" aria-hidden="true"><!-- X icon --></svg>
</button>
```

## Keyboard Navigation

### Focus Management

```html
<!-- Visible focus ring -->
<button class="rounded-lg bg-blue-600 px-4 py-2 text-white
  focus-visible:outline focus-visible:outline-2
  focus-visible:outline-offset-2 focus-visible:outline-blue-600">
  Action
</button>

<!-- Skip navigation link (place at start of body) -->
<a href="#main-content"
  class="sr-only focus:not-sr-only focus:absolute focus:z-50
  focus:rounded-lg focus:bg-blue-600 focus:px-4 focus:py-2 focus:text-white">
  Skip to main content
</a>
```

### Keyboard Interaction Specs

| Component | Key | Behavior |
|-----------|-----|----------|
| Button | Enter / Space | Trigger action |
| Link | Enter | Navigate |
| Dialog | Escape | Close |
| Tabs | Arrow keys | Switch tab |
| Dropdown | Arrow keys | Move up/down |
| Dropdown | Escape | Close |

### Tab Order

```html
<!-- Use tabindex to manage focus order -->
<div tabindex="0">Focusable custom element</div>
<div tabindex="-1">Only focusable via JS focus()</div>
<!-- Never use tabindex > 0 -->
```

## Screen Reader Friendly Patterns

### Visually Hidden but Readable

```html
<!-- Tailwind's sr-only: hidden visually but readable by screen readers -->
<label for="search" class="sr-only">Search</label>
<input id="search" type="search" placeholder="Search..." />

<!-- Decorative icons hidden from screen readers -->
<svg aria-hidden="true" class="h-5 w-5">...</svg>

<!-- Meaningful images get descriptive alt text -->
<img src="chart.png" alt="2024 sales trend chart showing 23% YoY growth in Q4" />

<!-- Purely decorative images -->
<img src="decoration.svg" alt="" role="presentation" />
```

### Accessible Forms

```html
<!-- Every input needs an associated label -->
<div>
  <label for="name" class="block text-sm font-medium text-gray-700">Name</label>
  <input id="name" type="text" required aria-required="true"
    class="mt-1 block w-full rounded-lg border-gray-300" />
</div>

<!-- Error messages linked to input -->
<div>
  <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
  <input id="email" type="email" aria-invalid="true" aria-describedby="email-err"
    class="mt-1 block w-full rounded-lg border-red-300" />
  <p id="email-err" role="alert" class="mt-1 text-sm text-red-600">
    Please enter a valid email address
  </p>
</div>
```

## Color Contrast

### Testing Tools

- Chrome DevTools: Inspect > view contrast ratio
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- Figma Plugin: Stark

### Safe Color Combinations

| Text Color | Background | Ratio | Pass? |
|------------|-----------|-------|-------|
| `gray-900` | `white` | 15.4:1 | AA + AAA |
| `gray-600` | `white` | 5.7:1 | AA |
| `gray-500` | `white` | 4.6:1 | AA (barely) |
| `gray-400` | `white` | 3.0:1 | Large text only |
| `white` | `blue-600` | 6.3:1 | AA + AAA |

## Prompting AI for Accessible Code

```markdown
## Accessibility Requirements
- All images have alt text (decorative images use alt="")
- All form inputs have associated labels
- Buttons have descriptive text or aria-label
- Dialogs have role="dialog" and aria-labelledby
- Use semantic HTML (nav, main, header, footer, section)
- Focus styles visible (focus-visible:outline)
- Color contrast meets WCAG AA
```
