# Landing Page Prompt Templates

> Copy into CLAUDE.md or send directly to AI to generate professional landing page sections.

## Hero Section

### Prompt

```
Create a modern hero section:
- Left: large heading (text-4xl lg:text-6xl font-bold) + subtitle (text-xl text-gray-600) + two CTA buttons (primary + secondary)
- Right: product screenshot or illustration placeholder
- Use Tailwind CSS, mobile-first
- Stack vertically on mobile, side-by-side on desktop
- Light gradient or white background
```

### Reference Structure

```html
<section class="relative overflow-hidden bg-white">
  <div class="mx-auto max-w-7xl px-4 py-16 sm:px-6 lg:px-8 lg:py-24">
    <div class="flex flex-col items-center gap-12 lg:flex-row">
      <!-- Copy -->
      <div class="flex-1 text-center lg:text-left">
        <h1 class="text-4xl font-bold tracking-tight text-gray-900 sm:text-5xl lg:text-6xl">
          Make your product<br />
          <span class="text-blue-600">stand out</span>
        </h1>
        <p class="mt-6 text-lg text-gray-600 max-w-xl">
          One sentence describing the core value proposition.
        </p>
        <div class="mt-8 flex flex-col gap-3 sm:flex-row sm:justify-center lg:justify-start">
          <a href="#" class="rounded-lg bg-blue-600 px-6 py-3 text-sm font-semibold
            text-white shadow-sm hover:bg-blue-700 transition-colors">
            Get started free
          </a>
          <a href="#" class="rounded-lg px-6 py-3 text-sm font-semibold text-gray-700
            ring-1 ring-gray-300 hover:bg-gray-50 transition-colors">
            View demo
          </a>
        </div>
      </div>
      <!-- Visual -->
      <div class="flex-1">
        <div class="aspect-[4/3] rounded-2xl bg-gray-100 shadow-xl"></div>
      </div>
    </div>
  </div>
</section>
```

## Features Grid

### Prompt

```
Create a 3-column feature showcase:
- Centered title + description paragraph
- Below: 3-column grid (1 col mobile, 2 col tablet, 3 col desktop)
- Each feature card: icon + title + description
- Tailwind, bg-gray-50 background, white cards with shadow-sm
```

### Reference Structure

```html
<section class="bg-gray-50 py-16 lg:py-24">
  <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
    <div class="text-center">
      <h2 class="text-3xl font-bold text-gray-900">Core Features</h2>
      <p class="mt-4 text-lg text-gray-600">Three key advantages, concise and clear</p>
    </div>
    <div class="mt-12 grid grid-cols-1 gap-8 sm:grid-cols-2 lg:grid-cols-3">
      <div class="rounded-xl bg-white p-6 shadow-sm">
        <div class="flex h-10 w-10 items-center justify-center rounded-lg bg-blue-100">
          <svg class="h-5 w-5 text-blue-600"><!-- icon --></svg>
        </div>
        <h3 class="mt-4 text-lg font-semibold text-gray-900">Feature Name</h3>
        <p class="mt-2 text-sm text-gray-600">Feature description, two lines is ideal.</p>
      </div>
      <!-- Repeat 2 more cards -->
    </div>
  </div>
</section>
```

## Pricing Table

### Prompt

```
Create a pricing section with 3 plans side by side:
- Basic, Pro (recommended, highlighted), Enterprise
- Each card: plan name, price, feature list, CTA button
- Recommended plan uses ring-2 ring-blue-600 + "Recommended" badge
- Stack vertically on mobile, 3 columns on desktop
```

## CTA Section

### Prompt

```
Create a bottom-of-page CTA section:
- Dark background (bg-gray-900) or gradient
- Centered large heading + description + prominent CTA button
- Keep it punchy — two lines of description max
```

### Reference Structure

```html
<section class="bg-gray-900 py-16 lg:py-24">
  <div class="mx-auto max-w-4xl px-4 text-center sm:px-6 lg:px-8">
    <h2 class="text-3xl font-bold text-white sm:text-4xl">
      Ready to get started?
    </h2>
    <p class="mt-4 text-lg text-gray-300">
      Free 14-day trial. No credit card required.
    </p>
    <a href="#" class="mt-8 inline-block rounded-lg bg-blue-600 px-8 py-3
      text-sm font-semibold text-white shadow-sm hover:bg-blue-700 transition-colors">
      Start now
    </a>
  </div>
</section>
```

## Footer

### Prompt

```
Create a website footer:
- 4-column link area (Product, Resources, Company, Legal)
- Bottom: copyright + social media icons
- 2 columns on mobile, 4 on desktop
- bg-gray-900 background, gray-400 text
```
