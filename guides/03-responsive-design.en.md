# Responsive Design

> Guide AI to produce layouts that look great on every device, starting mobile-first.

## Mobile-First Approach

Core principle: **Write mobile styles first, then scale up with breakpoints.**

```html
<!-- Correct: mobile-first -->
<div class="px-4 sm:px-6 lg:px-8">
  <h1 class="text-2xl sm:text-3xl lg:text-4xl">Title</h1>
</div>

<!-- Wrong: desktop-first scaling down -->
<div class="px-8 md:px-6 sm:px-4">  <!-- Backwards! -->
```

**Prompt for AI:**

```
Always use mobile-first responsive design. Write base styles without breakpoint
prefixes (for mobile), then progressively enhance with sm:, md:, lg: prefixes.
```

## Breakpoint Strategy

### Tailwind Default Breakpoints

| Breakpoint | Width | Typical Device |
|------------|-------|----------------|
| Default | 0px+ | Phone portrait |
| `sm` | 640px+ | Phone landscape, small tablet |
| `md` | 768px+ | Tablet portrait |
| `lg` | 1024px+ | Tablet landscape, small laptop |
| `xl` | 1280px+ | Laptop, desktop |
| `2xl` | 1536px+ | Large display |

### In Practice, Focus on Three

- **Default** (phone): Single column layout
- **`md`** (tablet): Two column layout
- **`lg`** (desktop): Full multi-column layout

## Common Responsive Patterns

### Stack to Row

```html
<!-- Mobile: vertical stack / Tablet+: horizontal row -->
<div class="flex flex-col gap-4 md:flex-row">
  <div class="md:w-1/2">Left content</div>
  <div class="md:w-1/2">Right content</div>
</div>
```

### Collapsible Sidebar

```html
<div class="flex min-h-screen">
  <!-- Sidebar: hidden on mobile, visible on desktop -->
  <aside class="hidden lg:flex lg:w-64 lg:flex-col bg-gray-900">
    <!-- Nav content -->
  </aside>
  <!-- Main area: always visible -->
  <main class="flex-1 px-4 py-6 lg:px-8">
    <!-- Mobile hamburger button -->
    <button class="lg:hidden mb-4 rounded-lg p-2 text-gray-500 hover:bg-gray-100">
      <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
          d="M4 6h16M4 12h16M4 18h16" />
      </svg>
    </button>
    <!-- Page content -->
  </main>
</div>
```

### Adaptive Grid

```html
<!-- 1 col mobile / 2 col tablet / 3 col desktop / 4 col large -->
<div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
  <div class="rounded-xl bg-white p-4 shadow-sm ring-1 ring-gray-200">Card 1</div>
  <div class="rounded-xl bg-white p-4 shadow-sm ring-1 ring-gray-200">Card 2</div>
  <div class="rounded-xl bg-white p-4 shadow-sm ring-1 ring-gray-200">Card 3</div>
  <div class="rounded-xl bg-white p-4 shadow-sm ring-1 ring-gray-200">Card 4</div>
</div>
```

### Responsive Table

```html
<!-- Horizontal scroll on small screens -->
<div class="overflow-x-auto">
  <table class="min-w-full divide-y divide-gray-200">
    <!-- Table content -->
  </table>
</div>

<!-- Or: switch to card layout on mobile -->
<div class="hidden md:block">
  <!-- Desktop table -->
</div>
<div class="space-y-4 md:hidden">
  <!-- Mobile card list -->
</div>
```

## Touch Targets and Mobile UX

### Minimum Touch Area

Buttons and tappable areas should be at least 44x44px:

```html
<!-- Correct: large enough touch target -->
<button class="min-h-[44px] min-w-[44px] px-4 py-3">Tap me</button>

<!-- Icon buttons also need sufficient touch area -->
<button class="flex h-11 w-11 items-center justify-center rounded-full hover:bg-gray-100">
  <svg class="h-5 w-5" ...></svg>
</button>
```

### Mobile Input Optimization

```html
<!-- Use correct input types to trigger appropriate virtual keyboards -->
<input type="email" inputmode="email" />     <!-- email keyboard -->
<input type="tel" inputmode="tel" />          <!-- number pad -->
<input type="url" inputmode="url" />          <!-- URL keyboard -->
<input type="number" inputmode="decimal" />   <!-- decimal keypad -->
```

### Safe Area Insets

```html
<!-- Handle notch and home indicator -->
<div class="pb-safe">
  <nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200
    px-4 pb-[env(safe-area-inset-bottom)]">
    <!-- Bottom navigation -->
  </nav>
</div>
```

## Prompting AI for Responsive Layouts

Add to your `CLAUDE.md`:

```markdown
## Responsive Design Rules
- Always mobile-first: base styles for phone, sm/md/lg progressive
- Phone: single column, px-4 horizontal padding
- Tablet (md): two columns allowed, px-6
- Desktop (lg): multi-column, max-w-7xl centered, px-8
- All tappable elements minimum 44x44px
- Tables must scroll horizontally on small screens
- Navigation collapses to hamburger on mobile
```
